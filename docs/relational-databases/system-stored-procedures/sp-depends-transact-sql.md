---
description: sp_depends (Transact-sql)
title: sp_depends (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_depends
- sp_depends_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_depends
ms.assetid: d9934590-c6ae-4936-91c3-146055ef2c57
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6251c556475165504075ae60a84b6d4f28766aef
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99206031"
---
# <a name="sp_depends-transact-sql"></a>sp_depends (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  テーブルまたはビューに依存するビューやプロシージャ、ビューまたはプロシージャに依存しているテーブルやビューなど、データベースオブジェクトの依存関係に関する情報を表示します。 現在のデータベース内に存在しないオブジェクトへの参照はレポートされません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md) と [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_depends [ @objname = ] '<object>'   
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name.  
    object_name  
}  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 データベースの名前です。  
  
 *schema_name*  
 オブジェクトが所属するスキーマの名前を指定します。  
  
 *object_name*  
 依存関係を調べるデータベースオブジェクトを示します。 オブジェクトには、テーブル、ビュー、ストアドプロシージャ、ユーザー定義関数、またはトリガーを指定できます。 o *bject_name* は **nvarchar (776)**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **sp_depends** には、2つの結果セットが表示されます。  
  
 次の結果セットは、が依存するオブジェクトを示して *\<object>* います。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (257** **)**|依存関係が存在するアイテムの名前。|  
|**type**|**nvarchar (16)**|項目の種類。|  
|**まし**|**nvarchar (7)**|項目が更新されているかどうか。|  
|**オフ**|**nvarchar(8)**|項目が SELECT ステートメントで使用されているかどうか。|  
|**column**|**sysname**|従属性が存在する列またはパラメーター。|  
  
 次の結果セットは、に依存するオブジェクトを示して *\<object>* います。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (257** **)**|依存関係が存在するアイテムの名前。|  
|**type**|**nvarchar (16)**|項目の種類。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-dependencies-on-a-table"></a>A. テーブルの従属性を一覧表示する  
 次の例では、データベース内のテーブルに依存するデータベースオブジェクトを一覧表示し `Sales.Customer` [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。 ここではスキーマ名とテーブル名の両方を指定します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_depends @objname = N'Sales.Customer' ;  
```  
  
### <a name="b-listing-dependencies-on-a-trigger"></a>B. トリガーの従属性を一覧表示する  
 次の例では、トリガーが依存しているデータベースオブジェクトを一覧表示し `iWorkOrder` ます。  
  
```  
EXEC sp_depends @objname = N'AdventureWorks2012.Production.iWorkOrder' ;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
