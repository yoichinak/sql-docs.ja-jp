---
description: MSmerge_history (Transact-SQL)
title: MSmerge_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: cawrites
ms.author: chadam
ms.openlocfilehash: 618a12dd664136e212bc6f31b9b59c1b87d413d7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203623"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_history** テーブルには、過去のマージエージェントジョブセッションの結果に関する詳細な説明を含む履歴行が含まれています。 このテーブルには、エージェントの出力行ごとに1つの行が含まれています。 このテーブルは、ディストリビューション データベースと各サブスクリプション データベースで使用されます。 ディストリビューションデータベースには、ディストリビューターを使用するすべてのマージパブリケーションおよびサブスクリプションの履歴が含まれています。 各サブスクリプションデータベースには、サブスクライバーがサブスクライブされているパブリケーションの履歴が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|マージエージェントジョブの ID。|  
|**agent_id**|**int**|マージエージェントの ID。|  
|**コメント**|**nvarchar (255)**|メッセージ テキスト。|  
|**error_id**|**int**|[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)システムテーブル内のエラーの ID。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
|**updatable_row**|**bit**|履歴行を上書きできる場合は、 **1** に設定します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
