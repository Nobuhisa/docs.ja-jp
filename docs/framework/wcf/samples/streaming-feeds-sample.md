---
title: "ストリーミング フィードのサンプル"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f1228c0-daaa-45f0-b93e-c4a158113744
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: f2789c6756d8e22dae9eb3189dfb616d162ad906
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="streaming-feeds-sample"></a>ストリーミング フィードのサンプル
このサンプルでは、多数の項目が含まれた配信フィードを管理する方法を示します。 サーバー側のサンプルは、フィード内での個々の <xref:System.ServiceModel.Syndication.SyndicationItem> オブジェクトの作成を、項目がネットワーク ストリームに書き込まれる直前まで遅らせる方法を示しています。  
  
 クライアント側のサンプルは、カスタム配信フィード フォーマッタを使用して個々の項目をネットワーク ストリームから読み取り、読み取られたフィードがメモリに完全にバッファーされないようにする方法を示しています。  
  
 配信 API のストリーミング機能を十分に示すため、このサンプルでは、無数の項目を含むフィードがサーバーによって公開されるという多少通常とは異なるシナリオを使用しています。 この場合、サーバーは、クライアントがフィードから特定の数 (既定では 10) の項目を読み取ったと判断するまで、新しい項目をフィードに対して生成し続けます。 処理を簡単にするために、クライアントとサーバーは両方とも同じプロセスで実装され、共有 `ItemCounter` オブジェクトを使用して、クライアントによって生成された項目の数を追跡します。 `ItemCounter` 型は、サンプル シナリオを正常に終了するためにのみ存在し、示されるパターンの重要な要素ではありません。  
  
 デモでは、使用[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]反復子 (を使用して、`yield``return`キーワード コンストラクト)。 反復子[!INCLUDE[crabout](../../../../includes/crabout-md.md)]、MSDN の「反復子の使用」を参照してください。  
  
## <a name="service"></a>サービス  
 次のコードに示すように、サービスは、1 つの操作で構成される基本的な <xref:System.ServiceModel.Web.WebGetAttribute> コントラクトを実装します。  
  
```  
[ServiceContract]  
interface IStreamingFeedService  
{  
    [WebGet]  
    [OperationContract]  
    Atom10FeedFormatter StreamedFeed();  
}  
```  
  
 次のコードに示すように、サービスは、`ItemGenerator` クラスを使用してこのコントラクトを実装し、反復子を使用する <xref:System.ServiceModel.Syndication.SyndicationItem> インスタンスの無数のストリームを作成します。  
  
```  
class ItemGenerator  
{  
    public IEnumerable<SyndicationItem> GenerateItems()  
    {  
        while (counter.GetCount() < maxItemsRead)  
        {  
            itemsReturned++;  
            yield return CreateNextItem();  
        }  
  
    }  
    ...  
}  
```  
  
 サービスの実装によってフィードが作成されると、項目のバッファされたコレクションの代わりに `ItemGenerator.GenerateItems()` の出力が使用されます。  
  
```  
public Atom10FeedFormatter StreamedFeed()  
{  
    SyndicationFeed feed = new SyndicationFeed("Streamed feed", "Feed to test streaming", null);  
    //Generate an infinite stream of items. Both the client and the service share  
    //a reference to the ItemCounter, which allows the sample to terminate  
    //execution after the client has read 10 items from the stream  
    ItemGenerator itemGenerator = new ItemGenerator(this.counter, 10);  
  
    feed.Items = itemGenerator.GenerateItems();  
    return feed.GetAtom10Formatter();  
}  
```  
  
 その結果、項目のストリームはメモリに完全にはバッファされません。 ブレークポイントを設定してこの動作を確認することができます、`yield``return`内のステートメント、`ItemGenerator.GenerateItems()`メソッドと、サービスの結果が返された後に初めてこのブレークポイントが発生したことに注意してください、`StreamedFeed()`メソッドです。  
  
## <a name="client"></a>クライアント  
 このサンプルのクライアントでは、フィードの項目をメモリにバッファする代わりに、個々の項目の実体化を遅延させるカスタム <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 実装を使用します。 カスタム `StreamedAtom10FeedFormatter` インスタンスの使用方法は次のとおりです。  
  
```  
XmlReader reader = XmlReader.Create("http://localhost:8000/Service/Feeds/StreamedFeed");  
StreamedAtom10FeedFormatter formatter = new StreamedAtom10FeedFormatter(counter);  
  
SyndicationFeed feed = formatter.ReadFrom(reader);  
```  
  
 通常、<xref:System.ServiceModel.Syndication.SyndicationFeedFormatter.ReadFrom%28System.Xml.XmlReader%29> の呼び出しは、フィードのコンテンツ全体がネットワークから読み取られ、メモリにバッファされるまで返されません。 ただし、次のコードに示すように、`StreamedAtom10FeedFormatter` オブジェクトによって <xref:System.ServiceModel.Syndication.Atom10FeedFormatter.ReadItems%28System.Xml.XmlReader%2CSystem.ServiceModel.Syndication.SyndicationFeed%2CSystem.Boolean%40%29> がオーバーライドされ、バッファ内のコレクションの代わりに反復子が返されます。  
  
```  
protected override IEnumerable<SyndicationItem> ReadItems(XmlReader reader, SyndicationFeed feed, out bool areAllItemsRead)  
{  
    areAllItemsRead = false;  
    return DelayReadItems(reader, feed);  
}  
  
private IEnumerable<SyndicationItem> DelayReadItems(XmlReader reader, SyndicationFeed feed)  
{  
    while (reader.IsStartElement("entry", "http://www.w3.org/2005/Atom"))  
    {  
        yield return this.ReadItem(reader, feed);  
    }  
  
    reader.ReadEndElement();  
}  
```  
  
 その結果、各項目は、`ReadItems()` の結果を走査するクライアント アプリケーションで使用可能な状態になるまで、ネットワークから読み取られません。 ブレークポイントを設定してこの動作を確認することができます、`yield``return`ステートメントの内側`StreamedAtom10FeedFormatter.DelayReadItems()`への呼び出し後に最初にこのブレークポイントが検出されることに注意`ReadFrom()`が完了します。  
  
 次の手順は、サンプルをビルドして実行する方法を示しています。 クライアントが 10 個の項目を読み取った後にサーバーによる項目の生成が停止されると、クライアントが読み取った項目数は 10 個より非常に多く出力されます。 これは、サンプルで使用されたネットワーキング バインディングによってデータが 4 キロバイト (KB) セグメントで転送されることが原因です。 このような場合、クライアントは、項目を 1 つでも読み取る前に 4 KB の項目データを受信します。 これは通常の動作です (適切にサイズが調整されたセグメントでストリーミングされた HTTP データを送信すると、パフォーマンスが向上します)。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1.  実行したことを確認してください、 [Windows Communication Foundation サンプルの 1 回限りのセットアップ手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)です。  
  
2.  ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)」の手順に従います。  
  
3.  1 つまたは複数コンピューター構成でサンプルを実行する手順についてで[Windows Communication Foundation サンプルの実行](../../../../docs/framework/wcf/samples/running-the-samples.md)です。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「 [.NET Framework 4 向けの Windows Communication Foundation (WCF) および Windows Workflow Foundation (WF) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780) 」にアクセスして、 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。 このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Syndication\StreamingFeeds`  
  
## <a name="see-also"></a>関連項目  
 [スタンドアロン診断フィード](../../../../docs/framework/wcf/samples/stand-alone-diagnostics-feed-sample.md)
