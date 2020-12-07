---
description: sys.dm_repl_traninfo (Transact-SQL)
title: sys.dm_repl_traninfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_traninfo
- dm_repl_traninfo
- sys.dm_repl_traninfo_TSQL
- dm_repl_traninfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_traninfo dynamic management view
ms.assetid: 5abe2605-0506-46ec-82b5-6ec08428ba13
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6369fc0d1ee2c0b70cb3e6e13fd201fd718236dc
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834574"
---
# <a name="sysdm_repl_traninfo-transact-sql"></a>sys.dm_repl_traninfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  レプリケートされたトランザクションまたは変更データ キャプチャ トランザクションごとの情報を返します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**fp2p_pub_exists**|**tinyint**|トランザクションがピアツーピアトランザクションレプリケーションを使用してパブリッシュされたデータベース内にある場合。 True の場合、値は1です。それ以外の場合は0になります。|  
|**db_ver**|**int**|データベースのバージョン。|  
|**comp_range_address**|**varbinary (8)**|スキップする必要がある部分ロールバック範囲を定義します。|  
|**textinfo_address**|**varbinary (8)**|キャッシュされたテキスト情報の構造体のメモリ内アドレス。|  
|**fsinfo_address**|**varbinary (8)**|キャッシュされたファイル ストリーム情報構造のメモリ内アドレス。|  
|**begin_lsn**|**nvarchar (64)**|トランザクションの開始ログレコードのログシーケンス番号 (LSN)。|  
|**commit_lsn**|**nvarchar (64)**|トランザクションのコミットログレコードの LSN。|  
|**dbid**|**smallint**|データベース ID。|  
|**rows**|**int**|トランザクション内のレプリケートされたコマンドの ID。|  
|**が属する xdesid**|**nvarchar (64)**|トランザクション ID。|  
|**artcache_table_address**|**varbinary (8)**|このトランザクションに最後に使用された、キャッシュされたアーティクルテーブル構造のメモリ内アドレス。|  
|**server**|**nvarchar (514)**|サーバー名。|  
|**server_len_in_bytes**|**smallint**|サーバー名の文字長 (バイト単位)。|  
|**database**|**nvarchar (514)**|データベース名。|  
|**db_len_in_bytes**|**smallint**|データベース名の文字長 (バイト単位)。|  
|**送信者**|**nvarchar (514)**|トランザクションが発生したサーバーの名前。|  
|**originator_len_in_bytes**|**smallint**|トランザクションが発生したサーバーの文字長 (バイト単位)。|  
|**orig_db**|**nvarchar (514)**|トランザクションが発生したデータベースの名前。|  
|**orig_db_len_in_bytes**|**smallint**|トランザクションが発生したデータベースの文字長 (バイト単位)。|  
|**cmds_in_tran**|**int**|現在のトランザクションでレプリケートされたコマンドの数。これは、論理トランザクションをコミットする必要があるかどうかを判断するために使用されます。|  
|**is_boundedupdate_singleton**|**tinyint**|一意の列の更新が単一行に影響するかどうかを指定します。|  
|**begin_update_lsn**|**nvarchar (64)**|一意の列更新で使用される LSN。|  
|**delete_lsn**|**nvarchar (64)**|更新プログラムの一部として削除する LSN。|  
|**last_end_lsn**|**nvarchar (64)**|論理トランザクションの最後の LSN。|  
|**fcomplete**|**tinyint**|コマンドが部分的な更新かどうかを指定します。|  
|**fcompensated**|**tinyint**|トランザクションが部分ロールバックに含まれるかどうかを示します。|  
|**fprocessingtext**|**tinyint**|トランザクションにバイナリ ラージ データ型列が含まれるかどうかを示します。|  
|**max_cmds_in_tran**|**int**|ログリーダーエージェントによって指定された、論理トランザクション内のコマンドの最大数。|  
|**begin_time**|**datetime**|トランザクションが開始された時刻。|  
|**commit_time**|**datetime**|トランザクションがコミットされた時刻。|  
|**session_id**|**int**|変更データキャプチャのログスキャンセッションの ID。 この列は[sys.dm_cdc_logscan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)の**session_id**列にマップされます。|  
|**session_phase**|**int**|エラー発生時のセッションのフェーズを示す数値。 この列は[sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)の**phase_number**列にマップされます。|  
|**is_known_cdc_tran**|**bit**|トランザクションが変更データキャプチャによって追跡されることを示します。<br /><br /> 0 = トランザクション レプリケーション トランザクション。<br /><br /> 1 = 変更データ キャプチャ トランザクション。|  
|**error_count**|**int**|発生したエラーの数。|  
  
## <a name="permissions"></a>アクセス許可  
 パブリケーション データベースまたは変更データ キャプチャが有効にされたデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>注釈  
 この情報は、アーティクルキャッシュに現在読み込まれている、レプリケートされたデータベースオブジェクトまたは変更データキャプチャが有効になっているテーブルに対してのみ返されます。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)   
 [変更データ キャプチャに関連した動的管理ビュー &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)  
  
