---
title: DataAdapter パラメーター
description: データ ソースからデータを返し、データ ソースへの変更を管理する DbDataAdapter のプロパティについて説明します。
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 90985f155392a78da408ffbda3e1d2c0b12d4648
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771604"
---
# <a name="dataadapter-parameters"></a>DataAdapter パラメーター

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:System.Data.Common.DbDataAdapter> には 4 つのプロパティがあり、データ ソースからデータを取得したりデータ ソースのデータを更新したりするために使用されます。<xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> プロパティは、データ ソースのデータを返します。<xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>、<xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A>、および <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> の各プロパティは、データ ソースの変更を管理するために使用されます。

> [!NOTE]
> `SelectCommand` プロパティは、`Fill` の `DataAdapter` メソッドを呼び出す前に設定しておく必要があります。 `InsertCommand`、`UpdateCommand`、`DeleteCommand` の各プロパティは、`Update` 内のデータに加えられた変更に応じて、`DataAdapter` の <xref:System.Data.DataTable> メソッドを呼び出す前に設定する必要があります。 たとえば、行が追加された場合には、`InsertCommand` を呼び出す前に `Update` を設定する必要があります。 `Update` によって挿入行、更新行、または削除行が処理されるとき、`DataAdapter` でそれぞれの `Command` プロパティが使用され、アクションが処理されます。 変更された行に関する現在の情報が `Command` コレクションを経由して `Parameters` オブジェクトに渡されます。

データ ソースの行を更新するときは、一意識別子を使用してテーブル内の更新する列を識別する UPDATE ステートメントを呼び出します。 一意識別子は、一般には主キー フィールドの値です。 UPDATE ステートメントでは、次の Transact-SQL ステートメントに示すように、一意識別子と更新する列および値の両方を含むパラメーターを使用します。

```sql
UPDATE Customers SET CompanyName = @CompanyName
  WHERE CustomerID = @CustomerID  
```  

> [!NOTE]
> パラメーターのプレースホルダーの構文はデータ ソースに依存します。 次に、SQL Server のデータ ソースのプレースホルダーの例を示します。

この例では、`CustomerID` が `@CustomerID` パラメーターの値と等しい行の `@CompanyName` パラメーターの値で `CompanyName` フィールドが更新されます。 これらのパラメーターでは、<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlParameter.SourceColumn%2A> プロパティを使用して、変更された行から情報が取得されます。 前のサンプル UPDATE ステートメントのパラメーターを次に示します。 このコードは、変数 `adapter` が有効な <xref:Microsoft.Data.SqlClient.SqlDataAdapter> オブジェクトを表すことを前提としています。

[!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter#2](~/../sqlclient/doc/samples/SqlDataAdapter_SqlDataAdapter.cs#2)]

`Parameters` コレクションの `Add` メソッドは、パラメーター名、データ型、サイズ (その型に適用可能な場合)、および <xref:System.Data.Common.DbParameter.SourceColumn%2A> の名前を `DataTable` から受け取ります。 <xref:System.Data.Common.DbParameter.SourceVersion%2A> パラメーターの `@CustomerID` が `Original` に設定されることに注意してください。 この設定により、変更された <xref:System.Data.DataRow> で 1 つまたは複数の識別列の値が変更されている場合に、データ ソース内の既存の行が確実に更新されます。 識別列の値が変更されている場合、`Original` 行の値がデータ ソースの現在の値と一致し、`Current` 行の値に更新済みの値が格納されます。 `SourceVersion` パラメーターの `@CompanyName` は設定されていないため、既定値である `Current` の行の値が使用されます。

> [!NOTE]
> `DataAdapter` の `Fill` 操作と `DataReader` の `Get` メソッドのどちらの場合も、.NET 型は Microsoft SqlClient Data Provider for SQL Server から返された型から推論されます。 Microsoft SQL Server データ型の推論された .NET 型およびアクセサー メソッドについては、「[ADO.NET のデータ型のマッピング](data-type-mappings-ado-net.md)」を参照してください。

## <a name="parametersourcecolumn-parametersourceversion"></a>Parameter.SourceColumn、Parameter.SourceVersion

`SourceColumn` および `SourceVersion` が、引数として `Parameter` コンストラクターに渡されるか、既存の `Parameter` のプロパティとして設定されます。 `SourceColumn` は、<xref:System.Data.DataColumn> の値の取得先である <xref:System.Data.DataRow> の `Parameter` の名前です。 `SourceVersion` により、`DataRow` で値の取得に使用される `DataAdapter` のバージョンを指定します。

<xref:System.Data.DataRowVersion> で使用できる `SourceVersion` 列挙型の値を次の表に示します。

|DataRowVersion 列挙定数|説明|  
|--------------------------------|-----------------|  
|`Current`|このパラメーターは列の現在の値を使用します。 既定値です。|  
|`Default`|このパラメーターには列の `DefaultValue` を使用します。|  
|`Original`|このパラメーターは列の元の値を使用します。|  
|`Proposed`|このパラメーターは提示された値を使用します。|  

次のセクションの `SqlClient` コード サンプルでは、<xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 列を 2 つのパラメーター `CustomerID` (`SourceColumn`) および `@CustomerID` (`SET CustomerID = @CustomerID`) の `@OldCustomerID` として使用する `WHERE CustomerID = @OldCustomerID` のパラメーターを定義します。 `@CustomerID` パラメーターを使用して、**CustomerID** 列を `DataRow` の現在の値に更新します。 そのため、`SourceVersion` が `Current` である `CustomerID` の `SourceColumn` が使用されます。 `@OldCustomerID` パラメーターは、データ ソースの現在の行を識別するために使用されています。 一致する列の値がその行の `Original` バージョンで見つかったため、`SourceColumn` が `CustomerID` である同じ `SourceVersion` (`Original`) が使用されます。

## <a name="work-with-sqlclient-parameters"></a>SqlClient パラメーターの使用

次のコード サンプルでは、データベースから追加のスキーマ情報を取得するために <xref:Microsoft.Data.SqlClient.SqlDataAdapter> を作成し、<xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> を <xref:System.Data.MissingSchemaAction.AddWithKey> に設定する方法を示します。 <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> プロパティ、<xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> プロパティ、<xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> プロパティ、および <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> プロパティが設定され、各プロパティに対応する <xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトが <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> コレクションに追加されます。 このメソッドは `SqlDataAdapter` オブジェクトを返します。

[!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter#1](~/../sqlclient/doc/samples/SqlDataAdapter_SqlDataAdapter.cs#1)]

## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-datareaders.md)
- [コマンドとパラメーター](commands-parameters.md)
- [DataAdapter を使用してデータ ソースを更新する](update-data-sources-with-dataadapters.md)
- [ストアド プロシージャによるデータの変更](modify-data-with-stored-procedures.md)
- [ADO.NET のデータ型のマッピング](data-type-mappings-ado-net.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
