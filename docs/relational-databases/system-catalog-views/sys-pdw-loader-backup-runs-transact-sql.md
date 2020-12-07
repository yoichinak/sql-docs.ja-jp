---
description: sys.pdw_loader_backup_runs (Transact-sql)
title: sys.pdw_loader_backup_runs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 31d8ae2e196d116b6e3ff58c23deedc20425fdf5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036985"
---
# <a name="syspdw_loader_backup_runs-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  での実行中および完了したバックアップと復元操作に関する情報、 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] およびでの進行中および完了したバックアップ、復元、および読み込み操作について説明し [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ます。 情報は、システムの再起動の間で永続化します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定のバックアップ、復元、または読み込み実行の一意の識別子。<br /><br /> このビューのキー。||  
|name|**nvarchar (255)**|読み込みの場合は Null です。 バックアップまたは復元のオプションの名前。||  
|submit_time|**datetime**|要求が送信された時刻。||  
|start_time|**datetime**|操作が開始された時刻。||  
|end_time|**datetime**|操作が完了した、失敗した、または取り消された時刻。||  
|total_elapsed_time|**int**|Start_time と現在の時刻の間の経過時間、または完了、取り消し、または失敗した実行の start_time と end_time の間の合計時間。|Total_elapsed_time が整数の最大値 (ミリ秒単位で24.8 日) を超えた場合、オーバーフローによる具体化エラーが発生します。<br /><br /> ミリ秒単位の最大値は24.8 日に相当します。|  
|operation_type|**nvarchar (16)**|読み込みの種類。|' BACKUP '、' LOAD '、' RESTORE '|  
|mode|**nvarchar (16)**|実行の種類内のモードです。|Operation_type =**バックアップ**の場合<br />**記号**<br />**FULL**<br /><br /> Operation_type の場合 = **読み込み**<br />**追記**<br />**直し**<br />**UPSERT**<br /><br /> Operation_type の場合 = **復元**<br />**データベース**<br />**HEADER_ONLY**|  
|database_name|**nvarchar (255)**|この操作のコンテキストであるデータベースの名前||  
|table_name|**nvarchar (255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|操作を要求しているユーザーの ID。||  
|session_id|**nvarchar(32)**|操作を実行するセッションの ID。|[Transact-sql&#41;&#40;sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)の session_id を参照してください。|  
|request_id|**nvarchar(32)**|操作を実行する要求の ID。 読み込みの場合、これはこの負荷に関連付けられている現在の要求または最後の要求です。|[Transact-sql&#41;&#40;sys.dm_pdw_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)の request_id を参照してください。|  
|status|**nvarchar (16)**|実行の状態。|' 取り消された '、' COMPLETED '、' FAILED '、' QUEUED '、' RUNNING '|  
|progress|**int**|完了した割合。|0 から 100|  
|command|**nvarchar (4000)**|ユーザーによって送信されたコマンドの完全なテキスト。|4000文字を超える場合は切り捨てられます (空白をカウントする場合)。|  
|rows_processed|**bigint**|この操作の一部として処理された行の数。||  
|rows_rejected|**bigint**|この操作の一部として拒否された行数。||  
|rows_inserted|**bigint**|この操作の一部としてデータベーステーブルに挿入された行の数。||  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
