---
description: sp_addsrvrolemember (Transact-SQL)
title: sp_addsrvrolemember (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec0b94d4423574729d4c92d869a73d04673edac8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536748"
---
# <a name="sp_addsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログインを固定サーバー ロールのメンバーとして追加します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>引数  
 [ @loginame **=** ] **'**_ログイン_**'**  
 固定サーバーロールに追加するログインの名前を指定します。 *login* は **sysname**,、既定値はありません。 *ログインに* は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたは Windows ログインを指定できます。 Windows ログインに対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのアクセスが許可されていない場合は、アクセスが自動的に許可されます。  
  
 [ @rolename **=** ] **'**_role_**'**  
 ログインを追加する固定サーバーロールの名前を指定します。 *role* の部分は **sysname**で、既定値は NULL です。次のいずれかの値を指定する必要があります。  
  
-   [sysadmin]  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 ログインを固定サーバー ロールに追加すると、そのロールに関係付けられている権限がログインに与えられます。  
  
 sa ログインと public のロール メンバーシップを変更することはできません。  
  
 メンバーを固定データベース ロールまたはユーザー定義のロールに追加するには、sp_addrolemember を使用します。  
  
 ユーザー定義のトランザクション内では、sp_addsrvrolemember は実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 新しいメンバーを追加するロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、Windows ログイン `Corporate\HelenS` を `sysadmin` 固定サーバーロールに追加します。  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
