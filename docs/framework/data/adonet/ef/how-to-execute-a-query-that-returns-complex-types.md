---
title: "複合型を返すクエリの実行方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: c2209fdb-70ef-4dea-8bb8-097fe96f5563
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a499c8cf9caeac480e09d7c965032db2d9fefec4
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-execute-a-query-that-returns-complex-types"></a>複合型を返すクエリの実行方法
このトピックでは、複合型プロパティを含むエンティティ型オブジェクトを返す [!INCLUDE[esql](../../../../../includes/esql-md.md)] クエリを実行する方法について説明します。  
  
### <a name="to-run-the-code-in-this-example"></a>この例のコードを実行するには  
  
1.  追加、 [AdventureWorks Sales Model](http://msdn.microsoft.com/en-us/f16cd988-673f-4376-b034-129ca93c7832)をプロジェクトに使用してプロジェクトを構成して、[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]です。 詳細については、次を参照してください。[する方法: Entity Data Model ウィザードを使用して](http://msdn.microsoft.com/en-us/dadb058a-c5d9-4c5c-8b01-28044112231d)です。  
  
2.  アプリケーションのコード ページで、次の `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3.  モデルを表示する .edmx ファイルをダブルクリックして、[モデル ブラウザー ウィンドウ](http://msdn.microsoft.com/en-us/94e836e8-a5ea-47ff-aa3e-599d8a02ebfd)エンティティ デザイナーのです。 エンティティ デザイナー画面で、選択、`Email`と`Phone`のプロパティ、`Contact`エンティティ型、し、右クリックして選択**新しい複合型にリファクター**です。  
  
4.  選択した場合は、新しい複合型`Email`と`Phone`にプロパティを追加、**モデル ブラウザー**です。 複合型で、既定の名前が指定されていること: 型の名前を変更`EmailPhone`で、**プロパティ**ウィンドウです。 また、新しい `ComplexProperty` プロパティが `Contact` エンティティ型に追加されます。 プロパティの名前を `EmailPhoneComplexType.` に変更します。  
  
     作成して、Entity Data Model ウィザードを使用した複合型の変更については、次を参照してください[する方法: 複合型プロパティへの既存のプロパティをリファクター](http://msdn.microsoft.com/en-us/5b2eb3b3-693d-42cb-b43a-405812d677eb)と[する方法: 作成との複合型の変更](http://msdn.microsoft.com/en-us/afb8e206-0ffe-4597-b6d4-6ab566897e1d).  
  
## <a name="example"></a>例  
 次の例のコレクションを返すクエリを実行する`Contact`オブジェクトし、の 2 つのプロパティを表示、`Contact`オブジェクト:`ContactID`との値、`EmailPhoneComplexType`複合型。  
  
 [!code-csharp[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#complextypewithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#complextypewithentitycommand)]
