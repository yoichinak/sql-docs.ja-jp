---
description: MSrepl_backup_lsns (Transact-SQL)
title: MSrepl_backup_lsns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 743657bad9cf4c0bd1611e7f00f1d410753583ce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540259"
---
# <a name="msrepl_backup_lsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_backup_lsns**テーブルには、ディストリビューションデータベースの "sync with backup" オプションをサポートするためのトランザクションログシーケンス番号 (LSN) が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|パブリッシャーデータベースの ID。|  
|**valid_xact_id**|**varbinary(16)**|ログの切り捨てポイントをマークするためにパブリッシャーに送信されるトランザクションの ID。 ディストリビューションデータベースが "sync with backup" モードの場合にのみ使用されます。 バックアップされたディストリビューションデータベース内の最新のレプリケートされたトランザクションの ID を格納します。 ログの切り捨てポイントをログリーダーがマークするために、パブリッシャーに送信されます。|  
|**valid_xact_seqno**|**varbinary(16)**|ログの切り捨てポイントをマークするためにパブリッシャーに送信されるトランザクションのシーケンス番号。 ディストリビューション データベースが "sync with backup" モードの場合にのみ使用されます。 バックアップされたディストリビューション データベース内の、最新のレプリケートされたトランザクションのログ シーケンス番号に相当します。 ログの切り捨てポイントをログリーダーがマークするために、パブリッシャーに送信されます。|  
|**next_xact_id**|**varbinary(16)**|バックアップ操作で使用する一時的なログ シーケンス番号。|  
|**nextx_xact_seqno**|**varbinary(16)**|バックアップ操作で使用する一時的なログ シーケンス番号。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
