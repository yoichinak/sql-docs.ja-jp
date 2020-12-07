---
description: plan_guides (Transact-sql)
title: plan_guides (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8aacbeebf50eae1a6e20d35262dbdc054f1429d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550482"
---
# <a name="sysplan_guides-transact-sql"></a>plan_guides (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  データベース内のプラン ガイドごとに 1 行のデータを保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|データベース内のプランガイドを表す一意の識別子です。|  
|**name**|**sysname**|プラン ガイドの名前です。|  
|**create_date**|**datetime**|プランガイドが作成された日付と時刻。|  
|**modify_date**|**Datetime**|プランガイドが最後に変更された日付。|  
|**is_disabled**|**bit**|1 = プランガイドは無効です。<br /><br /> 0 = プラン ガイドは有効です。|  
|**query_text**|**nvarchar(max)**|プラン ガイドの作成対象であるクエリのテキストです。|  
|**scope_type**|**tinyint**|プランガイドのスコープを識別します。<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar(60)**|プランガイドのスコープの説明です。<br /><br /> OBJECT<br /><br /> SQL<br /><br /> テンプレート|  
|**scope_object_id**|**Int**|スコープがオブジェクトの場合、プランガイドのスコープを定義するオブジェクトの object_id。<br /><br /> プランガイドのスコープがオブジェクトに設定されていない場合は NULL です。|  
|**scope_batch**|**nvarchar(max)**|バッチテキスト ( **scope_type** が SQL の場合)。<br /><br /> バッチ型が SQL でない場合は、NULL です。<br /><br /> NULL と **scope_type** が SQL の場合、 **query_text** の値が適用されます。|  
|**parameters**|**nvarchar(max)**|プラン ガイドに関連付けられているパラメーターの一覧を定義する文字列です。<br /><br /> NULL = プランガイドに関連付けられているパラメーターリストはありません。|  
|**ヒント**|**nvarchar(max)**|プランガイドに関連付けられている OPTION 句ヒント。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
