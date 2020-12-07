---
description: MSmerge_articlehistory (Transact-SQL)
title: MSmerge_articlehistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5fcf637d540b541f0a96e6a8f8322c34799ddcb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544540"
---
# <a name="msmerge_articlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_articlehistory**テーブルは、マージエージェント同期セッション中にアーティクルに加えられた変更を追跡し、変更が行われた各アーティクルに対して1つの行を使用します。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md)システムテーブル内のマージエージェントジョブセッションの ID。|  
|**phase_id**|**int**|同期セッションのフェーズ。次のいずれかを指定できます。<br /><br /> **1** = アップロードします。<br /><br /> **2** = ダウンロード。<br /><br /> **4** = クリーンアップ。<br /><br /> **5** = シャットダウン。<br /><br /> **6** = スキーマの変更。<br /><br /> **7** = BCP。|  
|**article_name**|**sysname**|変更が行われたアーティクルの名前。|  
|**start_time**|**datetime**|エージェントがアーティクルの処理を開始した時刻です。|  
|**duration**|**int**|エージェントがアーティクルを処理した時間の長さ (秒単位)。|  
|**ます**|**int**|同期中に特定のアーティクルに適用された挿入の数。 この値は同期プロセス中に増加し、終了値は合計数を表します。|  
|**更新プログラム**|**int**|同期中に特定のアーティクルに適用された更新数です。 この値は同期プロセス中に増加し、終了値は合計数を表します。|  
|**削除**|**int**|同期中に特定のアーティクルに適用された削除の数。 この値は同期プロセス中に増加し、終了値は合計数を表します。|  
|**重なっ**|**int**|同期中に発生した競合の数。 この値は同期プロセス中に増加し、終了値は合計数を表します。|  
|**conflicts_resolved**|**int**|同期中に発生した競合のうち、解決された競合の数。 この値は同期プロセス中に増加し、終了値は合計数を表します。|  
|**rows_retried**|**int**|同期中に再試行された、失敗した行の数。 この値は同期プロセス中に増加し、終了値は合計数を表します。|  
|**percent_complete**|**decimal**|セッション中にアーティクルに対してマージエージェントが費やした合計同期時間の割合。 この値は、セッションが完了するまで NULL です。|  
|**estimated_changes**|**int**|アーティクルに適用する必要がある行の変更の推定数。|  
|**relative_cost**|**decimal**|この記事の変更を適用するために費やされた時間と、セッション全体の合計時間。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
