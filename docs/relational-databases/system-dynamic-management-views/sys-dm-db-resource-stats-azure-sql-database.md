---
description: sys.dm_db_resource_stats (Azure SQL Database)
title: sys.dm_db_resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 02/27/2020
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 21cef237634891d4795e46f96f63eba701f55852
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91833706"
---
# <a name="sysdm_db_resource_stats-azure-sql-database"></a>sys.dm_db_resource_stats (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  データベースの CPU、i/o、およびメモリの消費量を返し [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ます。 データベースにアクティビティがない場合でも、15 秒ごとに 1 つの行が存在します。 履歴データは約1時間保持されます。  
  
|[列]|データ型|説明|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|UTC 時刻は、現在のレポート間隔の終了を示します。|  
|avg_cpu_percent|**decimal (5, 2)**|サービス層の制限に対する割合での平均コンピューティング使用率。|  
|avg_data_io_percent|**decimal (5, 2)**|サービス層の上限に対する平均データ i/o 使用率 (%)。 Hyperscale データベースについては、「 [リソース使用率の統計情報のデータ IO](/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)」を参照してください。|  
|avg_log_write_percent|**decimal (5, 2)**|サービス層の制限に対する割合としての、平均トランザクションログの書き込み (MBps)。|  
|avg_memory_usage_percent|**decimal (5, 2)**|サービス層の制限に対する平均メモリ使用率 (%)。<br /><br /> これには、バッファープールページに使用されるメモリと、インメモリ OLTP オブジェクトのストレージが含まれます。|  
|xtp_storage_percent|**decimal (5, 2)**|サービス層の制限 (レポート間隔の終了時) に対するインメモリ OLTP のストレージ使用率。 これには、メモリ最適化テーブル、インデックス、およびテーブル変数の、次のインメモリ OLTP オブジェクトのストレージに使用されるメモリが含まれます。 また、ALTER TABLE 操作の処理に使用されるメモリも含まれています。<br /><br /> インメモリ OLTP がデータベースで使用されていない場合は0を返します。|  
|max_worker_percent|**decimal (5, 2)**|データベースのサービス階層の上限に対する割合での最大同時実行ワーカー (要求)。|  
|max_session_percent|**decimal (5, 2)**|データベースのサービス層の上限に対する割合での最大同時セッション数。|  
|dtu_limit|**int**|この期間中のこのデータベースの現在の最大データベース DTU 設定です。 仮想コアベースのモデルを使用しているデータベースの場合、この列は NULL になります。|
|cpu_limit|**decimal (5, 2)**|この期間中のこのデータベースの仮想コア数。 DTU ベースのモデルを使用しているデータベースの場合、この列は NULL になります。|
|avg_instance_cpu_percent|**decimal (5, 2)**|オペレーティングシステムによって測定された、データベースをホストしている SQL Server インスタンスの平均 CPU 使用率。 ユーザーワークロードと内部ワークロードの両方による CPU 使用率が含まれます。|
|avg_instance_memory_percent|**decimal (5, 2)**|オペレーティングシステムによって測定された、データベースをホストしている SQL Server インスタンスのメモリ使用量の平均値。 ユーザーワークロードと内部ワークロードの両方によるメモリ使用率が含まれます。|
|avg_login_rate_percent|**decimal (5, 2)**|単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。|
|replica_role|**int**|現在のレプリカのロールのうち、0がプライマリ、1がセカンダリ、2がフォワーダー (geo セカンダリのプライマリ) であることを表します。 読み取り可能なすべてのセカンダリに ReadOnly インテントを使用して接続すると、"1" と表示されます。 ReadOnly インテントを指定せずに geo セカンダリに接続すると、"2" (フォワーダーに接続) が表示されます。|
|||
  
> [!TIP]  
> これらの制限とサービスレベルの詳細については、「 [サービスレベル](/azure/azure-sql/database/purchasing-models)」、「 [Azure SQL Database でのクエリのパフォーマンスの手動チューニング](/azure/azure-sql/database/performance-guidance)」、および「 [リソースの制限とリソースガバナンスの SQL Database](/azure/sql-database/sql-database-resource-limits-database-server)」を参照してください。
  
## <a name="permissions"></a>アクセス許可
 このビューには、VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>注釈
 **Sys.dm_db_resource_stats**によって返されるデータは、実行しているサービス階層/パフォーマンスレベルに対して許容される最大制限の割合として表されます。
 
 過去60分以内にデータベースが別のサーバーにフェールオーバーされた場合、ビューはそのフェールオーバー以降の時間についてのみデータを返します。  
  
 保有期間が長いこのデータの詳細なビューを表示するには、 **master**データベースの**sys.resource_stats**カタログビューを使用します。 このビューは、5分ごとにデータをキャプチャし、履歴データを14日間保持します。  詳細については、「 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)」を参照してください。  
  
 データベースがエラスティックプールのメンバーである場合、パーセント値として表示されるリソース統計は、エラスティックプール構成で設定されたデータベースの上限に対する比率として表されます。  
  
## <a name="example"></a>例  
  
次の例では、現在接続しているデータベースの最新の時間によって並べ替えられたリソース使用率データを返します。  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 次の例では、過去1時間のユーザーデータベースのパフォーマンスレベルで許容される最大 DTU 制限の割合という観点から、平均 DTU 消費量を示しています。 パフォーマンスレベルは、一定の割合で100% 近くの割合で増やすことを検討してください。  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 次の例では、過去1時間の CPU 使用率、データとログ i/o、およびメモリ使用量の平均値と最大値を返します。  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>参照  
 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md) [サービスレベル](/azure/azure-sql/database/purchasing-models)