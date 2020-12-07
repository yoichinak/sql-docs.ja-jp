---
title: JDBC のバッチ挿入に対する一括コピー API
description: Microsoft JDBC Driver for SQL Server では、Azure Data Warehouse に対するバッチ挿入操作に一括コピーを使用することがサポートされています。データベースにデータを読み込むスピードが速くなります。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09eac13d41656721a9a4cc6d8fb8fa9790779018
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943031"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>バッチ挿入操作に一括コピー API を使用する

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 for SQL Server では、Azure Data Warehouse に対するバッチ挿入操作に一括コピー API の使用がサポートされています。 この機能を使用すると、ユーザーは、バッチ挿入操作の実行時に、一括コピー操作をドライバーにバックグラウンドで実行させることができるようになります。 このドライバーは、通常のバッチ挿入操作で行われるのと同じデータを挿入したときのパフォーマンスを向上させることを目的としています。 ドライバーでは、通常のバッチ挿入操作の代わりに、一括コピー API を利用して、ユーザーの SQL クエリが解析されます。 バッチ挿入機能に対して一括コピー API を有効にするためのさまざまな方法と、その制限事項の一覧を以下に示します。 このページには、使用とパフォーマンスの向上を示す小さなサンプル コードも含まれています。

この機能は、PreparedStatement および CallableStatement の `executeBatch()` & `executeLargeBatch()` API にのみ適用できます。

## <a name="prerequisites"></a>前提条件

バッチ挿入に一括コピー API を有効にするには、次の 2 つの前提条件があります。

* サーバーは Azure Data Warehouse であること。
* クエリは挿入クエリであること (クエリにコメントを含めることはできますが、この機能を有効にするには、クエリの先頭に INSERT キーワードを使用する必要があります)。

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>バッチ挿入に一括コピー API を有効にする

バッチ挿入に一括コピー API を有効にするには、次の 3 つの方法があります。

### <a name="1-enabling-with-connection-property"></a>1.接続プロパティを使用して有効にする

接続文字列に **useBulkCopyForBatchInsert=true;** を追加して、この機能を有効にします。

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2.SQLServerConnection オブジェクトから setUseBulkCopyForBatchInsert() メソッドを使用して有効にする

**SQLServerConnection.setUseBulkCopyForBatchInsert(true)** を呼び出してこの機能を有効にします。

**SQLServerConnection.getUseBulkCopyForBatchInsert()** で **useBulkCopyForBatchInsert** 接続プロパティの現在の値が取得されます。

**useBulkCopyForBatchInsert** の値は、初期化時には各 PreparedStatement に対して一定のままです。 後続の **SQLServerConnection.setUseBulkCopyForBatchInsert()** への呼び出しは、その値に関して、既に作成された PreparedStatement には影響しません。

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3.SQLServerDataSource オブジェクトから setUseBulkCopyForBatchInsert() メソッドを使用して有効にする

上記と同様ですが、SQLServerDataSource を使用して SQLServerConnection オブジェクトを作成します。 どちらの方法も、同じ結果が得られます。

## <a name="known-limitations"></a>既知の制限事項

現在、この機能には、次の制限事項が適用されます。

* パラメーター化されていない値 (`INSERT INTO TABLE VALUES (?, 2`) など) を含む挿入クエリはサポートされていません。 この関数でサポートされているパラメーターは、ワイルドカード (?) だけです。
* INSERT-SELECT 式 (`INSERT INTO TABLE SELECT * FROM TABLE2` など) を含む挿入クエリはサポートされていません。
* 複数の VALUE 式 (`INSERT INTO TABLE VALUES (1, 2) (3, 4)` など) を含む挿入クエリはサポートされていません。
* OPTION 句が後に続く挿入クエリ、複数のテーブルと結合された挿入クエリ、または別のクエリが後に続く挿入クエリはサポートされていません。
* 一括コピー API の制限により、`MONEY`、`SMALLMONEY`、`DATE`、`DATETIME`、`DATETIMEOFFSET`、`SMALLDATETIME`、`TIME`、`GEOMETRY`、`GEOGRAPHY` の各データ型は、現在、この機能ではサポートされていません。

"SQL Server" に関連しないエラーが原因でクエリが失敗した場合、ドライバーによってエラー メッセージがログに記録され、バッチ挿入の元のロジックにフォールバックされます。

## <a name="example"></a>例

次に示すのは、通常と一括コピー API の両方のシナリオで、1,000 行の Azure Synapse Analytics (SQL DW) に対するバッチ挿入操作のユース ケースを示すコード例です。

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

結果:

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>関連項目

[JDBC ドライバーによるパフォーマンスと信頼性の強化](improving-performance-and-reliability-with-the-jdbc-driver.md)
