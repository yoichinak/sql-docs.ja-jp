---
title: ストアド プロシージャによるデータの変更
description: ストアド プロシージャの入力パラメーターおよび出力パラメーターを使用してデータベースに行を挿入し、新しい ID 値を返す方法について説明します。
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: f04884302bb1f13852097182d6ebc8e06570c66b
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744408"
---
# <a name="modify-data-with-stored-procedures"></a>ストアド プロシージャによるデータの変更

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ストアド プロシージャは、入力パラメーターとしてデータを受け取り、出力パラメーター、結果セット、または戻り値としてデータを返すことができます。 以下のサンプルは、Microsoft SqlClient Data Provider for SQL Server によって入力パラメーター、出力パラメーター、および戻り値が送受信される方法を示しています。 この例では、主キー列が ID 列であるテーブルに新しいレコードを挿入します。

> [!NOTE]
> <xref:Microsoft.Data.SqlClient.SqlDataAdapter> を使用してデータの編集または削除を行うためにストアド プロシージャを使用している場合は、ストアド プロシージャの定義内で **SET NOCOUNT ON** を使用しないようにしてください。 処理された行数がゼロとして返され、`DataAdapter` によってコンカレンシーの競合として解釈されてしまいます。 この場合、<xref:System.Data.DBConcurrencyException> がスローされます。

## <a name="example"></a>例

この例では、次のストアド プロシージャを使用して、**Northwind** **Categories** テーブルに新しいカテゴリを挿入します。 このストアド プロシージャは **CategoryName** 列の値を入力パラメーターとして受け取り、**SCOPE_IDENTITY()** 関数を使用して ID フィールド **CategoryID** の新しい値を取得し、その値を出力パラメーター内に返します。 RETURN ステートメントでは、 **\@\@ROWCOUNT** 関数を使用して、挿入された行の数を返します。

```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  

上述の `InsertCategory` ストアド プロシージャを <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> の <xref:Microsoft.Data.SqlClient.SqlDataAdapter> のソースとして使用する例を次に示します。 `@Identity` 出力パラメーターは、<xref:System.Data.DataSet> の `Update` メソッドが呼び出され、データベースにレコードが挿入された後で <xref:Microsoft.Data.SqlClient.SqlDataAdapter> に反映されます。 戻り値も取得されます。

[!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](~/../sqlclient/doc/samples/SqlDataAdapter_SPIdentityReturn.cs#1)]

## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得と変更](retrieving-modifying-data.md)
- [DataAdapter と DataReader](dataadapters-datareaders.md)
- [コマンドの実行](execute-command.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
