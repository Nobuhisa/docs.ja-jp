---
title: "ADO.NET での大きい値 (max) データの変更"
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
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3a80f316ffc3380408802fefe1a26d71e5e76ac0
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="modifying-large-value-max-data-in-adonet"></a>ADO.NET での大きい値 (max) データの変更
ラージ オブジェクト (LOB) データ型は、最大行サイズが 8 KB を超えるデータ型です。 SQL Server では、`max`、`varchar`、および `nvarchar` の各データ型に `varbinary` 指定子が用意されており、2^32 バイトの値を格納できます。 テーブル列および Transact-SQL 変数により、`varchar(max)`、`nvarchar(max)`、または `varbinary(max)` データ型を指定できます。 ADO.NET では、`max` データ型は、`DataReader` によってフェッチすることができ、特殊な処理を行うことなく入力パラメーターと出力パラメーター両方の値として指定することもできます。 サイズの大きい `varchar` データ型の場合は、データを段階的に取得および更新できます。  
  
 `max` データ型は、Transact-SQL 変数として比較に使用したり、連結に使用したりできます。 これらは SELECT ステートメントの DISTINCT 句、ORDER BY 句、GROUP BY 句で使用できるほか、集約、結合、サブクエリでも使用できます。  
  
 次の表は、SQL Server オンライン ブックのドキュメントへのリンクを提供します。  
  
 **SQL Server オンライン ブック**  
  
1.  [大きな値データ型の使用](http://go.microsoft.com/fwlink/?LinkId=120498)  
  
## <a name="large-value-type-restrictions"></a>大きい値型の制限事項  
 `max` データ型には、小さいデータ型にはない、次の制限事項が適用されます。  
  
-   `sql_variant` に大きい `varchar` データ型を含めることはできません。  
  
-   大きい `varchar` 列はインデックス内のキー列として指定することはできません。 非クラスター化インデックスに含まれる列で使用できます。  
  
-   大きい `varchar` 列はパーティション分割のキー列として使用できません。  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Transact-SQL での大きい値型の使用  
 Transact-SQL の `OPENROWSET` 関数は、リモート データへの接続およびアクセスに 1 回だけ使用できます。 この関数には、OLE DB データ ソースからリモート データにアクセスするために必要な、すべての接続情報が含まれています。 `OPENROWSET` は、クエリの FROM 句でテーブル名と同様に参照できます。 OLE DB プロバイダーの機能に従って、INSERT、UPDATE、または DELETE ステートメントのターゲット テーブルとして参照することもできます。  
  
 `OPENROWSET` 関数には、`BULK` 行セット プロバイダーが含まれており、データをターゲット テーブルに読み込むことなく、ファイルから直接読み取ることができます。 これにより、`OPENROWSET` を単純な INSERT SELECT ステートメントで使用できます。  
  
 `OPENROWSET``BULK`オプション引数により、開始およびデータの読み取りを終了する場所、エラーに対処する方法、およびデータを解釈する方法に大幅な制御。 たとえば、データ ファイルを 1 行として、あるいは `varbinary`、`varchar`、または `nvarchar` 型の 1 列の行セットとして読み取るように指定できます。 完全な構文とオプションについては、SQL Server オンライン ブックを参照してください。  
  
 次の例では、AdventureWorks サンプル データベースの ProductPhoto テーブルに写真を挿入しています。 使用する場合、`BULK``OPENROWSET`プロバイダー、すべての列に値を挿入しない場合でも、列の名前付きの一覧を指定する必要があります。 この場合の主キーは ID 列として定義され、列リストから省略することもできます。 ただし、`OPENROWSET` ステートメントの最後に相関関係名 (この場合は ThumbnailPhoto) を指定する必要があります。 これにより、ファイルが読み込まれる `ProductPhoto` テーブルの列との相関関係が定義されます。  
  
```  
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>UPDATE .WRITE を使用したデータの更新  
 Transact-SQL の UPDATE ステートメントでは、`varchar(max)`、`nvarchar(max)`、または `varbinary(max)` 列の内容を変更するための、新しい WRITE 構文を使用できます。 これにより、データの部分的な更新が可能になります。 次に UPDATE .WRITE 構文を省略形で示します。  
  
 UPDATE  
  
 { *\<オブジェクト >* }  
  
 SET  
  
 { *column_name* = {です。書き込み (*式*、 @Offset 、 @Length )}  
  
 WRITE メソッドには、ことを指定の値のセクションで、 *column_name*が変更されます。 式が値をコピーする、 *column_name*、`@Offset`に式が書き込まれたが、開始点は、および`@Length`引数は、列のセクションの長さ。  
  
|If|Then|  
|--------|----------|  
|expression が NULL|`@Length`無視されますとで値*column_name*は切り捨てられます内の指定した`@Offset`です。|  
|`@Offset` が NULL|更新操作では、既存の最後に式を追加します。 *column_name*値および`@Length`は無視されます。|  
|`@Offset` が column_name の値の長さより長い|SQL Server からエラーが返されます。|  
|`@Length` が NULL|更新操作により `@Offset` の値の `column_name` から最後までのすべてのデータが削除されます。|  
  
> [!NOTE]
>  `@Offset` または `@Length` のいずれにも負数を指定することはできません。  
  
## <a name="example"></a>例  
 この Transact-SQL の例では、AdventureWorks データベースの Document テーブルの `nvarchar(max)` 列である DocumentSummary の値の一部が更新されます。 置換後の単語、置換する単語の既存データ内での開始位置 (オフセット)、置換する文字数 (長さ) を指定することで、'components' という単語が 'features' という単語に置換されます。 この例では、結果を比較するために、UPDATE ステートメントの前後に SELECT ステートメントを指定しています。  
  
```  
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>ADO.NET での大きい値型の使用  
 ADO.NET での大きな値の型を使用するには、大きな値の型として指定することによって<xref:System.Data.SqlClient.SqlParameter>内のオブジェクト、<xref:System.Data.SqlClient.SqlDataReader>の結果を返すセット、またはを使用して、<xref:System.Data.SqlClient.SqlDataAdapter>を埋める、 `DataSet` /`DataTable`です。 大きい値型と、関連する小さい値型の使用方法に違いはありません。  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>GetSqlBytes を使用したデータの取得  
 `GetSqlBytes` の <xref:System.Data.SqlClient.SqlDataReader> メソッドを使用して、`varbinary(max)` 列の内容を取得できます。 次のコード フラグメントでは、<xref:System.Data.SqlClient.SqlCommand> という名前の `cmd` オブジェクトによってテーブルから `varbinary(max)` データが選択され、<xref:System.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトによってデータが <xref:System.Data.SqlTypes.SqlBytes> として取得されることを想定しています。  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim bytes As SqlBytes = reader.GetSqlBytes(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>GetSqlChars を使用したデータの取得  
 `GetSqlChars` の <xref:System.Data.SqlClient.SqlDataReader> メソッドを使用して、`varchar(max)` または `nvarchar(max)` 列の内容を取得できます。 次のコード フラグメントでは、<xref:System.Data.SqlClient.SqlCommand> という名前の `cmd` オブジェクトによってテーブルから `nvarchar(max)` データが選択され、<xref:System.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトによってデータが取得されることを想定しています。  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim buffer As SqlChars = reader.GetSqlChars(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>GetSqlBinary を使用したデータの取得  
 `GetSqlBinary` の <xref:System.Data.SqlClient.SqlDataReader> メソッドを使用して、`varbinary(max)` 列の内容を取得できます。 次のコード フラグメントでは、<xref:System.Data.SqlClient.SqlCommand> という名前の `cmd` オブジェクトによってテーブルから `varbinary(max)` データが選択され、<xref:System.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトによってデータが <xref:System.Data.SqlTypes.SqlBinary> ストリームとして取得されることを想定しています。  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim binaryStream As SqlBinary = reader.GetSqlBinary(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>GetBytes を使用したデータの取得  
 `GetBytes` の <xref:System.Data.SqlClient.SqlDataReader> メソッドにより、指定された配列のオフセットから開始するバイト配列に、指定された列のオフセットからバイトのストリームが読み込まれます。 次のコード フラグメントでは、<xref:System.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトによってバイトがバイト配列に読み込まれることが想定されています。 ただし `GetSqlBytes` とは異なり、`GetBytes` では配列バッファーのサイズを指定する必要があります。  
  
```vb  
While reader.Read()  
    Dim buffer(4000) As Byte  
    Dim byteCount As Integer = _  
    CInt(reader.GetBytes(1, 0, buffer, 0, 4000))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>GetValue を使用したデータの取得  
 `GetValue` の <xref:System.Data.SqlClient.SqlDataReader> メソッドにより、指定した列オフセットから値が配列に読み込まれます。 次のコード フラグメントでは、<xref:System.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトによって、最初の列のオフセットからバイナリ データが取得され、2 番目の列のオフセットから文字列データが取得されることが想定されています。  
  
```vb  
While reader.Read()  
    ' Read the data from varbinary(max) column  
    Dim binaryData() As Byte = CByte(reader.GetValue(0))  
  
    ' Read the data from varchar(max) or nvarchar(max) column  
    Dim stringData() As String = Cstr((reader.GetValue(1))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>大きい値型から CLR 型への変換  
 `varchar(max)` などの任意の文字列変換メソッドを使用して、`nvarchar(max)` または `ToString` 列の内容を変換できます。 次のコード フラグメントでは、<xref:System.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトによってデータが取得されることが想定されています。  
  
```vb  
While reader.Read()  
    Dim str as String = reader(0).ToString()  
    Console.WriteLine(str)  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>例  
 次のコードでは、`LargePhoto` データベースの `ProductPhoto` テーブルから名前と `AdventureWorks` オブジェクトが取得され、ファイルに保存されます。 このアセンブリは、<xref:System.Drawing> 名前空間への参照を指定してコンパイルする必要があります。  <xref:System.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> の <xref:System.Data.SqlClient.SqlDataReader> メソッドにより、<xref:System.Data.SqlTypes.SqlBytes> プロパティを公開する `Stream` オブジェクトが返されます。 コードでは、これを使用して、新しい`Bitmap`オブジェクト、および、Gif を保存し、`ImageFormat`です。  
  
 [!code-csharp[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/VB/source.vb#1)]  
  
## <a name="using-large-value-type-parameters"></a>大きな値型パラメーターの使用  
 大きい値型は、<xref:System.Data.SqlClient.SqlParameter> オブジェクト内の小さい値型と同じ方法で、<xref:System.Data.SqlClient.SqlParameter> オブジェクト内で使用できます。 として大きな値の型を取得する<xref:System.Data.SqlClient.SqlParameter>値は、次の例で示すようにします。 このコードでは、次の GetDocumentSummary ストアド プロシージャが、AdventureWorks サンプル データベースに存在することが想定されています。 ストアド プロシージャでは、という名前の入力パラメーター@DocumentIDである DocumentSummary 列の内容を返します、@DocumentSummary出力パラメーターです。  
  
```  
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>例  
 ADO.NET コードにより、<xref:System.Data.SqlClient.SqlConnection> および <xref:System.Data.SqlClient.SqlCommand> オブジェクトが作成され、GetDocumentSummary ストアド プロシージャが実行されることで、ドキュメントの概要が取得され、大きい値型として格納されます。 コード値を渡す、@DocumentID入力パラメーター、およびに渡された結果が表示されます、@DocumentSummaryコンソール ウィンドウでパラメーターを出力します。  
  
 [!code-csharp[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目  
 [SQL Server のバイナリ データと大きな値のデータ](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)  
 [SQL Server データ型のマッピング](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)  
 [ADO.NET における SQL Server データ操作](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)  
 [ADO.NET のマネージ プロバイダーと DataSet デベロッパー センター](http://go.microsoft.com/fwlink/?LinkId=217917)
