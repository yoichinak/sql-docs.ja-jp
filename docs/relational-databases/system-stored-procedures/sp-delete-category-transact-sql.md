---
description: sp_delete_category (Transact-sql)
title: sp_delete_category (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_category_TSQL
- sp_delete_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_category
ms.assetid: 63ea7d0d-a567-456e-a778-bee99e21d16c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cdeb258bf7a61e5cfa4bafe796729f7c445e8cde
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541833"
---
# <a name="sp_delete_category-transact-sql"></a>sp_delete_category (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したジョブ、警告、またはオペレーターのカテゴリを、現在のサーバーから削除します。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_category [ @class = ] 'class' , [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>引数  
`[ @class = ] 'class'` カテゴリのクラス。 *クラス* は **varchar (8)**,、既定値はありませんが、次のいずれかの値を持つ必要があります。  
  
|[値]|説明|  
|-----------|-----------------|  
|**補足**|ジョブカテゴリを削除します。|  
|**アラート**|アラートカテゴリを削除します。|  
|**OPERATOR**|オペレーター カテゴリを削除します。|  
  
`[ @name = ] 'name'` 削除するカテゴリの名前。 *名前* は **sysname**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_delete_category** は、 **msdb** データベースから実行する必要があります。  
  
 カテゴリを削除すると、そのカテゴリのすべてのジョブ、警告、または演算子が、クラスの既定のカテゴリに recategorizes ます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、`AdminJobs` というジョブ カテゴリを削除します。  
  
```  
USE msdb ;  
GO   
  
EXEC dbo.sp_delete_category  
    @name = N'AdminJobs',  
    @class = N'JOB' ;  
GO   
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_help_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
