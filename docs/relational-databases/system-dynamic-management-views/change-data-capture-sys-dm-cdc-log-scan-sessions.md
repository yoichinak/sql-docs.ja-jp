---
description: 変更データキャプチャ-sys. dm_cdc_log_scan_sessions
title: dm_cdc_log_scan_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_log_scan_sessions
- dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], log scan reporting
- sys.dm_cdc_log_scan_sessions dynamic management view
ms.assetid: d337e9d0-78b1-4a07-8820-2027d0b9f87c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bef7989e6533b56ff1976ccf5fe145954a69afb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534340"
---
# <a name="change-data-capture---sysdm_cdc_log_scan_sessions"></a>変更データキャプチャ-sys. dm_cdc_log_scan_sessions
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内のログスキャンセッションごとに1行のデータを返します。 最後に返された行は、現在のセッションを表します。 このビューを使用すると、現在のログ スキャン セッションのステータス情報を取得できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが開始されてからのすべてのセッションの集計情報を取得することもできます。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|セッションの ID。<br /><br /> 0 = この行で返されるデータは、のインスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最後に起動されてからのすべてのセッションの集計です。|  
|**start_time**|**datetime**|セッションの開始時刻です。<br /><br /> **Session_id** = 0 の場合、集計されたデータの収集が開始されます。|  
|**end_time**|**datetime**|セッションが終了した時刻。<br /><br /> NULL は、セッションがアクティブであることを表します。<br /><br /> **Session_id** = 0 の場合、最後のセッションが終了した時刻。|  
|**duration**|**bigint**|セッションの実行時間 (秒単位) です。<br /><br /> 0 = セッションには変更データキャプチャトランザクションが含まれていません。<br /><br /> **Session_id** = 0 の場合、変更データキャプチャトランザクションを含むすべてのセッションの期間 (秒単位) の合計。|  
|**scan_phase**|**nvarchar(200)**|セッションの現在のフェーズです。 使用可能な値とその説明を次に示します。<br /><br /> 1: 構成の読み取り<br />2: 最初のスキャン、ハッシュテーブルの作成<br />3: 2 回目のスキャン<br />4: 2 回目のスキャン<br />5: 2 回目のスキャン<br />6: スキーマのバージョン管理<br />7: 前回のスキャン<br />8: 完了<br /><br /> **Session_id** = 0 の場合、この値は常に "Aggregate" になります。|  
|**error_count**|**int**|発生したエラーの数。<br /><br /> **Session_id** = 0 の場合、すべてのセッションで発生したエラーの合計数。|  
|**start_lsn**|**nvarchar (23)**|セッションの開始 LSN です。<br /><br /> **Session_id** = 0 の場合、最後のセッションの開始 LSN です。|  
|**current_lsn**|**nvarchar (23)**|スキャンされている現在の LSN。<br /><br /> **Session_id** = 0 の場合、現在の LSN は0です。|  
|**end_lsn**|**nvarchar (23)**|セッションの最終 LSN です。<br /><br /> NULL は、セッションがアクティブであることを表します。<br /><br /> **Session_id** = 0 の場合、最後のセッションの終了 LSN です。|  
|**tran_count**|**bigint**|処理された変更データキャプチャトランザクションの数。 このカウンターはフェーズ2で設定されます。<br /><br /> **Session_id** = 0 の場合、すべてのセッションで処理されたトランザクションの数。|  
|**last_commit_lsn**|**nvarchar (23)**|最後に処理されたコミットログレコードの LSN。<br /><br /> **Session_id** = 0 の場合、任意のセッションの最後のコミットログレコードの LSN。|  
|**last_commit_time**|**datetime**|最後のコミットログレコードが処理された時刻。<br /><br /> **Session_id** = 0 の場合、任意のセッションの最後のコミットログレコードの時刻。|  
|**log_record_count**|**bigint**|スキャンされたログレコードの数。<br /><br /> **Session_id** = 0 の場合、すべてのセッションについてスキャンされたレコードの数。|  
|**schema_change_count**|**int**|検出されたデータ定義言語 (DDL) 操作の数。 このカウンターはフェーズ6で設定されます。<br /><br /> **Session_id** = 0 の場合、すべてのセッションで処理された DDL 操作の数。|  
|**command_count**|**bigint**|処理されたコマンドの数。<br /><br /> **Session_id** = 0 の場合、すべてのセッションで処理されたコマンドの数。|  
|**first_begin_cdc_lsn**|**nvarchar (23)**|変更データ キャプチャ トランザクションを含んでいた最初の LSN です。<br /><br /> **Session_id** = 0 の場合、変更データキャプチャトランザクションを含んでいる最初の LSN です。|  
|**last_commit_cdc_lsn**|**nvarchar (23)**|変更データキャプチャトランザクションが含まれていた最後のコミットログレコードの LSN。<br /><br /> **Session_id** = 0 の場合、変更データキャプチャトランザクションが含まれているすべてのセッションの最後のコミットログレコードの LSN|  
|**last_commit_cdc_time**|**datetime**|変更データ キャプチャ トランザクションを含んでいた最終コミット ログ レコードが処理された時刻です。<br /><br /> **Session_id** = 0 の場合、変更データキャプチャトランザクションが含まれているセッションの最後のコミットログレコードの時刻。|  
|**短い**|**int**|セッションの **end_time** と **last_commit_cdc_time** の差 (秒単位)。 このカウンターはフェーズ7の最後に設定されます。<br /><br /> **Session_id** = 0 の場合、セッションによって記録された最後の0以外の待機時間の値。|  
|**empty_scan_count**|**int**|変更データキャプチャトランザクションが含まれていない連続したセッションの数。|  
|**failed_sessions_count**|**int**|失敗したセッションの数。|  
  
## <a name="remarks"></a>解説  
 この動的管理ビューの値は、のインスタンスが起動されるたびにリセットされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="permissions"></a>アクセス許可  
 **Dm_cdc_log_scan_sessions**動的管理ビューに対してクエリを実行するには、VIEW DATABASE STATE 権限が必要です。 動的管理ビューに対する権限の詳細については、「 [transact-sql&#41;&#40;の動的管理ビューおよび関数 ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、最新のセッションに関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase,  
    error_count, start_lsn, current_lsn, end_lsn, tran_count,  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count,  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [dm_cdc_errors &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

