---
title: "SQL Server データ型と ADO.NET"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 16c675491a378d72d82a252d79a73379f494893c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server データ型と ADO.NET
SQL Server と .NET Framework は異なる型システムに基づいているので、両者間でデータ損失が発生する可能性があります。 データの整合性を維持するために、.NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient>) では、SQL Server データを処理するための型指定されたアクセサー メソッドが提供されています。 <xref:System.Data.SqlDbType> クラスの列挙値を使用して、<xref:System.Data.SqlClient.SqlParameter> データ型を指定できます。  
  
 詳細については、データを記述する型を SQL Server と .NET Framework データ型間のマッピング テーブルを参照してください[SQL Server データ型マッピング](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)です。  
  
 SQL Server 2008 では、業務上のニーズに対応して、日時データ、構造化データ、半構造化データ、および非構造化データを扱うための新しいデータ型が導入されました。 新しいデータ型は、SQL Server 2008 オンライン ブックで説明されています。  
  
 アプリケーションで使用可能な SQL Server のデータ型は、使用する SQL Server のバージョンによって異なります。 詳細については、次の表にある各バージョンの SQL Server オンライン ブックを参照してください。  
  
 **SQL Server オンライン ブック**  
  
1.  [データ型 (データベース エンジン)](http://go.microsoft.com/fwlink/?LinkID=107468)  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SqlTypes と DataSet](../../../../../docs/framework/data/adonet/sql/sqltypes-and-the-dataset.md)  
 `SqlTypes` 内の `DataSet` に対する型のサポートについて説明します。  
  
 [Null 値の処理](../../../../../docs/framework/data/adonet/sql/handling-null-values.md)  
 null 値と 3 値ロジックの使用例を示します。  
  
 [比較する GUID と uniqueidentifier 値](../../../../../docs/framework/data/adonet/sql/comparing-guid-and-uniqueidentifier-values.md)  
 SQL Server と .NET Framework での GUID および uniqueidentifier 値の使用例を示します。  
  
 [日付と時刻のデータ](../../../../../docs/framework/data/adonet/sql/date-and-time-data.md)  
 SQL Server 2008 で導入された新しい日付と時刻のデータ型の使用方法について説明します。  
  
 [大きな Udt](../../../../../docs/framework/data/adonet/sql/large-udts.md)  
 SQL Server 2008 で導入された大きな値の UDT からデータを取り出す方法の例を示します。  
  
 [SQL Server の XML データ](../../../../../docs/framework/data/adonet/sql/xml-data-in-sql-server.md)  
 SQL Server から取得した XML データを使用する方法について説明します。  
  
## <a name="reference"></a>参照  
 <xref:System.Data.DataSet>  
 `DataSet` クラスおよびそのすべてのメンバーについて説明します。  
  
 <xref:System.Data.SqlTypes>  
 `SqlTypes` 名前空間およびそのすべてのメンバーについて説明します。  
  
 <xref:System.Data.SqlDbType>  
 `SqlDbType` 列挙型およびそのすべてのメンバーについて説明します。  
  
 <xref:System.Data.DbType>  
 `DbType` 列挙型およびそのすべてのメンバーについて説明します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データ型のマッピング](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)  
 [パラメーターとパラメーターのデータ型の構成](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)  
 [テーブル値パラメーター](../../../../../docs/framework/data/adonet/sql/table-valued-parameters.md)  
 [SQL Server のバイナリ データと大きな値のデータ](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)  
 [ADO.NET のマネージ プロバイダーと DataSet デベロッパー センター](http://go.microsoft.com/fwlink/?LinkId=217917)
