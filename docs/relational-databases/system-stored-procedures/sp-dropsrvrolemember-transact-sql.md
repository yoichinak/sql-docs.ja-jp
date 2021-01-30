---
description: sp_dropsrvrolemember (Transact-sql)
title: sp_dropsrvrolemember (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: d042fa55cf15dac997d7e52f9bd39eb7309fd1b5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99158099"
---
# <a name="sp_dropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-sql)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

固定サーバー ロールから、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインや、Windows ユーザーまたはグループを削除します。

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) を使用してください。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## <a name="arguments"></a>引数

**[ @loginame =]** '_login_'  
固定サーバーロールから削除するログインの名前を指定します。 *login* は **sysname**,、既定値はありません。 *ログイン* が存在する必要があります。  

**[ @rolename =]** '_role_'  
サーバーロールの名前を指定します。 *role* の部分は **sysname** で、既定値は NULL です。 *role* には、次のいずれかの値を指定する必要があります。  

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
 固定サーバー ロールからログインを削除できるのは、sp_dropsrvrolemember だけです。 データベース ロールからメンバーを削除するには、sp_droprolemember を使用します。  
  
 sa ログインは、どの固定サーバー ロールからも削除できません。  
  
 ユーザー定義のトランザクション内では、sp_dropsrvrolemember は実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。または、サーバーに対する ALTER ANY LOGIN 権限と、メンバーが削除されるロールのメンバーシップの両方が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 `JackO` 固定サーバーロールからログインを削除し `sysadmin` ます。  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
