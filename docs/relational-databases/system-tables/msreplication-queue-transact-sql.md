---
description: MSreplication_queue (Transact-sql)
title: MSreplication_queue (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: caabac10703a39aa88afd357fd1596379f82978d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538260"
---
# <a name="msreplication_queue-transact-sql"></a>MSreplication_queue (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplication_queue**テーブルは、SQL ベースのキューを使用しているすべてのキュー更新サブスクリプションによって発行されたキューに登録されたコマンドを格納するために、レプリケーションプロセスによって使用されます。 このテーブルは、サブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**publisher_db**|**sysname**|パブリケーションデータベースの名前です。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**tranid**|**sysname**|キューに登録されたコマンドが実行されたときのトランザクション ID。|  
|**data**|**varbinary(8000)**|キューに置かれたコマンドに関する情報を格納した、パックされたバイトストリーム。|  
|**datalen**|**int**|データの長さ (バイト単位)。|  
|**commandtype**|**int**|キューに登録されるコマンドのタイプです。<br /><br /> 1 = トランザクション内のユーザーコマンド。<br /><br /> 2 = サブスクリプション同期コマンド|  
|**insertdate**|**datetime**|挿入日時です。|  
|**orderkey**|**bigint**|単調に増加する id 列。|  
|**cmdstate**|**bit**|コマンドの状態:<br /><br /> 0 = 完了します。<br /><br /> 1 = 部分的。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
