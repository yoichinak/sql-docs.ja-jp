---
description: MSrepl_errors (Transact-SQL)
title: MSrepl_errors (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5afa86de5a33eab4f7e77da1c825619a738381de
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540283"
---
# <a name="msrepl_errors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_errors**テーブルには、拡張ディストリビューションエージェントとマージエージェントエラー情報を含む行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|エラーの ID。|  
|**time**|**datetime**|エラーが発生した時刻。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id **|**int**|エラーソースの種類 ID。|  
|**source_name**|**nvarchar (100)**|エラー ソースの名前です。|  
|**error_code**|**sysname**|エラー コード。|  
|**error_text **|**ntext**|エラー メッセージ。|  
|**xact_seqno**|**varbinary(16)**|失敗した実行バッチの先頭のトランザクション ログ シーケンス番号です。 ディストリビューションエージェントでのみ使用されます。これは、失敗した実行バッチ内の最初のトランザクションのトランザクションログシーケンス番号です。|  
|**command_id**|**int**|失敗した実行バッチのコマンド ID。 ディストリビューションエージェントでのみ使用されます。これは、失敗した実行バッチ内の最初のコマンドのコマンド ID です。|  
|**session_id**|**int**|エラーが発生したエージェントセッションの ID。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
