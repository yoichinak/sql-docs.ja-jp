---
title: ADO.NET での大きな値 (max) データの変更
description: 大きな値のデータ型を扱う方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f55cb14a95844558e4a759a4acce71509d62d4ba
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725623"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>ADO.NET での大きな値 (max) データの変更

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

ラージ オブジェクト (LOB) データ型は、最大行サイズが 8 KB を超えるデータ型です。 SQL Server からは、`max` データ型、`varchar` データ型、`nvarchar` データ型に `varbinary` 指定子が提供され、2^32 バイトもの大きさの値を格納することができます。 テーブルの列と Transact-SQL 変数では、`varchar(max)`、`nvarchar(max)`、または `varbinary(max)` データ型を指定できます。 .NET では、`max` によって `DataReader` データ型をフェッチでき、特殊な処理を行うことなく入力および出力両方のパラメーター値として指定することもできます。 大きな `varchar` データ型の場合は、データを段階的に取得および更新できます。  
  
Transact-SQL 変数としての比較、および連結に `max` データ型を使用できます。 このデータ型は、SELECT ステートメントの DISTINCT 句、ORDER BY 句、GROUP BY 句のほか、集約、結合、およびサブクエリでも使用できます。

大きな値のデータ型の詳細については、SQL Server オンライン ブックの「[大きな値のデータ型の使用](/previous-versions/sql/sql-server-2008/ms178158(v=sql.100))」を参照してください。
  
## <a name="large-value-type-restrictions"></a>大きい値型の制限事項  
次の制限は、`max` データ型に適用されますが、これは小さいデータ型に対しては存在しません。  
  
- `sql_variant` に大きな `varchar` データ型を含めることはできません。  
  
- 大きな `varchar` 列を、インデックスのキー列として指定することはできません。 この列は、非クラスター化インデックスの付加列で許可されます。  
  
- 大きな `varchar` 列を、パーティション分割キー列として使用することはできません。  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Transact-SQL での大きい値型の使用  
Transact-SQL `OPENROWSET` 関数は、リモート データへの 1 回限りの接続およびアクセス方法です。 `OPENROWSET` は、テーブル名と同じように、クエリの FROM 句で参照できます。 INSERT、UPDATE、または DELETE ステートメントの対象のテーブルとしても参照できます。  
  
`OPENROWSET` 関数には `BULK` 行セット プロバイダーが含まれており、これによりデータをターゲット テーブルに読み込むことなく、ファイルから直接読み取ることができます。 これにより、`OPENROWSET` を単純な INSERT SELECT ステートメントで使用できます。  
  
`OPENROWSET BULK` オプション引数により、データの読み取りの開始位置および終了位置、エラーの処理、データの解釈の制御が大幅に容易になります。 たとえば、データ ファイルを `varbinary`、`varchar`、`nvarchar` 型の単一行、単一列の行セットとして読み取るように指定できます。 完全な構文とオプションについては、SQL Server オンライン ブックを参照してください。  
  
次の例は、写真を、AdventureWorks サンプル データベースの ProductPhoto テーブルに挿入しています。 `BULK OPENROWSET` プロバイダーを使用する場合は、すべての列に値を挿入しない場合でも、列名を挙げてリストを作成する必要があります。 この場合の主キーは ID 列として定義され、列リストから省略できます。 また、`OPENROWSET` ステートメントの末尾で相関関係名を指定する必要があることにも注意してください。この例では ThumbnailPhoto です。 これは、ファイルが読み込まれる先の `ProductPhoto` テーブルの列と関連しています。  
  
```sql
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
Transact-SQL の UPDATE ステートメントには、`varchar(max)` 列、`nvarchar(max)` 列、または `varbinary(max)` 列の内容を変更するための新しい WRITE 構文があります。 これにより、データを部分的に更新できます。 ここでは省略形式で UPDATE .WRITE 構文が示されています。  
  
UPDATE  
  
{ *\<object>* }  
  
SET  
  
{ *column_name* = { .WRITE ( *expression* , @Offset , @Length ) }  
  
WRITE メソッドは、*column_name* の値のセクションが変更されることを指定します。 この式は *column_name* にコピーされる値で、`@Offset` は式が記述される開始位置であり、`@Length` 引数は列のセクションの長さを示します。  
  
|状況|THEN|  
|--------|----------|  
|式が NULL に設定されています|`@Length` は無視され、*column_name* の値は指定された `@Offset` で切り捨てられます。|  
|`@Offset` は NULL です|更新操作によって既存の *column_name* の値の最後に式が追加され、`@Length` が無視されます。|  
|`@Offset` が column_name 値の長さを超えています|SQL Server はエラーを返します。|  
|`@Length` は NULL です|更新操作により、`@Offset` 値の終わりまですべてのデータが `column_name` から削除されます。|  
  
> [!NOTE]
>  `@Offset` も `@Length` も負の数にすることはできません。  
  
## <a name="example"></a>例  
この Transact-SQL の例では、AdventureWorks データベースの Document テーブルの `nvarchar(max)` 列である DocumentSummary の部分値を更新します。 置換する語、既存データ内で置換される語の開始位置 (オフセット)、置換する文字数 (長さ) を指定することにより、"components" という語が、"features" という語で置換されます。 この例では、結果を比較するために、UPDATE ステートメントの前後に SELECT ステートメントを挿入します。  
  
```sql
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
大きい値型を ADO.NET で使用するには、大きい値型を <xref:Microsoft.Data.SqlClient.SqlParameter> で <xref:Microsoft.Data.SqlClient.SqlDataReader> オブジェクトとして指定して結果セットを返すようにするか、<xref:Microsoft.Data.SqlClient.SqlDataAdapter> を使用して `DataSet`/`DataTable` に入力します。 大きな値の型と、それに関連する小さい値のデータ型の操作方法に違いはありません。  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>GetSqlBytes を使用したデータ取得  
`GetSqlBytes` の <xref:Microsoft.Data.SqlClient.SqlDataReader> メソッドを使用して、`varbinary(max)` 列の内容を取得できます。 次のコード フラグメントは、テーブルから <xref:Microsoft.Data.SqlClient.SqlCommand> データを選択する `cmd` という名前の `varbinary(max)` オブジェクトと、データを <xref:Microsoft.Data.SqlClient.SqlDataReader> として取得する `reader` という名前の <xref:System.Data.SqlTypes.SqlBytes> オブジェクトがあることを前提としています。  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>GetSqlChars を使用したデータ取得  
`GetSqlChars` の <xref:Microsoft.Data.SqlClient.SqlDataReader> メソッドを使用して、`varchar(max)` 列または `nvarchar(max)` 列の内容を取得できます。 次のコード フラグメントは、テーブルから <xref:Microsoft.Data.SqlClient.SqlCommand> データを選択する `cmd` という名前の `nvarchar(max)` オブジェクトと、データを取得する <xref:Microsoft.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトがあることを前提としています。   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>GetSqlBinary を使用したデータ取得  
`GetSqlBinary` の <xref:Microsoft.Data.SqlClient.SqlDataReader> メソッドを使用して、`varbinary(max)` 列の内容を取得できます。 次のコード フラグメントは、テーブルから <xref:Microsoft.Data.SqlClient.SqlCommand> データを選択する `cmd` という名前の `varbinary(max)` オブジェクトと、データを <xref:Microsoft.Data.SqlClient.SqlDataReader> ストリームとして取得する `reader` という名前の <xref:System.Data.SqlTypes.SqlBinary> オブジェクトがあることを前提としています。  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>GetBytes を使用したデータ取得  
`GetBytes` の <xref:Microsoft.Data.SqlClient.SqlDataReader> メソッドでは、バイトのストリームを、指定した列オフセットから、指定した配列オフセットから始まるバイト配列に読み取ります。 次のコード フラグメントは、バイト配列に対するバイトを取得する <xref:Microsoft.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトがあることを前提としています。 `GetSqlBytes` とは異なり、`GetBytes` には配列バッファーのサイズを必要とすることに注意してください。  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>GetValue を使用したデータ取得  
`GetValue` の <xref:Microsoft.Data.SqlClient.SqlDataReader> メソッドは、指定した列オフセットから配列に値を読み取ります。 次のコード フラグメントは、最初の列オフセットからバイナリ データを取得した後、2 番目の列オフセットから文字列データを取得する <xref:Microsoft.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトがあることを前提としています。  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>大きな値型から CLR 型への変換  
`varchar(max)` などの任意の文字列変換メソッドを使用して、`nvarchar(max)` 列または `ToString` 列の内容を変換できます。 次のコード フラグメントは、データを取得する <xref:Microsoft.Data.SqlClient.SqlDataReader> という名前の `reader` オブジェクトがあることを前提としています。  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>例  
次のコードでは、`LargePhoto` データベースの `ProductPhoto` テーブルから名前と `AdventureWorks` オブジェクトを取得し、ファイルに保存します。 アセンブリは、<xref:System.Drawing> 名前空間への参照を使用してコンパイルする必要があります。  <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> の <xref:Microsoft.Data.SqlClient.SqlDataReader> メソッドは、<xref:System.Data.SqlTypes.SqlBytes> プロパティを公開する `Stream` オブジェクトを返します。 コードではこのオブジェクトを使用して新しい `Bitmap` オブジェクトが作成され、Gif `ImageFormat` に保存されます。  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>大きな値型のパラメーターの使用  
<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトで大きな値型を使用する方法は、<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトで小さい値型を使用する方法と同じです。 次の例に示すように、大きい値型は <xref:Microsoft.Data.SqlClient.SqlParameter> 値として取得することができます。 このコードは、次の GetDocumentSummary ストアド プロシージャが AdventureWorks サンプル データベースに存在することを前提としています。 ストアド プロシージャでは @DocumentID という名前の入力パラメーターを受け取り、@DocumentSummary 出力パラメーターの DocumentSummary 列の内容を返します。  
  
```sql
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
ADO.NET コードは <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトと <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを作成して GetDocumentSummary ストアド プロシージャを実行し、大きな値型として格納されているドキュメントの概要を取得します。 このコードによって @DocumentID 入力パラメーターの値が渡され、@DocumentSummary 出力パラメーターに戻された結果がコンソール ウィンドウに表示されます。  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>次のステップ
- [SQL Server のバイナリ データと大きな値のデータ](sql-server-binary-large-value-data.md)
- [ADO.NET での SQL Server のデータ操作](sql-server-data-operations.md)