---
description: sys.dm_user_db_resource_governance (Transact-sql)
title: sys.dm_user_db_resource_governance (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 2038883693288a75f9e2dbe17d80b6b9c7474343
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753728"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-sql)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

現在のデータベースまたはエラスティック プールのリソース ガバナンス メカニズムによって使用されている実際の構成と容量の設定が返されます。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|INT|データベースの ID。 Azure SQL Database サーバー内で一意です。|
|**logical_database_guid**|UNIQUEIDENTIFIER|ユーザーデータベースの有効期間を経ているユーザーデータベースの論理 GUID。  データベースの名前を変更したり、サービスレベル目標を変更しても、この値は変わりません。|
|**physical_database_guid**|UNIQUEIDENTIFIER|ユーザーデータベースの物理インスタンスが存続しているユーザーデータベースの物理 GUID。 データベースのサービスレベル目標を変更すると、この値が変更されます。|
|**server_name**|nvarchar|論理サーバー名。|
|**database_name**|nvarchar|論理データベース名。|
|**slo_name**|nvarchar|ハードウェアの生成を含むサービスレベル目標。|
|**dtu_limit**|INT|データベースの DTU 制限 (vCore の場合は NULL)。|
|**cpu_limit**|INT|データベースの vCore の制限 (DTU データベースの場合は NULL)。|
|**min_cpu**|tinyint|ユーザーワークロードリソースプールの MIN_CPU_PERCENT 値。 「 [リソースプールの概念](../resource-governor/resource-governor-resource-pool.md#resource-pool-concepts)」を参照してください。|
|**max_cpu**|tinyint|ユーザーワークロードリソースプールの MAX_CPU_PERCENT 値。 「 [リソースプールの概念](../resource-governor/resource-governor-resource-pool.md#resource-pool-concepts)」を参照してください。|
|**cap_cpu**|tinyint|ユーザーワークロードリソースプールの CAP_CPU_PERCENT 値。 「 [リソースプールの概念](../resource-governor/resource-governor-resource-pool.md#resource-pool-concepts)」を参照してください。|
|**min_cores**|smallint|内部使用のみです。|
|**max_dop**|smallint|ユーザーワークロードグループの MAX_DOP 値。 「 [ワークロードグループの作成](../../t-sql/statements/create-workload-group-transact-sql.md)」を参照してください。|
|**min_memory**|INT|ユーザーワークロードリソースプールの MIN_MEMORY_PERCENT 値。 「 [リソースプールの概念](../resource-governor/resource-governor-resource-pool.md#resource-pool-concepts)」を参照してください。|
|**max_memory**|INT|ユーザーワークロードリソースプールの MAX_MEMORY_PERCENT 値。 「 [リソースプールの概念](../resource-governor/resource-governor-resource-pool.md#resource-pool-concepts)」を参照してください。|
|**max_sessions**|INT|ユーザーワークロードグループで許可されているセッションの最大数。|
|**max_memory_grant**|INT|ユーザーワークロードグループの REQUEST_MAX_MEMORY_GRANT_PERCENT 値。 「 [ワークロードグループの作成](../../t-sql/statements/create-workload-group-transact-sql.md)」を参照してください。|
|**max_db_memory**|INT|内部使用のみです。|
|**govern_background_io**|bit|内部使用のみです。|
|**min_db_max_size_in_mb**|bigint|データファイルの最小 max_size 値 (MB 単位)。 「 [Sys.database_files](../system-catalog-views/sys-database-files-transact-sql.md)」を参照してください。|
|**max_db_max_size_in_mb**|bigint|データファイルの最大 max_size 値 (MB 単位)。 「 [Sys.database_files](../system-catalog-views/sys-database-files-transact-sql.md)」を参照してください。|
|**default_db_max_size_in_mb**|bigint|データファイルの既定の max_size 値 (MB 単位)。 「 [Sys.database_files](../system-catalog-views/sys-database-files-transact-sql.md)」を参照してください。|
|**db_file_growth_in_mb**|bigint|データファイルの既定の拡張増分値 (MB 単位)。 「 [Sys.database_files](../system-catalog-views/sys-database-files-transact-sql.md)」を参照してください。|
|**initial_db_file_size_in_mb**|bigint|新しいデータファイルの既定のサイズ (MB 単位)。 「 [Sys.database_files](../system-catalog-views/sys-database-files-transact-sql.md)」を参照してください。|
|**log_size_in_mb**|bigint|新しいログファイルの既定のサイズ (MB 単位)。 「 [Sys.database_files](../system-catalog-views/sys-database-files-transact-sql.md)」を参照してください。|
|**instance_cap_cpu**|INT|内部使用のみです。|
|**instance_max_log_rate**|bigint|SQL Server インスタンスのログ生成率の制限 (バイト/秒)。 などのシステムデータベースを含め、インスタンスによって生成されたすべてのログに適用され `tempdb` ます。 エラスティックプールでは、はプール内のすべてのデータベースによって生成されるログに適用されます。|
|**instance_max_worker_threads**|INT|SQL Server インスタンスのワーカースレッドの制限。|
|**replica_type**|INT|レプリカの種類。ここで、0はプライマリ、1はセカンダリです。|
|**max_transaction_size**|bigint|任意のトランザクションで使用される最大ログ領域 (KB 単位)。|
|**checkpoint_rate_mbps**|INT|内部使用のみです。|
|**checkpoint_rate_io**|INT|内部使用のみです。|
|**last_updated_date_utc**|DATETIME|最終設定変更または再構成の日付と時刻 (UTC)。|
|**primary_group_id**|INT|プライマリレプリカとセカンダリレプリカでのユーザーワークロードのワークロードグループ ID。|
|**primary_group_max_workers**|INT|ユーザーワークロードグループのワーカースレッドの制限。|
|**primary_min_log_rate**|bigint|ユーザーワークロードグループレベルでの1秒あたりの最小ログ速度 (バイト単位)。 リソースガバナンスでは、この値を下回るログレートが減少しません。|
|**primary_max_log_rate**|bigint|ユーザーワークロードグループレベルでの1秒あたりの最大ログ速度 (バイト単位)。 リソースガバナンスでは、この値を超えるログレートは許可されません。|
|**primary_group_min_io**|INT|ユーザーワークロードグループの最小 IOPS。 リソースガバナンスでは、この値を下回る IOPS の削減は試行されません。|
|**primary_group_max_io**|INT|ユーザーワークロードグループの最大 IOPS。 リソースガバナンスでは、この値を超える IOPS は許可されません。|
|**primary_group_min_cpu**|float|ユーザーワークロードグループレベルの最小 CPU%。 リソースガバナンスでは、この値を下回る CPU 使用率の削減は試行されません。|
|**primary_group_max_cpu**|float|ユーザーワークロードグループレベルの最大 CPU%。 リソースガバナンスでは、この値を超える CPU 使用は許可されません。|
|**primary_log_commit_fee**|INT|ユーザーワークロードグループのログレートガバナンスコミット料金 (バイト単位)。 コミット料金では、ログレートのアカウンティングのみを目的として、各ログ IO のサイズが固定値で増加します。 ストレージへの実際のログ IO が増加していません。|
|**primary_pool_max_workers**|INT|ユーザーワークロードリソースプールのワーカースレッドの制限。|
|**pool_max_io**|INT|ユーザーワークロードリソースプールの最大 IOPS 制限。|
|**govern_db_memory_in_resource_pool**|bit|内部使用のみです。|
|**volume_local_iops**|INT|内部使用のみです。|
|**volume_managed_xstore_iops**|INT|内部使用のみです。|
|**volume_external_xstore_iops**|INT|内部使用のみです。|
|**volume_type_local_iops**|INT|内部使用のみです。|
|**volume_type_managed_xstore_iops**|INT|内部使用のみです。|
|**volume_type_external_xstore_iops**|INT|内部使用のみです。|
|**volume_pfs_iops**|INT|内部使用のみです。|
|**volume_type_pfs_iops**|INT|内部使用のみです。|
|||

## <a name="permissions"></a>アクセス許可

このビューには、VIEW DATABASE STATE 権限が必要です。

## <a name="remarks"></a>解説

Azure SQL Database でのリソースガバナンスの詳細については、「 [SQL Database リソースの制限](/azure/sql-database/sql-database-resource-limits-database-server)」を参照してください。

> [!IMPORTANT]
> この DMV によって返されるデータの大部分は内部使用を目的としており、いつでも変更される可能性があります。

## <a name="examples"></a>例

次のクエリは、ユーザーデータベースのコンテキストで実行され、ユーザーのワークロードグループとリソースプールレベルでの最大ログ速度と最大 IOPS を返します。 1つのデータベースの場合、1つの行が返されます。 エラスティックプール内のデータベースの場合、プール内の各データベースに対して行が返されます。

```
SELECT database_name,
       primary_group_id,
       primary_max_log_rate,
       primary_group_max_io,
       pool_max_io
FROM sys.dm_user_db_resource_governance
ORDER BY database_name;  
```

## <a name="see-also"></a>参照

- [リソース ガバナー](../resource-governor/resource-governor.md)
- [sys.dm_resource_governor_resource_pools (Transact-sql)](./sys-dm-resource-governor-resource-pools-transact-sql.md)
- [sys.dm_resource_governor_workload_groups (Transact-SQL)](./sys-dm-resource-governor-workload-groups-transact-sql.md)
- [sys.dm_resource_governor_resource_pools_history_ex (Transact-sql)](./sys-dm-resource-governor-resource-pools-history-ex-azure-sql-database.md)
- [sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database)](./sys-dm-resource-governor-workload-groups-history-ex-azure-sql-database.md)
- [トランザクション ログ速度ガバナンス](/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [単一データベースの DTU リソースの制限](/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [単一データベースの仮想コア リソースの制限](/azure/sql-database/sql-database-vcore-resource-limits-single-databases)