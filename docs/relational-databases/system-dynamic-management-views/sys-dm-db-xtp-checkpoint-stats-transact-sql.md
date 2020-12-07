---
title: dm_db_xtp_checkpoint_stats (Transact-sql) |Microsoft Docs
description: 現在のデータベースのインメモリ OLTP チェックポイント操作に関する統計を返します。 SQL Server のバージョンごとにこのビューがどのように異なるかを説明します。
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66532a6ed19dc3a7929fe7d5638fa850c893d119
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542319"
---
# <a name="sysdm_db_xtp_checkpoint_stats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  現在のデータベースのインメモリ OLTP チェックポイント操作に関する統計を返します。 データベースにインメモリ OLTP オブジェクトが存在しない場合、は空の結果セットを返します。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
```  
USE In_Memory_db_name
SELECT * FROM sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、より新しいバージョンとは大幅に異なります。 [SQL Server 2014](#bkmk_2014)のトピックでは、この点について説明します。**
  
## <a name="sssql15-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降  
 次の表では、で始まるの列について説明し `sys.dm_db_xtp_checkpoint_stats` **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** ます。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|コントローラーによって表示される最後の LSN。|  
|end_of_log_lsn|**数値 (38)**|ログの末尾の LSN。|  
|bytes_to_end_of_log|**bigint**|との間のバイトに対応する、コントローラーによって処理されたログのバイト数 `last_lsn_processed` `end_of_log_lsn` 。|  
|log_consumption_rate|**bigint**|コントローラーによるトランザクションログの使用率 (KB/秒)。|  
|active_scan_time_in_ms|**bigint**|トランザクションログをアクティブにスキャンするためにコントローラーによって費やされた時間。|  
|total_wait_time_in_ms|**bigint**|ログをスキャンしていないときの、コントローラーの累積待機時間。|  
|waits_for_io|**bigint**|コントローラースレッドによって発生したログ IO の待機の数。|  
|io_wait_time_in_ms|**bigint**|コントローラースレッドによるログ IO の待機に費やされた累積時間。|  
|waits_for_new_log_count|**bigint**|新しいログを生成するためにコントローラースレッドによって発生する待機の数。|  
|new_log_wait_time_in_ms|**bigint**|コントローラースレッドによる新しいログの待機に費やされた累積時間。|  
|idle_attempts_count|**bigint**|コントローラーがアイドル状態に遷移した回数。|  
|tx_segments_dispatched|**bigint**|コントローラーによって認識され、シリアライザーにディスパッチされたセグメントの数。 セグメントは、シリアル化の単位を形成するログの連続部分です。 現在のサイズは 1 MB に設定されていますが、将来変更される可能性があります。|  
|segment_bytes_dispatched|**bigint**|データベースの再起動後に、コントローラーによってシリアライザーにディスパッチされたバイトの合計バイト数。|  
|bytes_serialized|**bigint**|データベースの再起動後にシリアル化された合計バイト数。|  
|serializer_user_time_in_ms|**bigint**|ユーザーモードでシリアライザーによって費やされた時間。|  
|serializer_kernel_time_in_ms|**bigint**|カーネルモードでシリアライザーに費やされた時間。|  
|xtp_log_bytes_consumed|**bigint**|データベースの再起動後に使用されたログのバイト数の合計。|  
|checkpoints_closed|**bigint**|データベースの再起動以降に閉じられたチェックポイントの数。|  
|last_closed_checkpoint_ts|**bigint**|最後に閉じられたチェックポイントのタイムスタンプ。|  
|hardened_recovery_lsn|**数値 (38)**|この LSN から復旧が開始されます。|  
|hardened_root_file_guid|**uniqueidentifier**|最後に完了したチェックポイントの結果として書き込まれたルートファイルの GUID。|  
|hardened_root_file_watermark|**bigint**|**内部のみ**。 ルートファイルをどこまで読み取ることができるか (これは、内部的に関連する型のみの BSN と呼ばれます)。|  
|hardened_truncation_lsn|**数値 (38)**|切り捨てポイントの LSN。|  
|log_bytes_since_last_close|**bigint**|最後から現在のログの最後までのバイト数。|  
|time_since_last_close_in_ms|**bigint**|チェックポイントが最後に閉じられてからの時間です。|  
|current_checkpoint_id|**bigint**|現在、このチェックポイントに新しいセグメントが割り当てられています。 チェックポイントシステムはパイプラインです。 現在のチェックポイントは、ログから割り当てられているセグメントです。 制限に達すると、チェックポイントはコントローラーによって解放され、新しいとして作成されます。|  
|current_checkpoint_segment_count|**bigint**|現在のチェックポイント内のセグメントの数。|  
|recovery_lsn_candidate|**bigint**|**内部的にのみ**。 Current_checkpoint_id が閉じるときに recoverylsn として選択される候補です。|  
|outstanding_checkpoint_count|**bigint**|終了を待機しているパイプライン内のチェックポイントの数。|  
|closing_checkpoint_id|**bigint**|終了チェックポイントの ID です。<br /><br /> シリアライザーは並行して動作しているため、完了すると、チェックポイントは終了スレッドによって閉じられる候補になります。 ただし、close スレッドは一度に1つだけを閉じることができます。そのため、終了のチェックポイントは終了スレッドが処理されているものです。|  
|recovery_checkpoint_id|**bigint**|復旧に使用するチェックポイントの ID。|  
|recovery_checkpoint_ts|**bigint**|回復チェックポイントのタイムスタンプ。|  
|bootstrap_recovery_lsn|**数値 (38)**|ブートストラップの復旧 LSN。|  
|bootstrap_root_file_guid|**uniqueidentifier**|ブートストラップのルートファイルの GUID。|  
|internal_error_code|**bigint**|コントローラー、シリアライザー、閉じる、およびマージスレッドによってエラーが発生しました。|
|bytes_of_large_data_serialized|**bigint**|シリアル化されたデータの量。 |  
  
##  <a name="sssql14"></a><a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 次の表では、の列について説明し `sys.dm_db_xtp_checkpoint_stats` **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** ます。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|スレッドの現在のログシーケンス番号 (LSN) とログの末尾との間のログバイト数。|  
|total_log_blocks_processed|**bigint**|サーバーの起動後に処理されたログブロックの合計数。|  
|total_log_records_processed|**bigint**|サーバーが起動した後で処理されたログ レコードの合計数。|  
|xtp_log_records_processed|**bigint**|サーバーの起動以降に処理されたインメモリ OLTP ログレコードの合計数。|  
|total_wait_time_in_ms|**bigint**|累積待機時間 (ミリ秒)。|  
|waits_for_io|**bigint**|ログ IO の待機の数。|  
|io_wait_time_in_ms|**bigint**|ログ IO の待機に費やされた累積時間。|  
|waits_for_new_log|**bigint**|新しいログが生成されるのを待機する回数。|  
|new_log_wait_time_in_ms|**bigint**|新しいログの待機に費やされた累積時間。|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|前回のインメモリ OLTP チェックポイント以降に生成されたログの量。|  
|ms_since_last_checkpoint|**bigint**|最後のインメモリ OLTP チェックポイントからの経過時間 (ミリ秒)。|  
|checkpoint_lsn|**数値 (38)**|最後に完了したインメモリ OLTP チェックポイントに関連付けられている復旧ログシーケンス番号 (LSN)。|  
|current_lsn|**数値 (38)**|現在処理中のログレコードの LSN。|  
|end_of_log_lsn|**数値 (38)**|ログの末尾の LSN。|  
|task_address|**varbinary (8)**|SOS_Task のアドレス。 追加の情報を得るには、sys.dm_os_tasks と組み合わせます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW DATABASE STATE` 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
