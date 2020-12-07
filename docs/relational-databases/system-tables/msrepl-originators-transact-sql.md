---
description: MSrepl_originators (Transact-SQL)
title: MSrepl_originators (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_originators_TSQL
- MSrepl_originators
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_originators system table
ms.assetid: a3ac20a6-73f6-4fdc-ad5f-5f72746c9871
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 19e66da5cab574e18b592e0636cd9b3412870a10
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544499"
---
# <a name="msrepl_originators-transact-sql"></a>MSrepl_originators (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_originators**テーブルには、トランザクションが発生した更新可能なサブスクライバーごとに1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|更新サブスクライバーを識別します。|  
|**publisher_database_id**|**int**|パブリケーションデータベースを識別します。|  
|**srvname**|**sysname**|更新サーバーの名前。|  
|**dbname**|**sysname**|更新するデータベースの名前。|  
|**publication_id**|**int**|パブリケーションを識別します。|  
|**dbversion**|**int**|データベースのバージョンを識別します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
