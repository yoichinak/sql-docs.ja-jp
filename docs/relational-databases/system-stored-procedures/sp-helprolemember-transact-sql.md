---
description: sp_helprolemember (Transact-SQL)
title: sp_helprolemember (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bbfec9641e543b4774a8d8d6f7a288bd2fe23c8a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541712"
---
# <a name="sp_helprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに含まれるロールの直接的なメンバーに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] ' role '` 現在のデータベース内のロールの名前を指定します。 *role* の部分は **sysname**で、既定値は NULL です。 *ロール* は現在のデータベースに存在している必要があります。 *Role*が指定されていない場合は、現在のデータベースの少なくとも1つのメンバーを含むすべてのロールが返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|現在のデータベース内のロールの名前。|  
|**MemberName**|**sysname**|DbRole のメンバーの名前 **。**|  
|**MemberSID**|**varbinary(85)**|MemberName のセキュリティ識別子 **。**|  
  
## <a name="remarks"></a>解説  
 データベースに入れ子になったロールが含まれている場合、 **MemberName** にはロールの名前を指定できます。 **sp_helprolemember** には、入れ子になったロールで取得したメンバーシップは表示されません。 たとえば、User1 が Role1 のメンバーで、Role1 が Role2 のメンバーである場合、 `EXEC sp_helprolemember 'Role2'` は Role1 を返しますが、Role1 のメンバー (この例では user1) は返しません。 入れ子になったメンバーシップを返すには、入れ子になったロールごとに **sp_helprolemember** を繰り返し実行する必要があります。  
  
 **Sp_helpsrvrolemember**を使用すると、固定サーバーロールのメンバーを表示できます。  
  
 [IS_ROLEMEMBER &#40;transact-sql&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)を使用して、指定されたユーザーのロールメンバーシップを確認します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、ロール `Sales` のメンバーを表示します。  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
