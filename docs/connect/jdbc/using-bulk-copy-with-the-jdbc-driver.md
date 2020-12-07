---
title: JDBC ドライバーでの一括コピーの使用
description: SQLServerBulkCopy クラスを使用すると、標準の JDBC API よりも大幅にパフォーマンスが向上するデータ読み込みソリューションを Java で記述することができます。
ms.custom: ''
ms.date: 08/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69379b9af3dc126713cb2bbd3172003692a7d4de
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042235"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>JDBC ドライバーでの一括コピーの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft SQL Server には、SQL Server データベースのテーブルまたはビューに大きなファイルを高速で一括コピーするための、`bcp` という一般的なコマンド ライン ユーティリティが用意されています。 `SQLServerBulkCopy` クラスを使用すると、同様の機能を提供するコード ソリューションを Java で作成できます。 SQL Server のテーブルにデータを読み込むには、INSERT ステートメントを使用するなどの方法もありますが、`SQLServerBulkCopy` を使用すれば他の方法よりもパフォーマンス面で大幅に有利になります。  
  
`SQLServerBulkCopy` クラスを使用すると、SQL Server のテーブルにのみデータを書き込むことができます。 ただし、データ ソースは SQL Server に制限されていません。`ResultSet`、`RowSet`、または `ISQLServerBulkRecord` の実装で読み取れるデータであれば、任意のデータ ソースを使用できます。  
  
`SQLServerBulkCopy` クラスを使用すると、次のことを実行できます。  
  
- 単一の一括コピー操作  
  
- 複数の一括コピー操作  
  
- トランザクション内での一括コピー操作  
  
> [!NOTE]  
> Microsoft JDBC Driver 4.1 for SQL Server またはそれ以前のバージョン (SQLServerBulkCopy クラスをサポートしていない) を使用する場合、代わりに SQL Server Transact-SQL の BULK INSERT ステートメントを実行できます。  
  
## <a name="bulk-copy-example-setup"></a>一括コピーのセットアップ例  

`SQLServerBulkCopy` クラスは、SQL Server テーブルのみにデータを書き込む場合に使用できます。 この記事内に表示されているコード サンプルには、SQL Server のサンプル データベース [AdventureWorks](../../samples/adventureworks-install-configure.md) が使用されています。 コード サンプルの既存テーブルの改変を防ぐため、別途作成したテーブルにデータを書き込みます。このテーブルを最初に作成します。  
  
`BulkCopyDemoMatchingColumns` テーブルと `BulkCopyDemoDifferentColumns` テーブルはどちらも、AdventureWorks `Production.Products` テーブルに基づいています。 コード サンプルではこれらのテーブルを使用し、`Production.Products` テーブルからこれらのサンプル テーブルのいずれかにデータを追加します。 `BulkCopyDemoDifferentColumns` テーブルは、ソース データからコピー先のテーブルに列をマップする方法を例示するサンプルに使用されます。`BulkCopyDemoMatchingColumns` は他のサンプルの大部分に使用されます。  
  
1 つの `SQLServerBulkCopy` クラスを使用して複数のテーブルに書き込む方法を示すコード サンプルもあります。 これらのサンプルでは、`BulkCopyDemoOrderHeader` テーブルと `BulkCopyDemoOrderDetail` テーブルをコピー先のテーブルとして使用します。 これらのテーブルは、AdventureWorks の `Sales.SalesOrderHeader` テーブルと `Sales.SalesOrderDetail` テーブルに基づいています。  
  
> [!NOTE]  
> `SQLServerBulkCopy` コード サンプルでは、`SQLServerBulkCopy` だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server のインスタンス内に存在する場合、Transact-SQL INSERT ...SELECT ステートメントを使用すればより簡単かつ高速にデータをコピーすることができます。  

### <a name="table-setup"></a>テーブルのセットアップ  

コード サンプルを正しく実行するために必要なテーブルを作成するには、SQL Server データベースで次の Transact-SQL ステートメントを実行する必要があります。  

```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```

## <a name="single-bulk-copy-operations"></a>単一の一括コピー操作

SQL Server の一括コピー操作を実行する最も簡単な方法は、データベースに対して単一操作を実行することです。 既定では、一括コピー操作は分離された操作として実行されます。このコピー操作は非トランザクション方式で処理され、ロールバックできません。  
  
> [!NOTE]  
> エラーの発生時に、バルク コピー処理の全部または一部をロールバックする必要がある場合は、`SQLServerBulkCopy` が管理するトランザクションを使用するか、または既存のトランザクション内でバルク コピー操作を実行できます。  
> 詳細については、「[トランザクションと一括コピー操作](#transaction-and-bulk-copy-operations)」を参照してください。  
  
 通常、一括コピー操作の実行手順は次のようになります。  
  
1. コピー元のサーバーに接続し、コピーするデータを取得します。 `ResultSet` オブジェクトまたは `ISQLServerBulkRecord` の実装からデータを取得できる場合は、他のソースから取得する場合もあります。  
  
2. コピー先のサーバーに接続します (`SQLServerBulkCopy` を使用して接続を確立しない場合)。  
  
3. `SQLServerBulkCopy` オブジェクトを作成し、`setBulkCopyOptions` で必要なプロパティを設定します。  
  
4. `setDestinationTableName` メソッドを呼び出し、一括挿入操作の対象テーブルを指定します。  
  
5. `writeToServer` メソッドのいずれかを呼び出します。  
  
6. オプションとして、`setBulkCopyOptions` でプロパティを更新したり、必要に応じて `writeToServer` をもう一度呼び出したりします。  
  
7. `close` を呼び出すか、try-with-resources ステートメント内に一括コピー操作をラップします。  
  
> [!CAUTION]  
> コピー元とコピー先の列のデータ型を一致させることをお勧めします。 データ型が一致しない場合、`SQLServerBulkCopy` はコピー元のそれぞれの値をコピー先のデータ型に変換しようとします。 この変換はパフォーマンスに影響を及ぼすだけでなく、予期しないエラーが発生する場合もあります。 たとえば、double データ型はたいていの場合 decimal データ型に変換できますが、変換できない場合もあります。  
  
### <a name="example"></a>例

次のアプリケーションは、`SQLServerBulkCopy` クラスを使用してデータを読み込む方法を示しています。 この例では、`ResultSet` を使用し、SQL Server の AdventureWorks データベースに格納された Production.Product テーブルのデータを、同じデータベース内の同等のテーブルにコピーします。  
  
> [!IMPORTANT]  
> このサンプルは、「[テーブルのセットアップ](#table-setup)」で説明しているように作業テーブルを作成してからでないと動作しません。 このコードでは、`SQLServerBulkCopy` だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server のインスタンス内に存在する場合、Transact-SQL INSERT ...SELECT ステートメントを使用すればより簡単かつ高速にデータをコピーすることができます。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopySingle {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // In real world applications you would
            // not use SQLServerBulkCopy to move data from one table to the other
            // in the same database. This is for demonstration purposes only.

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // table match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(rsSourceData);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Transact-SQL を使用した一括コピー操作の実行

次の例では、BULK INSERT ステートメントを実行する `executeUpdate` メソッドの使用方法を説明します。  
  
> [!NOTE]  
> データ ソースのファイル パスはサーバーに対する相対パスです。 一括コピー操作を正常に実行するには、サーバー プロセスがこのパスにアクセスできる必要があります。  

```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  

## <a name="multiple-bulk-copy-operations"></a>複数の一括コピー操作  

`SQLServerBulkCopy` クラスの単一のインスタンスを使用して、一括コピー操作を複数回実行できます。 コピー元とコピー先で操作パラメーターが変わる場合 (たとえば、コピー先のテーブル名など)、`writeToServer` メソッドを続けて呼び出す前に、次の例で示すようにパラメーターを更新する必要があります。 明示的に変更した場合を除き、すべてのプロパティ値は、任意のインスタンスに対して前回一括コピー操作を実行したときと同じ状態のままになっています。  

> [!NOTE]  
> 通常、バルク コピー操作を複数回実行する場合は、同じ `SQLServerBulkCopy` のインスタンスを使用する方が各操作ごとに別のインスタンスを使用するよりも効率的です。  
  
同じ `SQLServerBulkCopy` オブジェクトを使用してバルク コピー操作を複数回実行する場合は、コピー元またはコピー先の情報が各操作ごとに一致しているかまたは異なっているかどうかは制限されません。 ただし、サーバーに書き込み処理を行うときは、列の関連付け情報を毎回正しく設定する必要があります。  
  
> [!IMPORTANT]  
> このサンプルは、「[テーブルのセットアップ](#table-setup)」で説明しているように作業テーブルを作成してからでないと動作しません。 このコードでは、`SQLServerBulkCopy` だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server のインスタンス内に存在する場合、Transact-SQL INSERT ...SELECT ステートメントを使用すればより簡単かつ高速にデータをコピーすることができます。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyMultiple {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationHeaderTable = "dbo.BulkCopyDemoOrderHeader";
        String destinationDetailTable = "dbo.BulkCopyDemoOrderDetail";
        int countHeaderBefore, countDetailBefore, countHeaderAfter, countDetailAfter;
        ResultSet rsHeader, rsDetail;

        try (Connection sourceConnection1 = DriverManager.getConnection(connectionUrl);
                Connection sourceConnection2 = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection1.createStatement();
                PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(
                        "SELECT [SalesOrderID], [OrderDate], [AccountNumber] FROM [Sales].[SalesOrderHeader] WHERE [AccountNumber] = ?;");
                PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(
                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], [SalesOrderDetailID], [OrderQty], [ProductID], [UnitPrice] FROM "
                                + "[Sales].[SalesOrderDetail] INNER JOIN [Sales].[SalesOrderHeader] ON "
                                + "[Sales].[SalesOrderDetail].[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] WHERE [AccountNumber] = ?;");
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl);) {

            // Empty the destination tables.
            stmt.executeUpdate("DELETE FROM " + destinationHeaderTable);
            stmt.executeUpdate("DELETE FROM " + destinationDetailTable);

            // Perform an initial count on the destination
            // table with matching columns.
            countHeaderBefore = getRowCount(stmt, destinationHeaderTable);

            // Perform an initial count on the destination
            // table with different column positions.
            countDetailBefore = getRowCount(stmt, destinationDetailTable);

            // Get data from the source table as a ResultSet.
            // The Sales.SalesOrderHeader and Sales.SalesOrderDetail
            // tables are quite large and could easily cause a timeout
            // if all data from the tables is added to the destination.
            // To keep the example simple and quick, a parameter is
            // used to select only orders for a particular account
            // as the source for the bulk insert.
            preparedStmt1.setString(1, "10-4020-000034");
            rsHeader = preparedStmt1.executeQuery();

            // Get the Detail data in a separate connection.
            preparedStmt2.setString(1, "10-4020-000034");
            rsDetail = preparedStmt2.executeQuery();

            // Create the SQLServerBulkCopySQLServerBulkCopy object.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setBulkCopyTimeout(100);
            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationHeaderTable);

            // Guarantee that columns are mapped correctly by
            // defining the column mappings for the order.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("OrderDate", "OrderDate");
            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");

            // Write rsHeader to the destination.
            bulkCopy.writeToServer(rsHeader);

            // Set up the order details destination.
            bulkCopy.setDestinationTableName(destinationDetailTable);

            // Clear the existing column mappings
            bulkCopy.clearColumnMappings();

            // Add order detail column mappings.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("SalesOrderDetailID", "SalesOrderDetailID");
            bulkCopy.addColumnMapping("OrderQty", "OrderQty");
            bulkCopy.addColumnMapping("ProductID", "ProductID");
            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");

            // Write rsDetail to the destination.
            bulkCopy.writeToServer(rsDetail);

            // Perform a final count on the destination
            // tables to see how many rows were added.
            countHeaderAfter = getRowCount(stmt, destinationHeaderTable);
            countDetailAfter = getRowCount(stmt, destinationDetailTable);

            System.out.println((countHeaderAfter - countHeaderBefore) + " rows were added to the Header table.");
            System.out.println((countDetailAfter - countDetailBefore) + " rows were added to the Detail table.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

## <a name="transaction-and-bulk-copy-operations"></a>トランザクションと一括コピー操作

 一括コピー操作は、単独の操作として、または、複数の手順からなるトランザクションの一部として実行されます。 複数の手順からなるトランザクションの一部として実行する場合、挿入、更新、削除など、他のデータベース操作に加えて、同じトランザクション内で一括コピー操作を複数回実行でき、トランザクション全体をコミットまたはロールバックすることもできます。  
  
 既定では、一括コピー操作は単独の操作として実行されます。 この一括コピー操作は非トランザクション方式で処理され、ロールバックできません。 エラーの発生時に一括コピー処理の全部または一部をロールバックする必要がある場合は、`SQLServerBulkCopy` により管理されるトランザクションを使用するか、既存のトランザクション内で一括コピー操作を実行できます。  

## <a name="extended-bulk-copy-for-azure-data-warehouse"></a>拡張された Azure Data Warehouse の一括コピー

ドライバー バージョン 8.4.1 には、新しい接続プロパティである `sendTemporalDataTypesAsStringForBulkCopy` が追加されています。 このブール型プロパティの既定値は `true` です。

この接続プロパティを `false` に設定すると、**DATE**、**DATETIME**、**DATIMETIME2**、**DATETIMEOFFSET**、**SMALLDATETIME**、および **TIME** データ型が文字列として送信されず、それぞれの型として送信されます。

テンポラル データ型をそれぞれの型として送信すると、ユーザーは Azure Synapse Analytics (SQL DW) の列にデータを送信できます。この操作は、以前はドライバーがデータを文字列に変換していたためできませんでした。 SQL Server では暗黙的な変換が実行されるため、テンポラル列に文字列データを送信しても機能しますが、Azure Synapse Analytics (SQL DW) では同じように機能しません。

さらに、**v8.4.1** 以降では、この接続文字列を 'false' に設定しなくても、**MONEY** および **SMALLMONEY** データ型が **DECIMAL** ではなく **MONEY** / **SMALLMONEY** データ型 として送信されるため、これらのデータ型も Azure Synapse Analytics (SQL DW) に一括コピーできます。

### <a name="extended-bulk-copy-for-azure-data-warehouse-limitations"></a>拡張された Azure Data Warehouse の一括コピーの制限事項

現在、次の 2 つの制限があります。

1. この接続プロパティが `false` に設定されている場合、次の例のように、ドライバーは各テンポラル データ型の既定の文字列リテラル形式のみを受け入れます。

    `DATE: YYYY-MM-DD`

    `DATETIME: YYYY-MM-DD hh:mm:ss[.nnn]`

    `DATETIME2: YYYY-MM-DD hh:mm:ss[.nnnnnnn]`

    `DATETIMEOFFSET: YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+/-}hh:mm]`

    `SMALLDATETIME:YYYY-MM-DD hh:mm:ss`

    `TIME: hh:mm:ss[.nnnnnnn]`

2. この接続プロパティが `false` に設定されている場合、一括コピーで指定する列の種類は、[こちら](../../connect/jdbc/using-basic-data-types.md)のデータ型マッピング表を反映している必要があります。 たとえば、以前のユーザーはデータを `DATE` 列に一括コピーするために `java.sql.Types.TIMESTAMP` を指定できましたが、この機能を有効にした場合は、同じ操作を実行するために `java.sql.Types.DATE` を指定する必要があります。
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>非トランザクション処理の一括コピー操作の実行

次のアプリケーションでは、非トランザクション処理の一括コピー操作で操作途中にエラーが発生した場合の処理を示しています。  
  
例では、コピー元のテーブルとコピー先のテーブルにそれぞれ `ProductID` という名前の ID 列があります。 このコードでは、最初にコピー先のテーブルの行をすべて削除してコピー先を用意し、コピー元のテーブルに存在する `ProductID` 行を 1 行挿入しています。 既定では、行が追加されるたびに、コピー先のテーブル内の ID 列に新しい値が生成されます。 この例では、一括読み込み処理でコピー元のテーブルの ID 値を強制的に使用する接続が開かれるときに、オプションが設定されます。  
  
このバルク コピー操作は、`BatchSize` プロパティを 10 に設定して実行されます。 操作中に無効な行が検出されると、例外がスローされます。 次に示す最初の例の一括コピー操作はトランザクション処理ではありません。 エラー発生ポイントまでにコピーされたバッチはすべてコミットされ、重複キーが含まれるバッチはロールバックされます。また、一括コピー操作は、他のバッチを処理する前に中止されます。  
  
> [!NOTE]  
> このサンプルは、「[テーブルのセットアップ](#table-setup)」で説明しているように作業テーブルを作成してからでないと動作しません。 このコードでは、`SQLServerBulkCopy` だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server のインスタンス内に存在する場合、Transact-SQL INSERT ...SELECT ステートメントを使用すればより簡単かつ高速にデータをコピーすることができます。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyNonTransacted {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error
            // after some of the batches have been copied.
            try {
                bulkCopy.writeToServer(rsSourceData);
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>トランザクションでの専用の一括コピー操作の実行

既定では、一括コピー操作ではトランザクション自体は作成されません。 専用の一括コピー操作を実行する場合は、接続文字列を使用して `SQLServerBulkCopy` の新しいインスタンスを作成します。 このシナリオでは、一括コピー操作の各バッチがデータベースによって暗黙的にコミットされます。 `SQLServerBulkCopyOptions` の `UseInternalTransaction` オプションを `true` に設定すると、一括コピー操作によってトランザクションが作成され、一括コピー操作の各バッチの後にコミットが実行されます。
  
```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```

### <a name="using-existing-transactions"></a>既存のトランザクションの使用

パラメーターとして有効になっているトランザクションを含む `Connection` オブジェクトを `SQLServerBulkCopy` コンストラクター内で渡すことができます。 この場合、一括コピー操作は既存のトランザクションで実行され、このトランザクションの状態は変更されません (つまり、コミットも中止もされません)。 これにより、アプリケーションは他のデータベース操作を行うトランザクションで一括コピー操作を実行できます。 エラーが発生したため一括コピー操作全体をロールバックする必要がある場合、またはロールバック可能な大きな処理の一部として一括コピー処理を実行する場合、一括コピー操作の開始後いつでも `Connection` オブジェクト上でロールバックを実行できます。  
  
次のアプリケーションは、`BulkCopyNonTransacted` と似ていますが、一括コピー操作がより大きな外部トランザクションに含まれている点が異なります。 主キー違反エラーが発生した場合、トランザクション全体がロールバックされ、コピー先のテーブルに行は追加されません。

> [!NOTE]  
> このサンプルは、「[テーブルのセットアップ](#table-setup)」で説明しているように作業テーブルを作成してからでないと動作しません。 このコードでは、`SQLServerBulkCopy` だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server のインスタンス内に存在する場合、Transact-SQL INSERT ...SELECT ステートメントを使用すればより簡単かつ高速にデータをコピーすることができます。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyExistingTransactions {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;
        SQLServerBulkCopyOptions copyOptions;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object inside the transaction.
            destinationConnection.setAutoCommit(false);

            copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error.
            try {
                bulkCopy.writeToServer(rsSourceData);
                destinationConnection.commit();
            }
            catch (SQLException e) {
                e.printStackTrace();
                destinationConnection.rollback();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        catch (Exception e) {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="bulk-copy-from-a-csv-file"></a>CSV ファイルからの一括コピー  

 次のアプリケーションは、`SQLServerBulkCopy` クラスを使用してデータを読み込む方法を示しています。 この例では、CSV ファイルを使用し、SQL Server の AdventureWorks データベース内の Production.Product テーブルからエクスポートされたデータを、このデータベース内の同等のテーブルにコピーします。  
  
> [!IMPORTANT]  
> このサンプルは、「[テーブルのセットアップ](#table-setup)」で説明しているように作業テーブルを作成して取得してからでないと動作しません。  
  
1. **SQL Server Management Studio** を開き、AdventureWorks データベースを含む SQL Server に接続します。  
  
2. データベースを展開し、AdventureWorks データベースを右クリックして、 **[タスク]** 、 **[データのエクスポート]** の順にクリックします。  
  
3. データ ソースに関しては、使用する SQL Server に接続できる**データ ソース** (例: SQL Server Native Client 11.0) を選択し、構成を確認して **[次へ]** をクリックします。  
  
4. コピー先に関しては、 **[フラット ファイル変換先]** を選択し、「`C:\Test\TestBulkCSVExample.csv`」のように変換先を含めた **[ファイル名]** を入力します。 **[形式]** が [区切りあり]、 **[テキスト修飾子]** が [なし] に設定されていることを確認し、 **[先頭データ行を列名として使用する]** を有効にして、 **[次へ]** をクリックします。  
  
5. **[転送するデータを指定するためのクエリを記述する]** をオンにして、 **[次へ]** をクリックします。  **SQL ステートメント** `SELECT ProductID, Name, ProductNumber FROM Production.Product` を入力し、 **[次へ]** をクリックします。  
  
6. 次のように構成を確認します。行区切り記号を `{CR}{LF}`、列区切り記号をコンマ `{,}` にしておくことができます。  **[マッピングの編集]** を選択し ... 各列のデータの **[型]** が適切かどうか (`ProductID` には整数、他は Unicode 文字列など) を確認します。  
  
7. **[完了]** に進んで、エクスポートを実行します。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopyCSV {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;

        // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.
        // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.
        try (Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = destinationConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);
                SQLServerBulkCSVFileRecord fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);) {

            // Set the metadata for each column to be copied.
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // data reader match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(fileRecord);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```  

### <a name="bulk-copy-with-delimiters-as-data-in-csv-file"></a>CSV ファイルのデータとして使用される区切り記号を含む一括コピー

ドライバー バージョン 8.4.1 には、新しい API `SQLServerBulkCSVFileRecord.setEscapeColumnDelimitersCSV(boolean)` が追加されています。 true に設定すると、次のルールが適用されます。

- 各フィールドを二重引用符で囲んでも囲まなくてもかまいかせん。
- フィールドを二重引用符で囲む場合、そのフィールド内に二重引用符を含めることはできません。
- 二重引用符や区切り記号を含むフィールドは、二重引用符で囲む必要があります。
- 二重引用符を使用してフィールドを囲む場合、フィールド内に現れる二重引用符は、その直前に別の二重引用符を追加してエスケープする必要があります。

### <a name="bulk-copy-with-always-encrypted-columns"></a>一括コピーと [Always Encrypted] 列  

Microsoft JDBC Driver 6.0 for SQL Server 以降では、[Always Encrypted] 列の一括コピーがサポートされています。  
  
一括コピーのオプションと、コピー元およびコピー先テーブルの暗号化の種類によっては、JDBC ドライバーはデータを透過的に復号し、暗号化することがあります。あるいは、暗号化されたデータをそのまま送信することがあります。 たとえば、暗号化されている列から暗号化されていない列にデータを一括コピーするとき、このドライバーは SQL Server に送信する前にデータを透過的に復号します。 同様に、暗号化されていない列から (あるいは、CSV ファイルから) 暗号化されている列にデータを一括コピーするとき、このドライバーは SQL Server に送信する前にデータを透過的に復号します。 コピー元とコピー先の両方が暗号化されている場合、`allowEncryptedValueModifications` 一括コピー オプションによっては、このドライバーはデータをそのまま送信するか、復号し、再び暗号化してから SQL Server に送信します。  
  
詳細については、下の `allowEncryptedValueModifications` 一括コピー オプションと「[JDBC ドライバーで Always Encrypted を使用する](using-always-encrypted-with-the-jdbc-driver.md)」を参照してください。  
  
> [!IMPORTANT]  
> CSV ファイルから暗号化されている列にデータを一括コピーするときの Microsoft JDBC Driver 6.0 for SQL Server の制限:  
>
> 日付と時刻の型については、Transact-SQL の既定の文字列リテラル形式がサポートされます  
>
> DATETIME データ型と SMALLDATETIME データ型はサポートされていません  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>JDBC ドライバー用 API の一括コピー  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy

別のソースからのデータを含む SQL Server テーブルを効率的に一括読み込みできます。  
  
Microsoft SQL Server には、単一のサーバー上または複数のサーバー間で、テーブルから別のテーブルへデータを移動するための bcp という一般的なコマンド プロンプト ユーティリティが用意されています。 `SQLServerBulkCopy` クラスを使用すると、同様の機能を提供するコード ソリューションを Java で記述できます。 SQL Server テーブルにデータを読み込む方法は他にもありますが (INSERT ステートメントなど)、`SQLServerBulkCopy` を使用する方が大幅にパフォーマンスが向上します。  
  
`SQLServerBulkCopy` クラスは、SQL Server テーブルのみにデータを書き込む場合に使用できます。 ただし、データ ソースは SQL Server に制限されていません。`ResultSet` インスタンスまたは `ISQLServerBulkRecord` の実装で読み取れるデータであれば、任意のデータ ソースを使用できます。  
  
| コンストラクター | 説明 |
| ----------- | ----------- |
| `SQLServerBulkCopy(Connection connection)` | `SQLServerBulkCopy` の指定されたオープン インスタンスを使用して、`SQLServerConnection` クラスの新しいインスタンスを初期化します。 `Connection` でトランザクションが有効になっている場合、コピー操作はそのトランザクション内で実行されます。 |
| `SQLServerBulkCopy(String connectionURL)` | 指定された `connectionURL` に基づいて、`SQLServerConnection` の新しいインスタンスを初期化して開きます。 コンストラクターは、`SQLServerConnection` を使用して、`SQLServerBulkCopy` クラスの新しいインスタンスを初期化します。 |
  
| プロパティ | 説明 |
| -------- | ----------- |
| `String DestinationTableName` | サーバー上にあるコピー先のテーブルの名前。<br /><br /> `writeToServer` の呼び出し時に `DestinationTableName` が設定されていない場合は、`SQLServerException` がスローされます。<br /><br /> `DestinationTableName` は 3 部構成の名前 (`<database>.<owningschema>.<name>`) です。 必要に応じ、テーブル名をデータベースと所有しているスキーマで修飾することができます。 ただし、テーブル名にアンダースコア ("_") またはその他の特殊文字を使用する場合は、角かっこで囲んで、名前をエスケープする必要があります。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。 |
| `ColumnMappings` | 列のマッピングでは、データ ソース内の列とコピー先の列の間の関係を定義します。<br /><br /> マッピングが定義されていない場合、列は序数の位置に基づいて暗黙的にマップされます。 これを行うには、コピー元のスキーマとコピー先のスキーマが一致する必要があります。 一致しない場合、例外がスローされます。<br /><br /> マッピングが空でない場合、データ ソースに存在するすべての列を指定する必要はありません。 マップされていない列は無視されます。<br /><br /> コピー元とコピー先の列は、名前か序数のいずれかで参照できます。 |
  
| Method | 説明 |
| ------ | ----------- |
| `void addColumnMapping(int sourceColumn, int destinationColumn)` | 序数を使用してコピー元とコピー先の両方の列を指定する、新しい列マッピングを追加します。 |
| `void addColumnMapping (int sourceColumn, String destinationColumn)` | コピー元の列の序数とコピー先の列の列名を使用する、新しい列マッピングを追加します。 |
| `void addColumnMapping (String sourceColumn, int destinationColumn)` | コピー元の列を説明する列名とコピー先の列を指定する序数を使用する、新しい列マッピングを追加します。 |
| `void addColumnMapping (String sourceColumn, String destinationColumn)` | 列名を使用してコピー元とコピー先の両方の列を指定する、新しい列マッピングを追加します。 |
| `void clearColumnMappings()` | 列マッピングの内容を消去します。 |
| `void close()` | `SQLServerBulkCopy` インスタンスを閉じます。 |
| `SQLServerBulkCopyOptions getBulkCopyOptions()` | `SQLServerBulkCopyOptions` の現在のセットを取得します。 |
| `String getDestinationTableName()` | 現在のコピー先テーブル名を取得します。 |
| `void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)` | 指定したオプションに従って `SQLServerBulkCopy` インスタンスの動作を更新します。 |
| `void setDestinationTableName(String tableName)` | コピー先テーブルの名前を設定します。 |
| `void writeToServer(ResultSet sourceData)` | 指定された `ResultSet` のすべての行を、`SQLServerBulkCopy` オブジェクトの `DestinationTableName` プロパティで指定される宛先テーブルにコピーします。 |
| `void writeToServer(RowSet sourceData)` | 指定された `RowSet` のすべての行を、`SQLServerBulkCopy` オブジェクトの `DestinationTableName` プロパティで指定される宛先テーブルにコピーします。 |
| `void writeToServer(ISQLServerBulkRecord sourceData)` | 指定された `ISQLServerBulkRecord` の実装のすべての行を、`SQLServerBulkCopy` オブジェクトの `DestinationTableName` プロパティで指定される宛先テーブルにコピーします。 |
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  

 `SQLServerBulkCopy` インスタンス内の `writeToServer` メソッドの動作を制御する設定のコレクション。  
  
| コンストラクター | 説明 |
| ----------- | ----------- |
| `SQLServerBulkCopyOptions()` | すべての設定に既定値を使用して `SQLServerBulkCopyOptions` クラスの新しいインスタンスを初期化します。 |
  
 get アクセス操作子および set アクセス操作子は、次のオプションのために存在します。  
  
| オプション | 説明 | Default |
| ------ | ----------- | ------- |
| `boolean CheckConstraints` | データが挿入される際の制約をチェックします。 | False - 制約はチェックされません |
| `boolean FireTriggers` | データベースに挿入される行に対する挿入トリガーがサーバーで発生します。 | False - トリガーは発生しません。 |
| `boolean KeepIdentity` | ソースの ID 値が保持されます。 | False - コピー先により ID 値が割り当てられます |
| `boolean KeepNulls` | 既定値の設定に関係なく、コピー先のテーブル内の null 値が保持されます。 | False - 該当する個所で、null 値は既定値で置き換えられます。 |
| `boolean TableLock` | 一括コピー操作の実行中、一括更新のロックを取得します。 | False - 行ロックが使用されます。 |
| `boolean UseInternalTransaction` | `true` に設定した場合、一括コピー操作の各バッチがトランザクション内で発生します。 `SQLServerBulkCopy` がコンストラクターで指定されている既存の接続を使用する場合、`SQLServerException` が発生します。  `SQLServerBulkCopy` が専用の接続を作成した場合、トランザクションが作成され、各バッチに対してコミットされます。 | False - トランザクションなし |
| `int BatchSize` | 各バッチに含まれる行数。 各バッチの最後に、バッチ内の行がサーバーに送信されます。<br /><br /> `BatchSize` 分の行が処理されるか、コピー先のデータ ソースに送信する行がなくなると、バッチは完了します。  `UseInternalTransaction` オプションが `false` に設定されて `SQLServerBulkCopy` インスタンスが宣言されている場合、行は一度にサーバーの `BatchSize` 行に送信されますが、トランザクション関連のアクションは実行されません。 `UseInternalTransaction` が `true` に設定されている場合は、行の各バッチは明示的なトランザクション内で実行されます。 | 0 - 各 `writeToServer` 操作が 1 つのバッチであることを示します |
| `int BulkCopyTimeout` | タイムアウトになる前に完了する操作の秒数。値 0 は無制限を意味しており、一括コピーは無期限に待機します。 | 60 秒。 |
| `boolean allowEncryptedValueModifications` | このオプションは、Microsoft JDBC Driver 6.0 (以降) for SQL Server で利用できます。<br /><br /> `true` に設定されている場合、`allowEncryptedValueModifications` はデータを暗号化解除することなく、テーブルまたはデータベース間で暗号化データを一括コピーできます。 一般的に、アプリケーションはデータを復号せずに 1 つのテーブルの暗号化された列からデータを選択し (アプリは、列の暗号化設定キーワードを無効に設定しているデータベースに接続します)、それからこのオプションを使用し、依然として暗号化されたままのデータを一括挿入します。 詳細については、「[JDBC ドライバーでの Always Encrypted の使用](using-always-encrypted-with-the-jdbc-driver.md)」を参照してください。<br /><br /> データベースが破損する可能性があるので、`allowEncryptedValueModifications` を `true` に指定する際には注意が必要です。これは、データが実際に暗号化されているかどうか、またはターゲット列と同じ暗号化のタイプ、アルゴリズム、およびキーを使用して正しく暗号化されているかどうかを、ドライバーがチェックしないためです。 |
  
 ゲッターとセッター:  
  
| メソッド | 説明 |
| ------- | ----------- |
| `boolean isCheckConstraints()` | データの挿入中、制約を確認するかどうかを示します。 |
| `void setCheckConstraints(boolean checkConstraints)` | データの挿入中、制約を確認するかどうかを設定します。 |
| `boolean isFireTriggers()` | データベースに挿入される行に対する挿入トリガーをサーバーから始動するかどうかを示します。 |
| `void setFireTriggers(boolean fireTriggers)` | データベースに挿入される行に対するトリガーを始動するようにサーバーを設定するかどうかを設定します。 |
| `boolean isKeepIdentity()` | コピー元の ID 値を保存するかどうかを示します。 |
| `void setKeepIdentity(boolean keepIdentity)` | ID 値を保存するかどうかを設定します。 |
| `boolean isKeepNulls()` | 既定値の設定に関係なく、コピー先テーブルに null 値を保存するかどうかを、あるいは null 値を既定値 (該当する場合) で置換するかどうかを示します。 |
| `void setKeepNulls(boolean keepNulls)` | 既定値の設定に関係なく、コピー先テーブルに null 値を保存するかどうかを、あるいは null 値を既定値 (該当する場合) で置換するかどうかを設定します。 |
| `boolean isTableLock()` | 一括コピー操作の実行中、`SQLServerBulkCopy` で一括更新のロックを取得するかどうかを示します。 |
| `void setTableLock(boolean tableLock)` | 一括コピー操作の実行中、`SQLServerBulkCopy` で一括更新のロックを取得するかどうかを設定します。 |
| `boolean isUseInternalTransaction()` | 一括コピー操作の各バッチがトランザクション内で発生するかどうかを指定します。 |
| `void setUseInternalTranscation(boolean useInternalTransaction)` | 一括コピー操作の各バッチがトランザクション内で発生するかどうかを設定します。 |
| `int getBatchSize()` | 各バッチの行数を取得します。 各バッチの最後に、バッチ内の行がサーバーに送信されます。 |
| `void setBatchSize(int batchSize)` | 各バッチの行数を設定します。 各バッチの最後に、バッチ内の行がサーバーに送信されます。 |
| `int getBulkCopyTimeout()` | タイムアウトになる前に完了する操作の秒数を取得します。 |
| `void  setBulkCopyTimeout(int timeout)` | タイムアウトになる前に完了する操作の秒数を設定します。 |
| `boolean isAllowEncryptedValueModifications()` | `allowEncryptedValueModifications` 設定が有効か無効かを示します。 |
| `void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)` | [Always Encrypted] 列を含む一括コピーに使用する `allowEncryptedValueModifications` 設定を構成します。 |
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  

 `ISQLServerBulkRecord` インターフェイスを使用すると、ファイルなどの任意のソースからデータを読み取るクラスを作成して、`SQLServerBulkCopy` インスタンスでそのデータを含む SQL Server テーブルを一括して読み込むことができます。  
  
| インターフェイス メソッド | 説明 |
| ----------------- | ----------- |
| `set<Integer> getColumnOrdinals()` | このデータ レコード内に表示される各列の序数を取得します。 |
| `String getColumnName(int column)` | 指定した列の名前を取得します。 |
| `int getColumnType(int column)` | 指定した列の JDBC データ型を取得します。 |
| `int getPrecision(int column)`  | 指定した列の精度を取得します。 |
| `object[] getRowData()` | オブジェクトの配列として、現在の行のデータを取得します。<br /><br /> 各オブジェクトは、指定した列の JDBC データ型を表すために使用する Java 言語の種類と一致する必要があります。  適切なマッピングの詳細については、「[JDBC ドライバーのデータ型について](understanding-the-jdbc-driver-data-types.md)」をご覧ください。 |
| `int getScale(int column)` | 指定した列の小数点以下桁数を取得します。 |
| `boolean isAutoIncrement(int column)` | その列が ID 列を表しているかどうかを示します。 |
| `boolean next()` | 次のデータ行に進みます。 |
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  

データ区切りがあり、各行がデータ行を表すファイルから、基本的な Java データ型を読み込むのに使用できる `ISQLServerBulkRecord` インターフェイスの単純な実装。  
  
実装に関する注意事項と制約事項:  
  
1. 1 行分のデータが一度に読み取られるため、各行で許容されるデータ量の上限は、使用可能なメモリによって制限されます。  
  
2. `varchar(max)`、`varbinary(max)`、`nvarchar(max)`、`sqlxml`、`ntext` などの大規模なデータ型のストリーミングはサポートされていません。  
  
3. CSV ファイル用に指定した区切り記号はデータ内に全く出現しないようにし、それが Java の正規表現で制限のある文字の場合には、正しくエスケープする必要があります。  
  
4. CSV ファイルの実装では、二重引用符はデータの一部として扱われます。 たとえば、区切り記号がコンマである場合、「`hello,"world","hello,world"`」という行は、それぞれ「`hello`」、「`"world"`」、「`"hello`」、「`world"`」という値を持つ 4 列として処理されます。  
  
5. 改行文字は行ターミネータとして使用され、データ内には使用できません。  
  
| Constructor | 説明 |
| ----------- | ----------- |
| `SQLServerBulkCSVFileRecord(String fileToParse, String encoding, String delimiter, boolean firstLineIsColumnNames)` | 指定された区切り記号とエンコードを使用して `fileToParse` 内の各行を解析する `SQLServerBulkCSVFileRecord` クラスの新しいインスタンスを初期化します。 `firstLineIsColumnNames` が True に設定されている場合、ファイルの最初の行は列名として解析されます。  エンコードが NULL の場合、既定のエンコードが使用されます。 |
| `SQLServerBulkCSVFileRecord(String fileToParse, String encoding, boolean firstLineIsColumnNames)` | コンマを区切り記号とし、指定されたエンコードを使用して `fileToParse` 内の各行を解析する `SQLServerBulkCSVFileRecord` クラスの新しいインスタンスを初期化します。 `firstLineIsColumnNames` が True に設定されている場合、ファイルの最初の行は列名として解析されます。  エンコードが NULL の場合、既定のエンコードが使用されます。 |
| `SQLServerBulkCSVFileRecord(String fileToParse, boolean firstLineIsColumnNames` | コンマを区切り記号とし、既定のエンコードを使用して `fileToParse` 内の各行を解析する `SQLServerBulkCSVFileRecord` クラスの新しいインスタンスを初期化します。 `firstLineIsColumnNames` が True に設定されている場合、ファイルの最初の行は列名として解析されます。 |
  
| メソッド | 説明 |
| ------ | ----------- |
| `void addColumnMetadata(int positionInFile, String columnName, int jdbcType, int precision, int scale)` | ファイル内の指定した列にメタデータを追加します。 |
| `void close()` | ファイル リーダーに関連付けられている任意のリソースを解放します。 |
| `void setTimestampWithTimezoneFormat(DateTimeFormatter dateTimeFormatter)` | ファイルからのタイムスタンプ データを `java.sql.Types.TIMESTAMP_WITH_TIMEZONE` として解析するための書式を設定します。 |
| `void setTimestampWithTimezoneFormat(String dateTimeFormat)` | ファイルからのタイム データを `java.sql.Types.TIME_WITH_TIMEZONE` として解析するための書式を設定します。 |
| `void setTimeWithTimezoneFormat(DateTimeFormatter dateTimeFormatter)` | ファイルからのタイム データを `java.sql.Types.TIME_WITH_TIMEZONE` として解析するための書式を設定します。 |
| `void setTimeWithTimezoneFormat(String timeFormat)` | ファイルからのタイム データを `java.sql.Types.TIME_WITH_TIMEZONE` として解析するための書式を設定します。 |
  
## <a name="see-also"></a>関連項目  

[JDBC ドライバーの概要](overview-of-the-jdbc-driver.md)  
