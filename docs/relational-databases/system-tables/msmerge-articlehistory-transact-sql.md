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
author: cawrites
ms.author: chadam
ms.openlocfilehash: 89a5e3969d6f55a38ecfdcb6abf2a41e322ce89f
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096249"
---
# <a name="msmerge_articlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_articlehistory** テーブルは、マージエージェント同期セッション中にアーティクルに加えられた変更を追跡し、変更が行われた各アーティクルに対して1つの行を使用します。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
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
  
  
