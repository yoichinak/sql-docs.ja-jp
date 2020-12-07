---
description: sysarticleupdates (Transact-sql)
title: sysarticleupdates (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ca984460c74628f919e16c77c3a3a97fa732b52
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89518226"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  即時更新サブスクリプションをサポートするアーティクルごとに1行のレコードを格納します。 このテーブルは、レプリケートされたデータベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルの一意な ID 番号を示す ID 列。|  
|**pubid**|**int**|アーティクルが属しているパブリケーションの ID。|  
|**sync_ins_proc**|**int**|挿入同期トランザクションを処理するストアドプロシージャの ID。|  
|**sync_upd_proc**|**int**|更新同期トランザクションを処理するストアドプロシージャの ID。|  
|**sync_del_proc**|**int**|削除同期トランザクションを処理するストアドプロシージャの ID。|  
|**autogen**|**bit**|ストアドプロシージャが自動的に生成されることを示します。<br /><br /> **0** = False、自動ではありません。<br /><br /> **1** = True、自動。|  
|**sync_upd_trig**|**int**|アーティクルテーブルの自動バージョン管理トリガーの ID です。|  
|**conflict_tableid**|**int**|競合テーブルの ID。|  
|**ins_conflict_proc**|**int**|競合を **conflict_table**に書き込むために使用されるプロシージャの ID。|  
|**identity_support**|**bit**|キュー更新を使用するときに、自動 id 範囲処理を有効にするかどうかを指定します。 **0** は、id 範囲がサポートされていないことを示します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
