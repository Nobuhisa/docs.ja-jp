---
title: "データ サービスの更新 (WCF Data Services)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework-oob
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, changing data
- WCF Data Services, client library
ms.assetid: 00d993be-ffed-4dea-baf7-6eea982cdb54
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: d51508abf27038e27b4a9d356c726bc8e15cb321
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="updating-the-data-service-wcf-data-services"></a>データ サービスの更新 (WCF Data Services)
使用する場合、[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]クライアント ライブラリを使用する[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]ライブラリ フィード、クライアント データ サービス クラスのインスタンスにフィードのエントリを変換します。 これらのデータ サービス クラスは、<xref:System.Data.Services.Client.DataServiceContext> が属する <xref:System.Data.Services.Client.DataServiceQuery%601> を使用して追跡されます。 クライアントでは、<xref:System.Data.Services.Client.DataServiceContext> にメソッドを使用して報告する、エンティティへの変更が追跡されます。 これらのメソッドを使用すると、クライアントは、追加および削除されたエンティティの追跡に加えて、プロパティ値に対して行われた変更やエンティティ インスタンス間のリレーションシップに対して行われた変更を追跡できます。 追跡されたこれらの変更は、<xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> メソッドが呼び出されたときに、REST ベースの操作としてデータ サービスに送り返されます。  
  
> [!NOTE]
>  <xref:System.Data.Services.Client.DataServiceCollection%601> のインスタンスを使用してデータをコントロールにバインドする場合、バインドされたコントロールのデータに対して行われた変更は <xref:System.Data.Services.Client.DataServiceContext> に自動的に報告されます。 詳細については、次を参照してください。[コントロールへのデータ バインディング](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)です。  
  
## <a name="adding-modifying-and-changing-entities"></a>エンティティの追加および変更  
 使用すると、**サービス参照の追加**への参照を追加する Visual Studio でのダイアログ、[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]フィード、結果として得られるクライアント データ サービス クラスそれぞれがある静的な*作成*を受け取るいずれかのメソッドnull 非許容のエンティティの各プロパティのパラメーターです。 このメソッドを使用すると、次の例に示すように、エンティティ型クラスのインスタンスを作成できます。  
  
 [!code-csharp[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#createnewproduct)]
 [!code-vb[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#createnewproduct)]  
  
 エンティティ インスタンスを追加するには、適切な呼び出し*AddTo*メソッドを<xref:System.Data.Services.Client.DataServiceContext>によって生成されたクラス、**サービス参照の追加**ダイアログ ボックスで、次の例に示すようにします。  
  
 [!code-csharp[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addproductspecific)]
 [!code-vb[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addproductspecific)]  
  
 オブジェクトがコンテキストおよび正しいエンティティ セットに追加されます。 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> を呼び出すこともできますが、エンティティ セット名を指定する必要があります。 追加したエンティティにその他のエンティティへの 1 つ以上のリレーションシップがある場合は、<xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> メソッドを使用するか、前のメソッドの 1 つを使用してこれらのリンクを明示的に定義することができます。 これらの操作の詳細については、このトピックの後半で説明します。  
  
 既存のエンティティ インスタンスを変更するには、まずそのエンティティを照会し、このエンティティのプロパティに必要な変更を加えてから、オブジェクトの更新を送信する必要があることをクライアント ライブラリに示すために、次のように <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> で <xref:System.Data.Services.Client.DataServiceContext> メソッドを呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#modifycustomerspecific)]
 [!code-vb[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#modifycustomerspecific)]  
  
 エンティティ インスタンスを削除するには、次の例に示すように、<xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> で <xref:System.Data.Services.Client.DataServiceContext> メソッドを呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#deleteproductspecific)]
 [!code-vb[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#deleteproductspecific)]  
  
 詳細については、次を参照してください。[する方法: エンティティを追加、変更、および削除](../../../../docs/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services.md)です。  
  
## <a name="attaching-entities"></a>エンティティのアタッチ  
 クライアント ライブラリでは、クエリを実行してエンティティを <xref:System.Data.Services.Client.DataServiceContext> に読み込むことなく、エンティティに対して行った変更を保存できます。 <xref:System.Data.Services.Client.DataServiceContext.AttachTo%2A> メソッドを使用して、既存のオブジェクトを <xref:System.Data.Services.Client.DataServiceContext> の特定のエンティティ セットにアタッチします。 その後、オブジェクトを変更して、変更内容をデータ サービスに保存できます。 次の例では、変更された顧客オブジェクトがコンテキストにアタッチされた後、<xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> が呼び出される前に、<xref:System.Data.Services.Client.EntityStates.Modified> が呼び出され、アタッチされたオブジェクトが <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> としてマークされます。  
  
 [!code-csharp[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#attachobjectspecific)]
 [!code-vb[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#attachobjectspecific)]  
  
 オブジェクトをアタッチする際は、次の点に注意してください。  
  
-   オブジェクトは、<xref:System.Data.Services.Client.EntityStates.Unchanged> 状態でアタッチされます。  
  
-   オブジェクトがアタッチされるとき、アタッチされるオブジェクトに関連付けられたオブジェクトはアタッチされません。  
  
-   エンティティがコンテキストによって既に追跡されている場合は、オブジェクトをアタッチできません。  
  
-   eTag 値と一緒に受け取ったエンティティ オブジェクトをアタッチした場合は、<xref:System.Data.Services.Client.DataServiceContext.AttachTo%28System.String%2CSystem.Object%2CSystem.String%29> メソッドの、`etag` パラメーターを受け取るオーバーロードが使用されます。 この eTag 値は、アタッチされたオブジェクトへの変更を保存したときに、同時実行をチェックするために使用されます。  
  
 詳細については、次を参照してください。[する方法: 既存のエンティティを DataServiceContext にアタッチ](../../../../docs/framework/data/wcf/attach-an-existing-entity-to-dc-wcf-data.md)です。  
  
## <a name="creating-and-modifying-relationship-links"></a>リレーションシップ リンクの作成および変更  
 いずれかを使用して、新しいエンティティを追加すると、<xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>メソッドまたは適切な*AddTo*のメソッド、<xref:System.Data.Services.Client.DataServiceContext>するクラス、**サービス参照の追加**ダイアログが生成されると、すべてのリレーションシップ新しいエンティティと関連するエンティティの間は自動的に定義されていません。  
  
 エンティティ インスタンス間のリレーションシップを作成および変更し、クライアント ライブラリを使用して、これらの変更をデータ サービスに反映できます。 エンティティ間のリレーションシップは、モデル内の関連付けとして定義されています。また、<xref:System.Data.Services.Client.DataServiceContext> は、各リレーションシップをコンテキスト内のリンク オブジェクトとして追跡します。 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]次のメソッドを提供、<xref:System.Data.Services.Client.DataServiceContext>クラスを作成、変更、およびこれらのリンクを削除します。  
  
|メソッド|説明|  
|------------|-----------------|  
|<xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A>|関連付けられた 2 つのエンティティ オブジェクトの間に新しいリンクを作成します。 このメソッドを呼び出すことは、<xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> と <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> を呼び出して、新しいオブジェクトを作成すること、および既存のオブジェクトへのリレーションシップを定義することと同じです。|  
|<xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>|関連付けられた 2 つのエンティティ オブジェクトの間に新しいリンクを作成します。|  
|<xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>|関連付けられた 2 つのエンティティ オブジェクト間の既存のリンクを更新します。 また、<xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> は、0 または 1 対 1 (`0..1:1`) および 1 対 1 (`1:1`) の基数を持つリンクの削除にも使用します。 これを行うには、関連付けられたオブジェクトを `null` に設定します。|  
|<xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A>|<xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> メソッドが呼び出されたときに、コンテキストが追跡するリンクに削除のマークを付けます。 このメソッドは、関連付けられたオブジェクトを削除する場合、または既存のオブジェクトへのリンクを削除した後に関連付けられた新しいオブジェクトへのリンクを追加してリレーションシップを変更する場合に使用します。|  
|<xref:System.Data.Services.Client.DataServiceContext.AttachLink%2A>|2 つのエンティティ オブジェクトの間の既存のリンクのコンテキストを通知します。 コンテキストでは、このリレーションシップがデータ サービス内に既に存在するものと見なされるので、<xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> メソッドを呼び出してもリンクは作成されません。 このメソッドは、2 つのオブジェクトをコンテキストにアタッチして、オブジェクト間のリンクもアタッチする必要がある場合に使用します。 新しいリレーションシップを定義する場合は、<xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> を使用してください。|  
|<xref:System.Data.Services.Client.DataServiceContext.DetachLink%2A>|コンテキストでの指定リンクの追跡を停止します。 このメソッドは、一対多 (`*:*`) のリレーションシップの削除に使用します。 基数が 1 のリレーションシップ リンクの場合は、<xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> を代わりに使用する必要があります。|  
  
 次の例は、<xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> メソッドを使用して、既存の `Order_Detail` エンティティに関連付けられた新しい `Orders` を追加する方法を示します。 新しい `Order_Details` オブジェクトは <xref:System.Data.Services.Client.DataServiceContext> によって追跡されるので、既存の `Order_Details` エンティティと追加された `Products` オブジェクトのリレーションシップは、<xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> メソッドを呼び出すことによって定義されます。  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addorderdetailtoorderspecific)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addorderdetailtoorderspecific)]  
  
 <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> メソッドは、データ サービス内に作成する必要のあるリンクを定義しますが、これらのリンクをコンテキスト内のオブジェクトに反映させるには、オブジェクト自身でナビゲーション プロパティを設定する必要があります。 前の例では、次のようにナビゲーション プロパティを設定します。  
  
 [!code-csharp[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#setnavprops)]
 [!code-vb[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#setnavprops)]  
  
 詳細については、次を参照してください。[する方法: エンティティ リレーションシップの定義](../../../../docs/framework/data/wcf/how-to-define-entity-relationships-wcf-data-services.md)です。  
  
## <a name="saving-changes"></a>変更の保存  
 変更は、<xref:System.Data.Services.Client.DataServiceContext> インスタンスで追跡されますが、サーバーには直ちに送信されません。 指定されたアクティビティに対して必要な変更が完了した後、<xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> を呼び出して、すべての変更をデータ サービスに送信します。 詳細については、次を参照してください。[データ サービス コンテキストを管理する](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)です。 変更は、<xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A> および <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A> メソッドを使用して、非同期で保存することもできます。 詳細については、次を参照してください。[非同期操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)です。  
  
## <a name="see-also"></a>関連項目  
 [WCF Data Services クライアント ライブラリ](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)  
 [データ サービスに対するクエリ](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)  
 [非同期操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)  
 [操作のバッチ処理](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)  
 [オブジェクトの具体化](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)  
 [データ サービス コンテキストを管理します。](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)
