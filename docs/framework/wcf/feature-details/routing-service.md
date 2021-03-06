---
title: "ルーティング サービス"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ca7c216a-5141-4132-8193-102c181d2eba
caps.latest.revision: "13"
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.openlocfilehash: a4f58c5124e229f1692dabbb0abded0e21a346f7
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="routing-service"></a>ルーティング サービス
ルーティング サービスは、メッセージ ルーターとして機能する、汎用の SOAP 中継局です。 ルーティング サービスの主要な機能は、メッセージのコンテンツに基づいてメッセージをルーティングする機能です。これにより、メッセージのヘッダーまたはメッセージ本文内に含まれる値に基づいて、メッセージをクライアント エンドポイントに転送できます。  
  
 <xref:System.ServiceModel.Routing.RoutingService> は、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] サービスとして <xref:System.ServiceModel.Routing> 名前空間で実装されます。 ルーティング サービスは、メッセージを受信し、その内容に基づいて各メッセージを 1 つ以上のクライアント エンドポイントにルーティングする、1 つ以上のサービス エンドポイントを公開します。 このサービスには、次の機能が用意されています。  
  
-   コンテンツ ベースのルーティング  
  
    -   サービスの集計  
  
    -   サービスのバージョン管理  
  
    -   優先度ルーティング  
  
    -   動的構成  
  
-   プロトコル ブリッジ  
  
-   SOAP 処理  
  
-   高度なエラー処理  
  
-   バックアップ エンドポイント  
  
 上記の機能の 1 つ以上を実現する中間サービスを作成することもできますが、このような実装では、特定のシナリオまたはソリューションに制限され、新しいアプリケーションにすぐに適用できません。  
  
 ルーティング サービスは、動的に構成できるプラグ可能な汎用の SOAP 中継局を提供します。この中継局は、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] のサービスおよびチャネル モデルと互換性があり、SOAP ベースのメッセージのコンテンツ ベースのルーティングを実行できます。  
  
> [!NOTE]
>  ルーティング サービスは、現在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] REST サービスのルーティングをサポートしていません。  REST 呼び出しをルーティングするには、使用を検討して<xref:System.Web.Routing>または[アプリケーション要求ルーティング処理](http://go.microsoft.com/fwlink/?LinkId=164589)(http://go.microsoft.com/fwlink/?LinkId=164589)。  
  
## <a name="content-based-routing"></a>コンテンツ ベースのルーティング  
 コンテンツ ベースのルーティングは、メッセージに含まれている 1 つ以上の値に基づいて、メッセージをルーティングする機能です。 ルーティング サービスでは、各メッセージを確認し、メッセージの内容と開発者が作成したルーティング ロジックに基づいて、送信先エンドポイントにメッセージをルーティングします。 コンテンツ ベースのルーティングは、サービス集計、サービスのバージョン管理、および優先度ルーティングの基礎になります。  
  
 コンテンツ ベースのルーティングを実装するために、ルーティング サービスは <xref:System.ServiceModel.Dispatcher.MessageFilter> 実装に依存しています。これらの実装は、ルーティングするメッセージ内の特定の値を照合するために使用されます。 場合、 **MessageFilter**に関連付けられている送信先エンドポイントにルーティングされるメッセージ、メッセージと一致する、 **MessageFilter**です。  メッセージ フィルターはフィルター テーブル (<xref:System.ServiceModel.Routing.Configuration.FilterTableCollection>) にグループ化されて、複雑なルーティング ロジックを構築します。 たとえば、フィルター テーブルに 5 つの相互に排他的なメッセージ フィルターが含まれ、それによって、5 つの送信先エンドポイントのうちの 1 つだけにメッセージがルーティングされる場合があります。  
  
 ルーティング サービスを使用すると、コンテンツ ベースのルーティングの実行に使用するロジックを構成できるほか、ルーティング ロジックを実行時に動的に更新できます。  
  
 メッセージ フィルターをフィルター テーブルにグループ化することで、ルーティング ロジックを構築し、次のような複数のルーティング シナリオを処理できます。  
  
-   サービスの集計  
  
-   サービスのバージョン管理  
  
-   優先度ルーティング  
  
-   動的構成  
  
 メッセージ フィルターとフィルター テーブルの詳細については、次を参照してください。[ルーティングの概要](../../../../docs/framework/wcf/feature-details/routing-introduction.md)と[メッセージ フィルター](../../../../docs/framework/wcf/feature-details/message-filters.md)です。  
  
### <a name="service-aggregation"></a>サービスの集計  
 コンテンツ ベースのルーティングを使用することで、外部のクライアント アプリケーションからメッセージを受信する 1 つのエンドポイントを公開し、メッセージ内の値に基づいて、各メッセージを適切な内部エンドポイントにルーティングできます。 これは、さまざまなバックエンド アプリケーションに対して単一のエンドポイントを提供する場合だけでなく、アプリケーションをさまざまなサービスにファクタリングしているときに単一のアプリケーション エンドポイントを顧客に提供する場合にも便利です。  
  
### <a name="service-versioning"></a>サービスのバージョン管理  
 ソリューションを新しいバージョンに移行するときに、既存の顧客に対応するために、古いバージョンを同時に維持する必要がある場合があります。 このような場合の多くでは、新しいバージョンに接続するクライアントが、ソリューションとの通信時に別のアドレスを使用することが必要になります。 ルーティング サービスを使用すると、メッセージに含まれるバージョン固有の情報に基づいて、適切なソリューションにメッセージをルーティングすることで、ソリューションの両方のバージョンに対応する単一のサービス エンドポイントを公開できます。 このような実装の例については、次を参照してください。[操作方法: サービスのバージョン管理](../../../../docs/framework/wcf/feature-details/how-to-service-versioning.md)です。  
  
### <a name="priority-routing"></a>優先度ルーティング  
 サービスを複数のクライアントに提供するときに、パートナーとサービス レベル アグリーメント (SLA) を結び、それらのパートナーのデータをすべて、その他のクライアントのデータとは別に処理するように規定している場合があります。 メッセージに含まれる顧客固有の情報を検索するフィルターを使用すると、特定のパートナーから送られたメッセージを、各パートナーの SLA 要件に合わせて作成されたエンドポイントに容易にルーティングできます。  
  
## <a name="dynamic-configuration"></a>動的構成  
 サービスを中断させずにメッセージを処理する必要があるミッション クリティカルなシステムをサポートするには、システム内のコンポーネントの構成を実行時に変更できることが非常に重要です。 このニーズを満たすために、ルーティング サービスでは <xref:System.ServiceModel.IExtension%601> 実装が提供されています。これは、実行時にルーティング サービス構成を動的に更新できるようにする <xref:System.ServiceModel.Routing.RoutingExtension> です。  
  
 ルーティング サービスの動的な構成の詳細については、次を参照してください。[ルーティングの概要](../../../../docs/framework/wcf/feature-details/routing-introduction.md)です。  
  
## <a name="protocol-bridging"></a>プロトコル ブリッジ  
 中継局シナリオの課題の 1 つは、内部エンドポイントとメッセージの送信先エンドポイントのトランスポートまたは SOAP バージョンの要件が異なる場合があることです。 このシナリオをサポートするために、ルーティング サービスでは、SOAP メッセージを送信先エンドポイントが必要とする <xref:System.ServiceModel.Channels.MessageVersion> に合わせて処理するなど、プロトコル間をブリッジできます。 これを利用して、内部の通信と外部の通信に別々のプロトコルを使用することができます。  
  
 異なるトランスポートを持つエンドポイント間でのメッセージのルーティングをサポートするために、ルーティング サービスでは、サービスが複数の異なるプロトコルをブリッジできるようにする、システム指定のバインディングを使用します。 この処理は、ルーティング サービスが公開するサービス エンドポイントで、メッセージのルーティング先のクライアント エンドポイントとは異なるプロトコルが使用されると、自動的に実行されます。  
  
## <a name="soap-processing"></a>SOAP 処理  
 一般的なルーティング要件は、異なる SOAP 要件を持つエンドポイント間でメッセージをルーティングできることです。 この要件をサポートするために、ルーティング サービスが、<xref:System.ServiceModel.Routing.SoapProcessingBehavior>を自動的に作成、新しい**MessageVersion**メッセージがルーティングされる前に、送信先エンドポイントの要件を満たしています。 この動作も新たに作成**MessageVersion**ことを確認する、要求元のクライアント アプリケーションに戻る前に応答メッセージに対して、 **MessageVersion**応答の一致しています。元の要求。  
  
 SOAP 処理の詳細については、次を参照してください。[ルーティングの概要](../../../../docs/framework/wcf/feature-details/routing-introduction.md)です。  
  
## <a name="error-handling"></a>エラー処理  
 システムを構成する分散サービスがネットワーク通信に依存する場合は、システム内の通信が、一時的なネットワーク障害に対応可能である必要があります。  ルーティング サービスはエラー処理を実装しており、これによって、サービスの停止を招く可能性がある多くの通信障害を処理できます。  
  
 ルーティング サービスがメッセージを送信している間に <xref:System.ServiceModel.CommunicationException> が発生した場合は、エラー処理が実行されます。  これらの例外は、一般的に、<xref:System.ServiceModel.EndpointNotFoundException>、<xref:System.ServiceModel.ServerTooBusyException>、<xref:System.ServiceModel.CommunicationObjectFaultedException> など、定義されているクライアント エンドポイントとの通信を試みている間に問題が発生したことを示します。  エラー処理コードでキャッチして再送信しようとしています。 はまた、 **TimeoutException**発生すると、から派生していない別の一般的な例外は**CommunicationException**です。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]エラー処理を参照してください[ルーティングの概要](../../../../docs/framework/wcf/feature-details/routing-introduction.md)です。  
  
## <a name="backup-endpoints"></a>バックアップ エンドポイント  
 フィルター テーブル内の各フィルター定義と関連付けられる送信先クライアント エンドポイントに加えて、転送エラーが発生した場合にメッセージをルーティングする、バックアップ エンドポイントのリストも作成できます。 エラーが発生した場合に、フィルター エントリのバックアップ リストが定義されていると、ルーティング サービスにより、そのリストに定義されている最初のエンドポイントにメッセージが送信されます。 この送信に失敗した場合は、送信に成功する、送信失敗に関連しないエラーが返される、またはバックアップ リスト内のすべてのエンドポイントで送信エラーが返されるまで、次のエンドポイントへの送信が試みられます。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]エンドポイントのバックアップ、参照[ルーティングの概要](../../../../docs/framework/wcf/feature-details/routing-introduction.md)と[メッセージ フィルター](../../../../docs/framework/wcf/feature-details/message-filters.md)です。  
  
## <a name="streaming"></a>ストリーム  
 バインディングがストリーミングをサポートするように設定すると、ルーティング サービスはメッセージを正常にストリーミングできます。  ただし、メッセージのバッファーが必要となる可能性のある条件がいくつかあります。  
  
-   マルチキャスト (追加のメッセージ コピーを作成するためのバッファー)  
  
-   フェールオーバー (メッセージがバックアップに送信される必要がある場合のバッファー)  
  
-   System.ServiceModel.Routing.RoutingConfiguration.RouteOnHeadersOnly は false です (フィルターが本文を検査できるように MessageBuffer と共に MessageFilterTable を示すバッファー)  
  
-   動的構成  
  
## <a name="see-also"></a>関連項目  
 [ルーティングの概要](../../../../docs/framework/wcf/feature-details/routing-introduction.md)  
 [ルーティング コントラクト](../../../../docs/framework/wcf/feature-details/routing-contracts.md)  
 [メッセージ フィルター](../../../../docs/framework/wcf/feature-details/message-filters.md)
