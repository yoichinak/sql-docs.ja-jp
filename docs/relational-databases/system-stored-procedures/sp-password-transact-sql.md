---
description: sp_password (Transact-sql)
title: sp_password (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f0675634050234b00cadccf63c0f44295a21e56a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481103"
---
# <a name="sp_password-transact-sql"></a>sp_password (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログインのパスワードを追加または変更 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @old = ] 'old_password'` 古いパスワードを入力します。 *old_password* は **sysname**,、既定値は NULL です。  
  
`[ @new = ] 'new_password'` 新しいパスワードを入力します。 *new_password* は **sysname**であり、既定値はありません。 名前付きパラメーターを使用しない場合は、 *old_password*を指定する必要があります。  
  
> [!IMPORTANT]  
>  NULL パスワードは使用しないでください。 強力なパスワードを使用してください。 詳細については、「 [Strong Passwords](../../relational-databases/security/strong-passwords.md)」を参照してください。  
  
`[ @loginame = ] 'login'` パスワード変更によって影響を受けるログインの名前を指定します。 *login* のデータ型は **sysname** で、既定値は NULL です。 *ログイン* は既に存在している必要があり、 **sysadmin** または **securityadmin** 固定サーバーロールのメンバーのみが指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **SP_PASSWORD** ALTER LOGIN を呼び出します。 このステートメントでは、追加のオプションがサポートされています。 パスワードの変更の詳細については、「 [ALTER LOGIN &#40;transact-sql&#41;](../../t-sql/statements/alter-login-transact-sql.md)」を参照してください。  
  
 **sp_password** は、ユーザー定義のトランザクション内では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY LOGIN 権限が必要です。 古いパスワードを指定しないでパスワードをリセットする場合、または変更されるログインに CONTROL SERVER 権限がある場合は、CONTROL SERVER 権限も必要です。  
  
 プリンシパルは自身のパスワードを変更できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. 古いパスワードがわからなくてもログインのパスワードを変更する  
 次の例では、`ALTER LOGIN` を使って、`Victoria` ログイン用のパスワードを `B3r1000d#2-36` に変更します。 可能であればこの方法の使用をお勧めします。 このコマンドを実行するユーザーには、CONTROL SERVER 権限が必要です。  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. パスワードの変更  
 次の例は、を使用して、 `ALTER LOGIN` ログインのパスワードをからに変更する方法を示して `Victoria` `B3r1000d#2-36` `V1cteAmanti55imE` います。 可能であればこの方法の使用をお勧めします。 ユーザー `Victoria` は、追加の権限を取得しなくてもこのコマンドを実行できます。 他のユーザーには ALTER ANY LOGIN 権限が必要です。  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
