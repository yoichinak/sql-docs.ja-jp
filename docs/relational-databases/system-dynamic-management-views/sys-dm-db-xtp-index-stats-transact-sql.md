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
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0916891a629298602c274d4cf787e6bd9e1a8a9f
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099914"
---
# <a name="sysdm_db_xtp_index_stats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  前回データベースが再起動されてから収集された統計が含まれます。  
  
 詳細については、「 [インメモリ OLTP &#40;In-Memory の最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) 」と [Memory-Optimized テーブルでのインデックスの使用に関するガイドライン](/previous-versions/sql/sql-server-2016/dn133166(v=sql.130))を参照してください。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|このインデックスが所属するオブジェクトの ID。|  
|xtp_object_id|**bigint**|オブジェクトの現在のバージョンに対応する内部 ID。<br /><br /> 注: に適用さ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] れます。|  
|index_id|**bigint**|インデックスの ID。 index_id は、オブジェクト内でのみ一意です。|  
|scans_started|**bigint**|実行されたインメモリ OLTP のインデックス スキャンの回数。 すべての select、insert、update、または delete には、インデックススキャンが必要です。|  
|scans_retries|**bigint**|再試行が必要なインデックススキャンの数。|  
|rows_returned|**bigint**|テーブルが作成された後、またはが開始されてから返された、累積行数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|rows_touched|**bigint**|テーブルの作成以降にアクセスされた行の累積数またはの先頭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|rows_expiring|**bigint**|内部使用のみ。|  
|rows_expired|**bigint**|内部使用のみ。|  
|rows_expired_removed|**bigint**|内部使用のみ。|  
|phantom_scans_started|**bigint**|内部使用のみ。|  
|phatom_scans_retries|**bigint**|内部使用のみ。|  
|phantom_rows_touched|**bigint**|内部使用のみ。|  
|phantom_expiring_rows_encountered|**bigint**|内部使用のみ。|  
|phantom_expired_rows_encountered|**bigint**|内部使用のみ。|  
|phantom_expired_removed_rows_encountered|**bigint**|内部使用のみ。|  
|phantom_expired_rows_removed|**bigint**|内部使用のみ。|  
|object_address|**varbinary (8)**|内部使用のみ。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
