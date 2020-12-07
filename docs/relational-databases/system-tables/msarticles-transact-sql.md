---
description: MSarticles (Transact-sql)
title: MSarticles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3123834712540681748ab39edbfa6ee39d78ea14
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545724"
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Msarticles**テーブルには、パブリッシャーによってレプリケートされるアーティクルごとに1行の情報が格納されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**publication_id**|**int**|パブリケーションの ID です。|  
|**記事**|**sysname**|アーティクルの名前です。|  
|**article_id**|**int**|アーティクルの ID です。|  
|**destination_object**|**sysname**|サブスクライバーで作成されたテーブルの名前です。|  
|**source_owner**|**sysname**|パブリッシャー上の元のテーブルのスキーマの名前です。|  
|**source_object**|**sysname**|アーティクルを追加するソースオブジェクトの名前です。|  
|**description**|**nvarchar (255)**|アーティクルの説明です。|  
|**destination_owner**|**sysname**|サブスクライバーで作成されたテーブルのスキーマの名前です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
