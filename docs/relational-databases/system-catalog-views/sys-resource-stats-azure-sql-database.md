---
description: sys.resource_stats (Azure SQL データベース)
title: sys.resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: eea603b089c93b86b92ac39a22d0c6e9c64b49d9
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91807021"
---
# <a name="sysresource_stats-azure-sql-database"></a>sys.resource_stats (Azure SQL データベース)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Azure SQL Database の CPU 使用率とストレージ データを返します。 データは、5 分間隔で収集と集計が実行されます。 各ユーザーデータベースには、5分間のレポートウィンドウごとに1行のデータがあり、リソースの消費量が変化します。 返されるデータには、CPU 使用率、ストレージサイズの変更、およびデータベース SKU の変更が含まれます。 変更のないアイドル状態のデータベースは、5分間隔で行を保持できません。 履歴データは約 14 日間保持されます。  
  
 **Sys.resource_stats**ビューの定義は、データベースが関連付けられている Azure SQL Database サーバーのバージョンによって異なります。 新しいサーバーバージョンにアップグレードするときに、これらの違いとアプリケーションで必要な変更を検討してください。  
  
 次の表では、v12 サーバーで使用できる列について説明します。  
  
|[列]|データ型|説明|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|5分間のレポート間隔の開始を示す UTC 時刻。|  
|end_time|**datetime**|5分間のレポート間隔の終了を示す UTC 時刻。|  
|database_name|**nvarchar(128)**|ユーザーデータベースの名前。|  
|sku|**nvarchar(128)**|データベースのサービス階層。 使用できる値を次に示します。<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />General Purpose<br /><br />Business Critical|  
|storage_in_megabytes|**float**|データベースデータ、インデックス、ストアドプロシージャ、およびメタデータを含む、期間の最大ストレージサイズ (mb)。|  
|avg_cpu_percent|**decimal (5, 2)**|サービス層の制限に対する割合での平均コンピューティング使用率。|  
|avg_data_io_percent|**decimal (5, 2)**|サービス層の制限に基づく平均 i/o 使用率 (%)。 Hyperscale データベースについては、「 [リソース使用率の統計情報のデータ IO](/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)」を参照してください。|  
|avg_log_write_percent|**decimal (5, 2)**|サービス層の上限に対するパーセンテージで示した、平均書き込みリソース使用率。|  
|max_worker_percent|**decimal (5, 2)**|データベースのサービスレベルの上限に基づく割合の最大同時実行ワーカー (要求)。<br /><br /> 現在、最大値は、同時実行ワーカー数の15秒のサンプルに基づいて、5分間隔で計算されます。|  
|max_session_percent|**decimal (5, 2)**|データベースのサービス階層の上限に基づく割合の最大同時セッション数。<br /><br /> 現在、最大値は、同時セッション数の15秒のサンプルに基づいて、5分間隔で計算されます。|  
|dtu_limit|**int**|この期間中のこのデータベースの現在の最大データベース DTU 設定です。 |
|xtp_storage_percent|**decimal (5, 2)**|サービス層の制限 (レポート間隔の終了時) に対するインメモリ OLTP のストレージ使用率。 これには、メモリ最適化テーブル、インデックス、およびテーブル変数の、次のインメモリ OLTP オブジェクトのストレージに使用されるメモリが含まれます。 また、ALTER TABLE 操作の処理に使用されるメモリも含まれています。<br /><br /> インメモリ OLTP がデータベースで使用されていない場合は0を返します。|
|avg_login_rate_percent|**decimal (5, 2)**|単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。|
|avg_instance_cpu_percent|**decimal (5, 2)**|SQL Database プロセスに対する平均データベース CPU 使用率 (%)。|
|avg_instance_memory_percent|**decimal (5, 2)**|平均データベースメモリ使用量を SQL Database プロセスに対する割合として計算します。|
|cpu_limit|**decimal (5, 2)**|この期間中のこのデータベースの仮想コア数。 DTU ベースのモデルを使用しているデータベースの場合、この列は NULL になります。|
|allocated_storage_in_megabytes|**float**|データベースデータを格納するために使用できる、フォーマットされたファイル領域のサイズ (MB)。 フォーマットされたファイル領域は、割り当てられたデータ領域とも呼ばれます。  詳細については、「 [SQL Database でのファイル領域管理](/azure/sql-database/sql-database-file-space-management)」を参照してください。|
  
> [!TIP]  
>  これらの制限とサービスレベルの詳細については、「 [サービスレベル](/azure/azure-sql/database/purchasing-models)」を参照してください。  
    
## <a name="permissions"></a>アクセス許可  
 このビューは、仮想 **master** データベースに接続するためのアクセス許可を持つすべてのユーザーロールで使用できます。  
  
## <a name="remarks"></a>注釈  
 **Sys.resource_stats**によって返されるデータは、実行しているサービス階層/パフォーマンスレベルに対して許容される最大制限の割合として表されます。  
  
 データベースがエラスティックプールのメンバーである場合、パーセント値として表示されるリソース統計は、エラスティックプール構成で設定されたデータベースの上限に対する比率として表されます。  
  
 このデータをより詳細に表示するには、ユーザーデータベースで **sys.dm_db_resource_stats** 動的管理ビューを使用します。 このビューでは、15秒ごとにデータをキャプチャし、1時間の履歴データを保持します。  詳細については、「 [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)」を参照してください。  

## <a name="examples"></a>例  
 次の例では、過去1週間のコンピューティング使用率の平均が80% 以上のすべてのデータベースを返します。  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>参照  
 [サービスレベル](/azure/azure-sql/database/purchasing-models)   
 [サービス層の機能と制限](/azure/azure-sql/database/performance-guidance)  
  
