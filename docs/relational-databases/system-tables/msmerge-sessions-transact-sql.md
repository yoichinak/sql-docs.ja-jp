---
description: MSmerge_sessions (Transact-sql)
title: MSmerge_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8bcfbf7faab359bec8241428aad9e471d4ed79be
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545627"
---
# <a name="msmerge_sessions-transact-sql"></a>MSmerge_sessions (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_sessions**テーブルには、前のマージエージェントジョブセッションの結果を含む履歴行が含まれています。 このテーブルには、マージ エージェントが実行されるたびに、新しい行が追加されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|マージエージェントジョブセッションの ID です。|  
|**agent_id**|**int**|マージエージェントの ID。|  
|**start_time**|**datetime**|ジョブの実行が開始された時刻。|  
|**end_time**|**datetime**|ジョブの実行完了時刻。|  
|**duration**|**int**|このジョブセッションの累積時間 (秒単位)。|  
|**delivery_time**|**int**|変更のバッチを適用するために要した秒数。|  
|**upload_time**|**int**|パブリッシャーに変更をアップロードするのにかかった時間 (秒数)。|  
|**download_time**|**int**|サブスクライバーへの変更のダウンロードに要した秒数。|  
|**delivery_rate**|**float**|1秒間に配信されたコマンドの平均数。|  
|**time_remaining**|**int**|アクティブなセッションの残りの秒数。|  
|**percent_complete**|**decimal**|アクティブなセッションで既に配信されている変更の合計の推定割合。|  
|**upload_inserts **|**int**|パブリッシャー側で適用される挿入の数です。|  
|**upload_updates**|**int**|パブリッシャーで適用された更新数。|  
|**upload_deletes **|**int**|パブリッシャー側で適用される削除の数です。|  
|**upload_conflicts**|**int**|パブリッシャー側で変更を適用する間に発生した競合の数です。|  
|**upload_conflicts_resolved**|**int**|パブリッシャーで変更を適用している間に、解決された競合の数。|  
|**upload_rows_retried**|**int**|パブリッシャーにアップロードされた行数のうち、再試行された行数。|  
|**download_inserts **|**int**|サブスクライバー側で適用される挿入の数です。|  
|**download_updates**|**int**|サブスクライバーで適用された更新プログラムの数。|  
|**download_deletes **|**int**|サブスクライバー側で適用される削除の数です。|  
|**download_conflicts**|**int**|サブスクライバーで変更を適用している間に発生した競合の数。|  
|**download_conflicts_resolved**|**int**|サブスクライバーで変更を適用している間に、解決された競合の数。|  
|**download_rows_retried**|**int**|サブスクライバーにダウンロードされた行数のうち、再試行された行数。|  
|**schema_changes**|**int**|セッション中に適用されたスキーマ変更の数。|  
|**metadata_rows_cleanedup**|**int**|セッション中にクリーンアップされたメタデータの行の数。|  
|**runstatus**|**int**|実行ステータスです。<br /><br /> **1** = 開始します。<br /><br /> **2** = 成功します。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗。|  
|**estimated_upload_changes**|**int**|パブリッシャーで適用する必要がある変更の推定数。|  
|**estimated_download_changes**|**int**|サブスクライバーで適用する必要がある変更の推定数。|  
|**connection_type**|**int**|アップロード中に使用される接続:<br /><br /> **1** = ローカルエリアネットワーク (LAN)。<br /><br /> **2** = ダイヤルアップネットワーク接続。<br /><br /> **3** = Web 同期。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
