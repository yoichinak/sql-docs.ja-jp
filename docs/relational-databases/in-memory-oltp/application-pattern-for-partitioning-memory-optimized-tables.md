---
title: アプリケーションのパターン - メモリ最適化テーブルのパーティション分割
description: メモリ最適化テーブルに現在のアクティブなデータを格納し、パーティション テーブルに古いデータを格納するインメモリ OLTP アプリケーション デザイン パターンについて説明します。
ms.custom: seo-dt-2019,issue-PR=4700-14820
ms.date: 05/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57c6a851f192e9166fef872a9531a73339177238
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867368"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>メモリ最適化テーブルのパーティション分割に関するアプリケーションのパターン

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[hek_2](../../includes/hek-2-md.md)] では、比較的新しいデータでパフォーマンス リソースをふんだんに利用するアプリケーション設計パターンがサポートされます。 このパターンは、現在のデータが、以前のデータよりもはるかに頻繁に読み取られるか更新される場合に適用できます。 ここでは、現在のデータが "*アクティブ*" または "*ホット*" で、古いデータが "*コールド*" であるとします。

基本的には、"*ホット*" データをメモリ最適化テーブルに格納します。 "*コールド*" になった古いデータは、週または月単位でパーティション テーブルに移動されます。 パーティション テーブルのデータは、メモリ内ではなく、ディスクまたは他のハード ドライブに格納されています。

通常、この設計では **datetime** キーを使用して、ホット データとコールド データを効率的に区別するために移動プロセスを有効にします。

## <a name="advanced-partitioning"></a>高度なパーティション分割

この設計は、1 つのメモリ最適化パーティションも含むパーティション テーブルを模倣することを意図しています。 この設計を機能させるには、すべてのテーブルで共通のスキーマが確実に共有されるようにする必要があります。 この記事の後半にあるコード サンプルでは、この手法を示します。

新しいデータは、定義上、ホットであると見なされます。 ホット データは、メモリ最適化テーブルに挿入され、更新されます。 コールド データは、従来のパーティション テーブルに保持されます。 ストアド プロシージャでは、定期的に新しいパーティションを追加します。 パーティションには、メモリ最適化テーブルから移動された最新のコールド データが含まれます。

操作でホット データのみが必要な場合は、ネイティブ コンパイル ストアド プロシージャを使用してデータにアクセスできます。 ホットまたはコールド データにアクセスする可能性がある操作では、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、メモリ最適化テーブルをパーティション テーブルと結合する必要があります。

### <a name="add-a-partition"></a>パーティションを追加する

最近コールドになったデータは、パーティション テーブルに移動する必要があります。 この定期パーティション スワップの手順は次のとおりです。

1. メモリ最適化テーブルのデータでは、ホット データと新しいコールド データの間の境界またはカットオフである datetime を決定します。
2. 新しいコールド データを、インメモリ OLTP テーブルから *cold\_staging* テーブルに挿入します。
3. メモリ最適化テーブルから同じコールド データを削除します。
4. cold\_staging テーブルをパーティションにスワップします。
5. パーティションを追加します。

#### <a name="maintenance-window"></a>メンテナンス期間

上記の手順の 1 つは、メモリ最適化テーブルから新しいコールド データを削除することです。 このように削除してから、最後の手順で新しいパーティションを追加するまで、ある程度の期間があります。 この期間中に、アプリケーションで新しいコールド データを読み取ろうとすると失敗します。

関連サンプルについては、「 [アプリケーション レベルのパーティション分割](../../relational-databases/in-memory-oltp/application-level-partitioning.md)」を参照してください。

## <a name="code-sample"></a>コード サンプル

次の Transact-SQL サンプルは、プレゼンテーションを容易にする目的でのみ、一連の小さなコード ブロックで表示されています。 テストのために、それらをすべて 1 つの大きなコード ブロックに追加することができます。

全体として、T-SQL サンプルでは、メモリ最適化テーブルをディスク ベースのパーティション テーブルと共に使用する方法が示されています。

T-SQL サンプルの最初のフェーズでは、データベースを作成してから、データベース内にテーブルなどのオブジェクトを作成します。 後のフェーズでは、メモリ最適化テーブルからパーティション テーブルにデータを移動する方法を示します。

### <a name="create-a-database"></a>データベースを作成する

T-SQL サンプルのこのセクションでは、テスト データベースを作成します。 データベースは、メモリ最適化テーブルとパーティション テーブルの両方をサポートするように構成されています。

```sql
CREATE DATABASE PartitionSample;
GO

-- Add a FileGroup, enabled for In-Memory OLTP.
-- Change file path as needed.

ALTER DATABASE PartitionSample
    ADD FILEGROUP PartitionSample_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE PartitionSample
    ADD FILE(
        NAME = 'PartitionSample_mod',
        FILENAME = 'c:\data\PartitionSample_mod')
    TO FILEGROUP PartitionSample_mod;
GO
```

### <a name="create-a-memory-optimized-table-for-hot-data"></a>ホット データ用のメモリ最適化テーブルを作成する

このセクションでは、最新のデータ (ほとんどの場合、ホット データのままである) を保持するメモリ最適化テーブルを作成します。

```sql
USE PartitionSample;
GO

-- Create a memory-optimized table for the HOT Sales Order data.
-- Notice the index that uses datetime2.

CREATE TABLE dbo.SalesOrders_hot (
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,
   so_total MONEY NOT NULL,
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) WITH (MEMORY_OPTIMIZED=ON);
GO
```

### <a name="create-a-partitioned-table-for-cold-data"></a>コールド データ用のパーティション テーブルを作成する

このセクションでは、コールド データを保持するパーティション テーブルを作成します。

```sql
-- Create a partition and table for the COLD Sales Order data.
-- Notice the index that uses datetime2.

CREATE PARTITION FUNCTION [ByDatePF](datetime2) AS RANGE RIGHT
   FOR VALUES();
GO

CREATE PARTITION SCHEME [ByDateRange]
   AS PARTITION [ByDatePF]
   ALL TO ([PRIMARY]);
GO

CREATE TABLE dbo.SalesOrders_cold (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) ON [ByDateRange](so_date);
GO
```

### <a name="create-a-table-to-store-cold-data-during-move"></a>移動中にコールド データを格納するテーブルを作成する

このセクションでは、cold\_staging テーブルを作成します。 2 つのテーブルのホットおよびコールド データを結合するビューも作成されます。

```sql
-- A table used to briefly stage the newly cold data, during moves to a partition.

CREATE TABLE dbo.SalesOrders_cold_staging (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date datetime2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')
);
GO

-- A view, for retrieving the aggregation of hot plus cold data.

CREATE VIEW dbo.SalesOrders
AS SELECT so_id,
          cust_id,
          so_date,
          so_total,
          1 AS 'is_hot'
       FROM dbo.SalesOrders_hot
   UNION ALL
   SELECT so_id,
          cust_id,
          so_date,
          so_total,
          0 AS 'is_cold'
       FROM dbo.SalesOrders_cold;
GO
```

### <a name="create-the-stored-procedure"></a>ストアド プロシージャを作成する

このセクションでは、定期的に実行するストアド プロシージャを作成します。 プロシージャでは、新しいコールド データをメモリ最適化テーブルからパーティション テーブルに移動します。

```sql
-- A stored procedure to move all newly cold sales orders data
-- to its staging location.

CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2
   AS
   BEGIN
      BEGIN TRANSACTION;

      -- Insert the cold data as a temporary heap.
      INSERT INTO dbo.SalesOrders_cold_staging WITH (TABLOCKX)
      SELECT so_id , cust_id , so_date , so_total
         FROM dbo.SalesOrders_hot WITH (serializable)
         WHERE so_date <= @splitdate;

      -- Delete the moved data from the hot table.
      DELETE FROM dbo.SalesOrders_hot WITH (SERIALIZABLE)
         WHERE so_date <= @splitdate;

      -- Update the partition function, and switch in the new partition.
      ALTER PARTITION SCHEME [ByDateRange] NEXT USED [PRIMARY];

      DECLARE @p INT = (
        SELECT MAX(partition_number)
            FROM sys.partitions
            WHERE object_id = OBJECT_ID('dbo.SalesOrders_cold'));

      EXEC sp_executesql
        N'ALTER TABLE dbo.SalesOrders_cold_staging
            SWITCH TO dbo.SalesOrders_cold partition @i',
        N'@i int',
        @i = @p;

      ALTER PARTITION FUNCTION [ByDatePF]()
      SPLIT RANGE( @splitdate);

      -- Modify a constraint on the cold_staging table, to align with new partition.
      ALTER TABLE dbo.SalesOrders_cold_staging
         DROP CONSTRAINT CHK_SalesOrders_cold_staging;

      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging 
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';
      PRINT @sql;
      EXEC sp_executesql @sql;

      COMMIT;
END;
GO
```

### <a name="prepare-sample-data-and-demo-the-stored-procedure"></a>サンプル データを準備し、ストアド プロシージャのデモを行う

このセクションでは、サンプル データを生成して挿入してから、デモとしてストアド プロシージャを実行します。

```sql
-- Insert sample values into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO

-- Verify that the hot data is in the table, by selecting from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Treat all data in the hot table as cold data:
-- Run the stored procedure, to move (offload) all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Again, read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Retrieve the name of every partition.
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');

-- Insert more data into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, run the stored procedure, to move all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, retrieve the name of every partition.
-- The stored procedure can modify the partitions.
SELECT OBJECT_NAME( object_id) , partition_number , row_count
  FROM sys.dm_db_partition_stats ps
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold')
    AND index_id = 1;
```

### <a name="drop-all-the-demo-objects"></a>すべてのデモ オブジェクトを削除する

テスト システムからデモ テスト データベースを消去することを忘れないでください。

```sql
-- You must first leave the context of the PartitionSample database.

-- USE <A-Database-Name-Here>;
GO

DROP DATABASE PartitionSample;
GO
```

## <a name="see-also"></a>参照

[メモリ最適化テーブル](./sample-database-for-in-memory-oltp.md)