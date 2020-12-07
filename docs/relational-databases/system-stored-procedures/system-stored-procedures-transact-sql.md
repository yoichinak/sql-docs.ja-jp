---
description: システム ストアド プロシージャ (Transact-SQL)
title: システムストアドプロシージャ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.TSQLSysNoExpandPortal.f1
- sql13.TSQLSysNoExpandPortal.f1_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server]
- APIs [SQL Server]
- stored procedures [SQL Server], categories
- system stored procedures [SQL Server], categories
- system stored procedures [SQL Server]
ms.assetid: a5c4d5b8-5a24-4a2d-99b4-d003b546ee3a
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 581ac92066750ac578cf8103383087fddeb01e65
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810299"
---
# <a name="system-stored-procedures-transact-sql"></a>システム ストアド プロシージャ (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、システム ストアド プロシージャを使用して、さまざまな管理操作や情報操作を実行できます。 システム ストアド プロシージャは、次の表に示すカテゴリに分類されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|カテゴリ|説明|  
|--------------|-----------------|  
|[アクティブ Geo レプリケーションのストアドプロシージャ]()|Azure SQL Database でアクティブな Geo レプリケーションの構成を管理するために、を管理するために使用されます|  
|[カタログ ストアド プロシージャ](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|ODBC データ辞書関数を実装し、ODBC アプリケーションを基になるシステムテーブルへの変更から分離するために使用されます。|  
|[変更データ キャプチャ ストアド プロシージャ](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|変更データキャプチャオブジェクトの有効化、無効化、またはレポートに使用されます。|  
|[カーソル ストアド プロシージャ](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|カーソル変数の機能を実装するために使用されます。|  
|[データ コレクター ストアド プロシージャ](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|データコレクターおよび次のコンポーネント (コレクションセット、コレクションアイテム、コレクション型) を操作するために使用します。|  
|[データベース エンジン ストアド プロシージャ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の全般的なメンテナンスに使用します。|  
|[Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|のインスタンス内から電子メール操作を実行するために使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|[データベース メンテナンス プラン ストアド プロシージャ](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|データベースのパフォーマンスの管理に必要な基本のメンテナンス タスクを設定する場合に使用します。|  
|[分散クエリ ストアド プロシージャ](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|分散クエリを実装および管理するために使用します。|  
|[Filestream および FileTable ストアドプロシージャ &#40;Transact-sql&#41;](./filestream-and-filetable-sp-filestream-force-garbage-collection.md)|FILESTREAM 機能および FileTable 機能の構成と管理に使用します。|  
|[ファイアウォールルールのストアドプロシージャ &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|Azure SQL Database ファイアウォールを構成するために使用します。|  
|[フルテキスト検索ストアド プロシージャ](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|フルテキストインデックスの実装とクエリに使用されます。|  
|[汎用拡張ストアド プロシージャ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|さまざまなメンテナンス作業のために、のインスタンスから外部プログラムへのインターフェイスを提供するために使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|[ログ配布ストアド プロシージャ](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|ログ配布構成を構成、変更、および監視するために使用します。|  
|[管理データ ウェアハウスのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|管理データウェアハウスを構成するために使用します。|  
|[OLE オートメーションストアドプロシージャ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|標準バッチ内で使用する標準オートメーションオブジェクトを有効にするために使用され [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。|  
|[ポリシー ベースの管理ストアド プロシージャ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|ポリシー ベースの管理に使用します。|  
|[PolyBase ストアド プロシージャ](./polybase-stored-procedures-sp-polybase-join-group.md)|PolyBase スケールアウトグループのコンピューターを追加または削除します。|  
|[クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|パフォーマンスを調整するために使用します。|  
|[レプリケーションストアドプロシージャ](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|レプリケーションを管理するために使用します。|  
|[セキュリティ ストアド プロシージャ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|セキュリティを管理するために使用されます。|  
|[スナップショットバックアップストアドプロシージャ](./snapshot-backup-sp-delete-backup.md)|FILE_SNAPSHOT バックアップをすべてのスナップショットと共に削除したり、個々のバックアップファイルスナップショットを削除したりする場合に使用します。|  
|[空間インデックスストアドプロシージャ](./spatial-index-stored-procedures-arguments-and-properties.md)|空間インデックスのインデックス作成のパフォーマンスを分析し、改善するために使用されます。|  
|[SQL Server エージェント ストアド プロシージャ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] で、パフォーマンスと利用状況の監視に使用します。|  
|[SQL Server Profiler ストアド プロシージャ](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|スケジュールされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクティビティとイベントドリブンアクティビティを管理するためにエージェントによって使用されます。|  
|[ストアドプロシージャの Stretch Database](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|Stretch データベースを管理するために使用します。|  
|[テンポラルテーブルストアドプロシージャ](./spatial-index-stored-procedures-arguments-and-properties.md)|テンポラルテーブルに使用する|  
|[XML ストアド プロシージャ](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|XML テキストの管理に使用します。|  
  
> [!NOTE]  
>  特に明記されていない限り、すべてのシステムストアドプロシージャは、成功を示す値0を返します。 失敗した場合は、0 以外の値が返されます。  
  
## <a name="api-system-stored-procedures"></a>API システム ストアド プロシージャ  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]ADO、OLE DB、および ODBC アプリケーションに対して実行するユーザーは、このリファレンスで説明されていないシステムストアドプロシージャを使用して、これらのアプリケーションに気付くことがあり [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 これらのストアドプロシージャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client OLE DB プロバイダーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client ODBC ドライバーによって、データベース API の機能を実装するために使用されます。 ユーザー要求を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに伝えるための機能を持っています。 プロバイダーまたはドライバーの内部使用のみを目的としています。 ベースのアプリケーションからの明示的な呼び出し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はサポートされていません。  
  
 Sp_createorphan および sp_droporphans ストアドプロシージャは、ODBC の **ntext**、 **テキスト**、および **イメージ** の処理に使用されます。  
  
 sp_reset_connection ストアド プロシージャは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でトランザクション内のリモート ストアド プロシージャ呼び出しをサポートする場合に使用します。 このストアドプロシージャは、接続が接続プールから再利用された場合に、Audit Login イベントと Audit Logout イベントも発生させます。  
  
 次の表のシステムストアドプロシージャは、のインスタンス内、またはクライアント Api を使用してのみ使用され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一般的なユーザーの使用は想定されていません。 これらは変更される可能性があり、互換性は保証されていません。  
  
 次のストアドプロシージャは、オンラインブックに記載されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
:::row:::
    :::column:::
        sp_catalogs
    :::column-end:::
    :::column:::
        sp_column_privileges
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_ex
    :::column-end:::
    :::column:::
        sp_columns
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_ex
    :::column-end:::
    :::column:::
        sp_databases
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursor
    :::column-end:::
    :::column:::
        sp_cursorclose
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursorexecute
    :::column-end:::
    :::column:::
        sp_cursorfetch
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursoroption
    :::column-end:::
    :::column:::
        sp_cursoropen
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursorprepare
    :::column-end:::
    :::column:::
        sp_cursorprepexec
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursorunprepare
    :::column-end:::
    :::column:::
        sp_execute
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_datatype_info
    :::column-end:::
    :::column:::
        sp_fkeys
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreignkeys
    :::column-end:::
    :::column:::
        sp_indexes
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_pkeys
    :::column-end:::
    :::column:::
        sp_primarykeys
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_prepare
    :::column-end:::
    :::column:::
        sp_prepexec
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_prepexecrpc
    :::column-end:::
    :::column:::
        sp_unprepare
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_server_info
    :::column-end:::
    :::column:::
        sp_special_columns
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_sproc_columns
    :::column-end:::
    :::column:::
        sp_statistics
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges
    :::column-end:::
    :::column:::
        sp_table_privileges_ex
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables
    :::column-end:::
    :::column:::
        sp_tables_ex
    :::column-end:::
:::row-end:::

&nbsp;
  
次のストアドプロシージャは、ドキュメントに記載されていません。  

:::row:::
    :::column:::
        sp_assemblies_rowset
    :::column-end:::
    :::column:::
        sp_assemblies_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_assemblies_rowset2
    :::column-end:::
    :::column:::
        sp_assembly_dependencies_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_assembly_dependencies_rowset_rmt
    :::column-end:::
    :::column:::
        sp_assembly_dependencies_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_bcp_dbcmptlevel
    :::column-end:::
    :::column:::
        sp_catalogs_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_catalogs_rowset;2
    :::column-end:::
    :::column:::
        sp_catalogs_rowset;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_catalogs_rowset_rmt
    :::column-end:::
    :::column:::
        sp_catalogs_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_check_constbytable_rowset
    :::column-end:::
    :::column:::
        sp_check_constbytable_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_check_constbytable_rowset2
    :::column-end:::
    :::column:::
        sp_check_constraints_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_check_constraints_rowset;2
    :::column-end:::
    :::column:::
        sp_check_constraints_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_rowset
    :::column-end:::
    :::column:::
        sp_column_privileges_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_rowset;5
    :::column-end:::
    :::column:::
        sp_column_privileges_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_rowset2
    :::column-end:::
    :::column:::
        sp_columns_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_90_rowset
    :::column-end:::
    :::column:::
        sp_columns_90_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_90_rowset2
    :::column-end:::
    :::column:::
        sp_columns_ex_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_rowset
    :::column-end:::
    :::column:::
        sp_columns_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_rowset;5
    :::column-end:::
    :::column:::
        sp_columns_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_rowset2
    :::column-end:::
    :::column:::
        sp_constr_col_usage_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_datatype_info_90
    :::column-end:::
    :::column:::
        sp_ddopen; 1
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen; 10
    :::column-end:::
    :::column:::
        sp_ddopen;11
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen; 12
    :::column-end:::
    :::column:::
        sp_ddopen;13
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen; 2
    :::column-end:::
    :::column:::
        sp_ddopen; 3
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;4
    :::column-end:::
    :::column:::
        sp_ddopen; 5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;6
    :::column-end:::
    :::column:::
        sp_ddopen;7
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen; 8
    :::column-end:::
    :::column:::
        sp_ddopen;9
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset
    :::column-end:::
    :::column:::
        sp_foreign_keys_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset;3
    :::column-end:::
    :::column:::
        sp_foreign_keys_rowset;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset_rmt
    :::column-end:::
    :::column:::
        sp_foreign_keys_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset3
    :::column-end:::
    :::column:::
        sp_indexes_90_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_90_rowset_rmt
    :::column-end:::
    :::column:::
        sp_indexes_90_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_rowset
    :::column-end:::
    :::column:::
        sp_indexes_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_rowset;5
    :::column-end:::
    :::column:::
        sp_indexes_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_rowset2
    :::column-end:::
    :::column:::
        sp_linkedservers_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_linkedservers_rowset;2
    :::column-end:::
    :::column:::
        sp_linkedservers_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_oledb_database
    :::column-end:::
    :::column:::
        sp_oledb_defdb
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_oledb_deflang
    :::column-end:::
    :::column:::
        sp_oledb_language
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_oledb_ro_usrname
    :::column-end:::
    :::column:::
        sp_primary_keys_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_primary_keys_rowset;2
    :::column-end:::
    :::column:::
        sp_primary_keys_rowset;3
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_primary_keys_rowset;5
    :::column-end:::
    :::column:::
        sp_primary_keys_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_primary_keys_rowset2
    :::column-end:::
    :::column:::
        sp_procedure_params_90_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedure_params_90_rowset2
    :::column-end:::
    :::column:::
        sp_procedure_params_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedure_params_rowset;2
    :::column-end:::
    :::column:::
        sp_procedure_params_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedures_rowset
    :::column-end:::
    :::column:::
        sp_procedures_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedures_rowset2
    :::column-end:::
    :::column:::
        sp_provider_types_90_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_provider_types_rowset
    :::column-end:::
    :::column:::
        sp_schemata_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_schemata_rowset;3
    :::column-end:::
    :::column:::
        sp_special_columns_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_sproc_columns_90
    :::column-end:::
    :::column:::
        sp_statistics_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_statistics_rowset;2
    :::column-end:::
    :::column:::
        sp_statistics_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_stored_procedures
    :::column-end:::
    :::column:::
        sp_table_constraints_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_constraints_rowset;2
    :::column-end:::
    :::column:::
        sp_table_constraints_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges_rowset
    :::column-end:::
    :::column:::
        sp_table_privileges_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges_rowset;5
    :::column-end:::
    :::column:::
        sp_table_privileges_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges_rowset2
    :::column-end:::
    :::column:::
        sp_table_statistics_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_statistics_rowset;2
    :::column-end:::
    :::column:::
        sp_table_statistics2_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tablecollations
    :::column-end:::
    :::column:::
        sp_tablecollations_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_90_rowset
    :::column-end:::
    :::column:::
        sp_tables_info_90_rowset_64
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_90_rowset2
    :::column-end:::
    :::column:::
        sp_tables_info_90_rowset2_64
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_rowset
    :::column-end:::
    :::column:::
        sp_tables_info_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_rowset_64
    :::column-end:::
    :::column:::
        sp_tables_info_rowset_64;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_rowset2
    :::column-end:::
    :::column:::
        sp_tables_info_rowset2_64
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_rowset;2
    :::column-end:::
    :::column:::
        sp_tables_rowset;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_rowset_rmt
    :::column-end:::
    :::column:::
        sp_tables_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_usertypes_rowset
    :::column-end:::
    :::column:::
        sp_usertypes_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_usertypes_rowset2
    :::column-end:::
    :::column:::
        sp_views_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_views_rowset2
    :::column-end:::
    :::column:::
        sp_xml_schema_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_xml_schema_rowset2
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  

## <a name="see-also"></a>参照  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [ストアド プロシージャ &#40;データベース エンジン&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [ストアドプロシージャの実行 &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [ストアドプロシージャの実行](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ストアド プロシージャの実行](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
