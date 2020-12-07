---
description: sys.dm_db_xtp_index_stats (Transact-SQL)
title: sys.dm_db_xtp_index_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3e6cf5401a48623df1a5b0c2338cf9d1c7287231
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91833797"
---
# <a name="sysdm_db_xtp_index_stats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  前回データベースが再起動されてから収集された統計が含まれます。  
  
 詳細については、「イン [メモリ OLTP &#40;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) メモリ最適化テーブルでの [インデックスの使用に関するガイドライン](/previous-versions/sql/sql-server-2016/dn133166(v=sql.130))&#41;」を参照してください。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|このインデックスが所属するオブジェクトの ID。|  
|xtp_object_id|**bigint**|オブジェクトの現在のバージョンに対応する内部 ID。<br /><br /> 注: に適用さ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] れます。|  
|index_id|**bigint**|インデックスの ID。 index_id は、オブジェクト内でのみ一意です。|  
|scans_started|**bigint**|実行されたインメモリ OLTP のインデックス スキャンの回数。 すべての select、insert、update、または delete には、インデックススキャンが必要です。|  
|scans_retries|**bigint**|再試行が必要なインデックススキャンの数。|  
|rows_returned|**bigint**|テーブルが作成された後、またはが開始されてから返された、累積行数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|rows_touched|**bigint**|テーブルの作成以降にアクセスされた行の累積数またはの先頭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|rows_expiring|**bigint**|内部使用のみです。|  
|rows_expired|**bigint**|内部使用のみです。|  
|rows_expired_removed|**bigint**|内部使用のみです。|  
|phantom_scans_started|**bigint**|内部使用のみです。|  
|phatom_scans_retries|**bigint**|内部使用のみです。|  
|phantom_rows_touched|**bigint**|内部使用のみです。|  
|phantom_expiring_rows_encountered|**bigint**|内部使用のみです。|  
|phantom_expired_rows_encountered|**bigint**|内部使用のみです。|  
|phantom_expired_removed_rows_encountered|**bigint**|内部使用のみです。|  
|phantom_expired_rows_removed|**bigint**|内部使用のみです。|  
|object_address|**varbinary (8)**|内部使用のみです。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
