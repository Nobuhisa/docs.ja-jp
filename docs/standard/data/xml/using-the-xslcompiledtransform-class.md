---
title: "XslCompiledTransform クラスの使用"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
caps.latest.revision: "3"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 5a5c71a7796790343bf39de5bbfd03997c25d5f0
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="using-the-xslcompiledtransform-class"></a>XslCompiledTransform クラスの使用
<xref:System.Xml.Xsl.XslCompiledTransform> クラスは Microsoft .NET Framework XSLT プロセッサです。 このクラスは、スタイル シートをコンパイルし、XSLT 変換を実行するために使用されます。  
  
> [!NOTE]
>  全体的なパフォーマンスは <xref:System.Xml.Xsl.XslCompiledTransform> クラスの方が <xref:System.Xml.Xsl.XslTransform> クラスより優れていますが、<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> クラスの <xref:System.Xml.Xsl.XslCompiledTransform> メソッドが変換で初めて呼び出されたときは、<xref:System.Xml.Xsl.XslTransform.Load%2A> クラスの <xref:System.Xml.Xsl.XslTransform> メソッドよりパフォーマンスが劣る場合があります。 これは、XSLT ファイルを読み込む前にコンパイルする必要があるためです。 詳細については、次のブログの投稿を参照してください: [XslCompiledTransform は XslTransform より遅いですか?](http://go.microsoft.com/fwlink/?LinkId=130590)  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XslCompiledTransform クラスへの入力](../../../../docs/standard/data/xml/inputs-to-the-xslcompiledtransform-class.md)  
 使用可能な XSLT 入力オプションについて説明します。  
  
 [XslCompiledTransform クラスの出力オプション](../../../../docs/standard/data/xml/output-options-on-the-xslcompiledtransform-class.md)  
 使用可能な XSLT 出力オプションについて説明します。  
  
 [XSLT 処理中に外部のリソースの解決](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
 外部リソースを解決するための <xref:System.Xml.XmlResolver> クラスの使用について説明します。  
  
 [XSLT スタイル シートを拡張します。](../../../../docs/standard/data/xml/extending-xslt-style-sheets.md)  
 XSLT の拡張機能のサポートについて説明します。  
  
|||  
|-|-|  
|[XSLT エラーの解決](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)|W3C (World Wide Web Consortium) 勧告『XSLT 1.0』で許可されている随意動作を示し、<xref:System.Xml.Xsl.XslCompiledTransform> クラスによるこれらの動作の処理方法を説明します。|  
|[方法: ノード フラグメントを変換](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)|ノード フラグメントの変換方法を説明します。|  
  
## <a name="related-sections"></a>関連項目  
 [XslTransform クラスからの移行](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 <xref:System.Xml.Xsl.XslTransform> クラスからコードを移行する方法について説明します。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Xml.Xsl.XsltSettings>  
 <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>
