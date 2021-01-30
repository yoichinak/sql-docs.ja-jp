---
description: sys.edge_constraint_clauses (Transact-sql)
title: sys.edge_constraint_clauses (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.edge_constraint_clauses
- edge_constraint_clauses
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraint_clauses catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0138fea256558ee3cf57766462452452dfaa7c16
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203896"
---
# <a name="sysedge_constraint_clauses-transact-sql"></a>sys.edge_constraint_clauses (Transact-sql)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

エッジ制約の句ごとに1行の値を格納します。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|エッジの制約の object_id。|  
|**from_object_id**|**int**|FROM node テーブルの object_id。|  
|**to_object_id**|**int**|TO node テーブルの object_id。|  
|**clause_number**|**int**|句の内部で生成された整数インデックス。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
