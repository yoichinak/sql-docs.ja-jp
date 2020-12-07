---
title: tempdb データベース | Microsoft Docs
description: このトピックでは、SQL Server と Azure SQL Database で tempdb データベースを構成し、使用する方法について説明します。
ms.custom: P360
ms.date: 09/16/2020
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c49e89d9ed81950d0c8781d39c57eef3e408482b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195559"
---
# <a name="tempdb-database"></a>tempdb データベース

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`tempdb` システム データベースは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスまたは Azure SQL Database に接続しているすべてのユーザーが使用できるグローバル リソースです。 `tempdb` には、次のものが保持されています。  
  
- 明示的に作成された一時的な "*ユーザー オブジェクト*"。 グローバルまたはローカルな一時テーブルおよびインデックス、一時ストアド プロシージャ、テーブル変数、テーブル値関数で返されるテーブル、カーソルなどが含まれます。  
- データベース エンジンによって作成された "*内部オブジェクト*"。 それには以下が含まれます。
  - スプール、カーソル、並べ替え、および一時的なラージ オブジェクト (LOB) 記憶域の中間結果を格納する作業テーブル。
  - ハッシュ結合操作またはハッシュ集計操作用の作業ファイル
  - インデックスの作成または再構築などの操作 (`SORT_IN_TEMPDB` が指定されている場合) や、`GROUP BY`、`ORDER BY`、`UNION` などの特定のクエリにおける、並べ替えの中間結果。

  各内部オブジェクトでは、少なくとも 9 つのページが使用されます (IAM ページと 8 ページ分のエクステント)。 ページとエクステントの詳細については、「[ページとエクステント](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents)」を参照してください。

  > [!IMPORTANT]
  > `tempdb` に保存され、データベース レベルまで調べられるグローバル一時テーブルとグローバル一時ストアド プロシージャは、Azure SQL Database 単一データベースおよびエラスティック プールによってサポートされています。 
  >
  > グローバル一時テーブルとグローバル一時ストアド プロシージャは、同じ SQL データベース内のすべてのユーザーのセッションで共有されます。 他の SQL データベースからのユーザー セッションは、グローバル一時テーブルにアクセスできません。 詳細については、「[Database scoped global temporary tables (Azure SQL Database)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database)」(データベース スコープ グローバル一時テーブル (Azure SQL Database)) を参照してください。 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) では、SQL Server と同じ一時オブジェクトがサポートされます。
  >
  > Azure SQL Database の単一データベースとエラスティック プールでは、master データベースと `tempdb` データベースのみが適用されます。 詳細については、[Azure SQL Database サーバーの概要](/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server)に関する記事を参照してください。 Azure SQL Database の単一データベースとエラスティック プールのコンテキストでの `tempdb` については、[Azure SQL Database の単一データベースとエラスティック プールでの tempdb データベース](#tempdb-database-in-sql-database)に関する説明を参照してください。 
  >
  > Azure SQL Managed Instance の場合、すべてのシステム データベースが適用されます。

- "*バージョン ストア*"。これは行のバージョン管理のための機能をサポートするデータ行が保持されるデータ ページのコレクションです。 共通バージョン ストアとオンライン インデックス ビルド バージョン ストアの 2 種類があります。 バージョン ストアに保持される内容:
  - 行バージョン管理分離トランザクションまたはスナップショット分離トランザクションを通して `READ COMMITTED` を使用するデータベース内のデータ変更トランザクションによって生成される行バージョン。  
  - オンライン インデックス操作、複数のアクティブな結果セット (MARS)、`AFTER` トリガーなどの機能に対するデータ変更トランザクションによって生成される行バージョン。  
  
トランザクションをロールバックできるように、`tempdb` での操作のログ記録は最小限に抑えられます。 `tempdb` は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動されるたびに再作成され、システムが常にデータベースのクリーンなコピーで起動されるようにします。 一時テーブルと一時ストアド プロシージャは、切断時に自動的に削除され、システムのシャットダウン時にアクティブな接続はありません。 

`tempdb` には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のあるセッションから別のセッションに保存されるものは何もありません。 `tempdb` では、バックアップおよび復元の操作は実行できません。  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>SQL Server での tempdb の物理プロパティ

次の表は、SQL Server での `tempdb` のデータ ファイルとログ ファイルの初期構成値の一覧です。 値は、`model` データベースの既定値に基づいています。 これらのファイルのサイズは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションによって多少異なる場合があります。  
  
|ファイル|論理名|物理名|初期サイズ|ファイル拡張|  
|----------|------------------|-------------------|------------------|-----------------|  
|プライマリ データ|tempdev|tempdb.mdf|8 MB|ディスクがいっぱいになるまで 64 MB ずつ自動拡張|  
|セカンダリ データ ファイル|temp#|tempdb_mssql_#.ndf|8 MB|ディスクがいっぱいになるまで 64 MB ずつ自動拡張|  
|ログ|templog|templog.ldf|8 MB|最大 2 TB まで 64 MB ずつ自動拡張|  
  
セカンダリ データ ファイルの数は、コンピューター上の (論理) プロセッサの数に依存します。 一般的なルールとして、論理プロセッサの数が 8 以下の場合、論理プロセッサと同じ数のデータ ファイルを使用します。 論理プロセッサの数が 8 より多い場合は、8 つのデータ ファイルが使用されます。 そのとき、競合が続く場合は、競合が許容できるレベルに低下するまでデータ ファイルの数を 4 の倍数分ずつ増やすか、ワークロードまたはコードを変更します。

> [!NOTE]
> データ ファイルの数の既定値は、 [KB 2154845](https://support.microsoft.com/kb/2154845/)の一般的なガイドラインに基づいています。  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>SQL Server の tempdb のデータ ファイルとログ ファイルの移動

`tempdb` のデータ ファイルとログ ファイルを移動するには、「[システム データベースの移動](../../relational-databases/databases/move-system-databases.md)」を参照してください。  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>SQL Server での tempdb のデータベース オプション

`tempdb` データベースの各データベース オプションの既定値とそのオプションを変更できるかどうかを次の表に示します。 これらのオプションの現在の設定を表示するには、 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューを使用します。  
  
|データベース オプション|既定値|変更可否|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|はい|  
|ANSI_NULL_DEFAULT|OFF|はい|  
|ANSI_NULLS|OFF|はい|  
|ANSI_PADDING|OFF|はい|  
|ANSI_WARNINGS|OFF|はい|  
|ARITHABORT|OFF|はい|  
|AUTO_CLOSE|OFF|いいえ|  
|AUTO_CREATE_STATISTICS|ON|はい|  
|AUTO_SHRINK|OFF|いいえ|  
|AUTO_UPDATE_STATISTICS|ON|はい|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|はい|  
|CHANGE_TRACKING|OFF|いいえ|  
|CONCAT_NULL_YIELDS_NULL|OFF|はい|  
|CURSOR_CLOSE_ON_COMMIT|OFF|はい|  
|CURSOR_DEFAULT|GLOBAL|はい|  
|データベース可用性オプション|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|いいえ<br /><br /> いいえ<br /><br /> いいえ|  
|DATE_CORRELATION_OPTIMIZATION|OFF|はい|  
|DB_CHAINING|ON|いいえ|  
|ENCRYPTION|OFF|いいえ|  
|MIXED_PAGE_ALLOCATION|OFF|いいえ|  
|NUMERIC_ROUNDABORT|OFF|はい|  
|PAGE_VERIFY|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新規インストールの場合は CHECKSUM<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレードの場合は NONE|はい|  
|PARAMETERIZATION|SIMPLE|はい|  
|QUOTED_IDENTIFIER|OFF|はい|  
|READ_COMMITTED_SNAPSHOT|OFF|いいえ|  
|RECOVERY|SIMPLE|いいえ|  
|RECURSIVE_TRIGGERS|OFF|はい|  
|Service Broker のオプション|ENABLE_BROKER|はい|  
|TRUSTWORTHY|OFF|いいえ|  
  
これらのデータベース オプションの説明は、「[ALTER DATABASE の SET オプション (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
## <a name="tempdb-database-in-sql-database"></a>SQL Database の tempdb データベース

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>DTU に基づくサービス層の tempdb のサイズ

<!-- tempdb being larger for Basic and 50 eDTU pools than for 100-400 eDTU pools reflects actual config (historical reasons) --> 

|サービス レベルの目標|`tempdb` の最大データ ファイル サイズ (GB)|`tempdb` のデータ ファイルの数|`tempdb` の最大データ サイズ (GB)|
|---|---:|---:|---:|
|Basic|13.9|1|13.9|
|S0|13.9|1|13.9|
|S1|13.9|1|13.9|
|S2|13.9|1|13.9|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13.9|12|166.7|
|P2|13.9|12|166.7|
|P4|13.9|12|166.7|
|P6|13.9|12|166.7|
|P11|13.9|12|166.7|
|P15|13.9|12|166.7|
|Basic エラスティック プール (すべての DTU 構成)|13.9|12|166.7|
|Standard エラスティック プール (50 eDTU)|13.9|12|166.7|
|Standard エラスティック プール (100 eDTU)|32|1|32|
|Standard エラスティック プール (200 eDTU)|32|2|64|
|Standard エラスティック プール (300 eDTU)|32|3|96|
|Standard エラスティック プール (400 eDTU)|32|3|96|
|Standard エラスティック プール (800 eDTU)|32|6|192|
|Standard エラスティック プール (1200 eDTU)|32|10|320|
|Standard エラスティック プール (1600-3000 eDTU)|32|12|384|
|Premium エラスティック プール (すべての DTU 構成)|13.9|12|166.7|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>vCore に基づくサービス層の tempdb のサイズ

[仮想コア ベースのリソース制限](/azure/sql-database/sql-database-vcore-resource-limits)に関する記事を参照してください。

## <a name="restrictions"></a>制限事項

`tempdb` データベースでは、次の操作を実行できません。  
  
- ファイル グループの追加。
- データベースのバックアップまたは復元。
- 照合順序の変更。 既定の照合順序はサーバーの照合順序です。
- データベース所有者の変更。 `tempdb` は *sa* によって所有されます。
- データベース スナップショットの作成。
- データベースの削除。
- データベースからの *guest* ユーザーの削除。
- 変更データ キャプチャの有効化。
- データベース ミラーリングへの参加。
- プライマリ ファイル グループ、プライマリ データ ファイル、またはログ ファイルの削除。
- データベース名またはプライマリ ファイル グループ名の変更。
- `DBCC CHECKALLOC` の実行。
- `DBCC CHECKCATALOG` の実行。
- データベースの `OFFLINE` への設定。
- データベースまたはプライマリ ファイル グループの `READ_ONLY` への設定。
  
## <a name="permissions"></a>アクセス許可

すべてのユーザーが `tempdb` 内に一時オブジェクトを作成できます。 ユーザーは追加の権限を付与されない限り、自分で作成したオブジェクトにしかアクセスできません。 `tempdb` に対する接続アクセス許可を取り消して、ユーザーが `tempdb` を使用できないようにすることができます。 一部のルーチン操作で `tempdb` を使用する必要があるため、それはお勧めしません。  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>SQL Server の tempdb のパフォーマンスの最適化
`tempdb` データベースのサイズと物理的な配置場所は、システムのパフォーマンスに影響を与えることがあります。 たとえば、`tempdb` に対して定義されているサイズが小さすぎる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが再起動されるたびに、`tempdb` をワークロードのサポートに必要なサイズまで自動的に拡張することに、システム処理の負荷の一部が占有される可能性があります。

可能な場合は、[ファイルの瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)を使用して、データ ファイルの拡張操作のパフォーマンスを向上させます。

すべての `tempdb` ファイルに対する領域をあらかじめ割り当てるには、環境における一般的なワークロードに十分に対応できる大きさの値にファイル サイズを設定します。 事前に割り当てておけば、`tempdb` は頻繁に拡張されず、パフォーマンスに影響が出なくなります。 `tempdb` データベースは、想定外の例外に対してディスク領域が増加するよう、自動拡張が行われるように設定する必要があります。

データ ファイルのサイズは、各[ファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md#filegroups)内で等しくする必要があります。これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、より多くの空き領域を持つファイル内の割り当てを優先する比例配分アルゴリズムが使用されているためです。 サイズの等しい複数のデータ ファイルに `tempdb` を分割すると、`tempdb` を使用する操作において効率の高い並列処理を実現できます。

`tempdb` データベース ファイルの拡張単位が小さすぎることのないように、ファイル拡張の増分値を妥当なサイズに設定します。 `tempdb` に書き込まれるデータ量と比較してファイルの拡張単位が小さすぎると、`tempdb` を頻繁に拡張することが必要になる場合があります。 それにより、パフォーマンスが影響を受けます。

`tempdb` の現在のサイズと拡張パラメーターを確認するには、次のクエリを使用します。

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

高速な I/O サブシステムに `tempdb` データベースを配置します。 直接アタッチされたディスクが多数ある場合は、ディスク ストライピングを使用します。 I/O ボトルネックも発生しているのでない限り、個々の `tempdb` データ ファイルまたはそのグループを、異なるディスクまたはスピンドルに配置する必要は必ずしもありません。

ユーザー データベースによって使用されるものとは異なるディスクに、`tempdb` データベースを配置します。

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>SQL Server の tempdb でのパフォーマンスの強化
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、`tempdb` のパフォーマンスが次の方法でさらに最適化されています。  
  
- 一時テーブルとテーブル変数はキャッシュされます。 キャッシュを使用することで、一時オブジェクトを削除および作成する操作を非常に高速に実行できます。 また、キャッシュによって、ページの割り当てやメタデータの競合も減少します。  
- 割り当てページ ラッチ プロトコルが改善され、使用される `UP` (更新) ラッチの回数が減っています。  
- `tempdb` のログ記録オーバーヘッドが減少し、`tempdb` ログ ファイルのディスク I/O 帯域幅消費が減少しました。  
- セットアップによって、新しいインスタンスのインストール中に複数の `tempdb` データ ファイルが追加されます。 このタスクを実行するには、 **[データベース エンジンの構成]** セクションの新しい UI 入力コントロールと、コマンド ライン パラメーター `/SQLTEMPDBFILECOUNT` を使用します。 既定では、セットアップ時に、論理プロセッサ数または 8 のいずれか小さい方と同数の `tempdb` データ ファイルが追加されます。  
- 複数の `tempdb` データ ファイルがある場合は、拡張設定に応じて、すべてのファイルが同時に同量ずつ自動拡張されます。 [トレース フラグ 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) は必須ではなくなりました。  
- `tempdb` 内のすべての割り当てで単一エクステントが使用されます。 [トレース フラグ 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) は必須ではなくなりました。  
- プライマリ ファイル グループの場合、`AUTOGROW_ALL_FILES` プロパティはオンにされており、プロパティは変更できません。

`tempdb` でのパフォーマンス向上の詳細については、[TEMPDB - ファイルとトレース フラグと更新](/archive/blogs/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my)に関するブログ記事を参照してください。

## <a name="memory-optimized-tempdb-metadata"></a>メモリ最適化 tempdb メタデータ
`tempdb` でのメタデータの競合は、従来、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上で実行されている多くのワークロードのスケーラビリティに対するボトルネックになっていました。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、[メモリ内データベース](../in-memory-database.md)機能ファミリの一部として、メモリ最適化 tempdb メタデータという新機能が導入されています。 

この機能により、このボトルネックが実質的に除去され、tempdb の負荷が高いワークロードに新しいレベルのスケーラビリティが提供されます。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、一時テーブルのメタデータの管理に関連するシステム テーブルを、ラッチ フリーの非持続的メモリ最適化テーブルに移動できます。

メモリ最適化 tempdb メタデータを使用する方法とそのタイミングの概要については、この 7 分間のビデオをご覧ください。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-and-When-To-Memory-Optimized-TempDB-Metadata/player?WT.mc_id=dataexposed-c9-niner]


### <a name="configuring-and-using-memory-optimized-tempdb-metadata"></a>メモリ最適化 tempdb メタデータの構成と使用

この新しい機能にオプトインするには、次のスクリプトを使用します。

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON;
```

この構成の変更を有効にするには、サービスの再起動が必要です。

次の T-SQL コマンドを使用して、`tempdb` がメモリ最適化かどうかを確認できます。

```sql
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized');
```

メモリ最適化 `tempdb` メタデータを有効にした後に、何らかの理由でサーバーの起動に失敗した場合は、 **-f** スタートアップ オプションを使用して[最小構成](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)で SQL Server インスタンスを開始することで、この機能を回避できます。 その後、この機能を無効にして、通常モードで SQL Server を再起動できます。

サーバーを潜在的なメモリ不足の状態から保護するために、`tempdb` を[リソース プール](../in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)にバインドすることができます。 これは、リソース プールをデータベースにバインドするために通常実行する手順の代わりに [`ALTER SERVER`](../../t-sql/statements/alter-server-configuration-transact-sql.md) コマンドを使用して行います。

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON (RESOURCE_POOL = 'pool_name');
```

メモリ最適化 tempdb メタデータが既に有効になっている場合でも、この変更を有効にするには再起動も必要です。

### <a name="memory-optimized-tempdb-limitations"></a>メモリ最適化 tempdb メタデータの制限

- 機能のオンとオフの切り替えは、動的ではありません。 `tempdb` の構造を根本的に変更する必要があるため、この機能を有効または無効にするには再起動が必要です。

- 1 つのトランザクションで複数のデータベース内のメモリ最適化テーブルにアクセスすることはできません。 ユーザー データベース内のメモリ最適化テーブルを使用するトランザクションでは、同じトランザクション内で `tempdb` システム ビューにアクセスすることはできません。 ユーザー データベース内のメモリ最適化テーブルと同じトランザクションで `tempdb` システム ビューにアクセスしようとした場合、次のエラーが返されます。
    
  ```
  A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
  ```
    
  例:
    
  ```sql
  BEGIN TRAN;
  
  SELECT *
  FROM tempdb.sys.tables;  -----> Creates a user in-memory OLTP transaction in tempdb
  
  INSERT INTO <user database>.<schema>.<mem-optimized table>
  VALUES (1); ----> Tries to create a user in-memory OLTP transaction in the user database but will fail
  
  COMMIT TRAN;
  ```
    
- メモリ最適化テーブルに対するクエリではロックと分離のヒントがサポートされていないため、メモリ最適化 `tempdb` カタログ ビューに対するクエリでは、ロックと分離のヒントは適用されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の他のシステム カタログ ビューと同じように、システム ビューに対するすべてのトランザクションは、`READ COMMITTED` (または、このケースでは `READ COMMITTED SNAPSHOT`) の分離になります。

- メモリ最適化 `tempdb` メタデータが有効になっている場合、一時テーブルに[列ストア インデックス](../indexes/columnstore-indexes-overview.md)を作成することはできません。

- 列ストア インデックスでの制限により、メモリ最適化 `tempdb` メタデータが有効になっている場合は、`COLUMNSTORE` または `COLUMNSTORE_ARCHIVE` データ圧縮パラメーターを指定して `sp_estimate_data_compression_savings` システム ストアド プロシージャを使用することはできません。

> [!NOTE] 
> これらの制限は、`tempdb` システム ビューを参照している場合にのみ適用されます。 必要に応じて、ユーザー データベース内のメモリ最適化テーブルにアクセスするときに、同じトランザクションで一時テーブルを作成できます。

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>SQL Server での tempdb の容量計画
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 運用環境での `tempdb` の適切なサイズを判断するには、多くの要因が関係します。 前に説明したように、これらの要因には既存のワークロードや使用されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能などがあります。 SQL Server のテスト環境で次のタスクを実行して、既存のワークロードを分析することをお勧めします。

- `tempdb` に自動拡張を設定する。
- 個々のクエリまたはワークロード トレース ファイルを実行し、`tempdb` 領域の使用を監視する。
- インデックスの再構築などのインデックス メンテナンス操作を実行し、`tempdb` 領域を監視する。
- 前の手順の領域使用の値を使用して、ワークロードの総使用量を予測する。 予測される同時実行アクティビティに対してこの値を調整した後、それに応じて `tempdb` のサイズを設定します。

## <a name="monitoring-tempdb-use"></a>tempdb の使用の監視
`tempdb` のディスク領域が不足すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 運用環境で重大な中断が発生する可能性があります。 また、実行中のアプリケーションが操作を完了できなくなる場合もあります。 [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 動的管理ビューを使用して、`tempdb` ファイルで使用されているディスク領域を監視できます。

```sql
 -- Determining the amount of free space in tempdb
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by the version store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by internal objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the amount of space used by user objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

`tempdb` でのページの割り当てや割り当て解除のアクティビティをセッションまたはタスク レベルで監視するには、[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) および [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md) 動的管理ビューを使用できます。 これらのビューを使用すると、`tempdb` のディスク領域を大量に使用している大きなクエリ、一時テーブル、またはテーブル変数を特定できます。 また、いくつかのカウンターを使用して、`tempdb` で使用できる空き領域と、`tempdb` を使用しているリソースを監視することもできます。

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>関連コンテンツ
[インデックスの SORT_IN_TEMPDB オプション](../../relational-databases/indexes/sort-in-TempDB-option-for-indexes.md)    
[システム データベース](../../relational-databases/databases/system-databases.md)    
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)    
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)    
[データベース ファイルの移動](../../relational-databases/databases/move-database-files.md)    
