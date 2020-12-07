---
description: sp_dropremotelogin (Transact-SQL)
title: sp_dropremotelogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 6ccb8f6c4bbf5795784c8ad3712c5fe8163ff0e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474226"
---
# <a name="sp_dropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行中のローカル サーバーに対してリモート ストアド プロシージャを実行する場合に使用される、ローカル ログインにマップされているリモート ログインを削除します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 代わりに、リンクサーバーとリンクサーバーストアドプロシージャを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @remoteserver = ] 'remoteserver'` 削除するリモートログインにマップされるリモートサーバーの名前を指定します。 *remoteserver* は **sysname**,、既定値はありません。 *remoteserver* は既に存在している必要があります。  
  
`[ @loginame = ] 'login'` リモートサーバーに関連付けられているローカルサーバー上のログイン名を指定します (省略可能)。 *login* のデータ型は **sysname** で、既定値は NULL です。 指定した場合、*ログイン*は既に存在している必要があります。  
  
`[ @remotename = ] 'remote_name'` リモートサーバーからログインするときに *ログイン* にマップされるリモートログインの名前を指定します (省略可能)。 *remote_name* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 *Remoteserver*のみを指定した場合は、そのリモートサーバーのすべてのリモートログインがローカルサーバーから削除されます。 *Login*も指定すると、その特定のローカルログインにマップされている*remoteserver*からのすべてのリモートログインが、ローカルサーバーから削除されます。 *Remote_name*も指定されている場合、 *remoteserver*からのリモートユーザーのリモートログインのみがローカルサーバーから削除されます。  
  
 ローカルサーバーユーザーを追加するには、 **sp_addlogin**を使用します。 ローカルサーバーユーザーを削除するには、 **sp_droplogin**を使用します。  
  
 リモート ログインは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用する場合にのみ必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 以降では、代わりにリンク サーバー ログインを使用します。 **Sp_addlinkedsrvlogin**と**sp_droplinkedsrvlogin**を使用して、リンクサーバーのログインを追加および削除します。  
  
 **sp_dropremotelogin** は、ユーザー定義のトランザクション内では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**または**securityadmin**固定サーバーロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. リモートサーバーのすべてのリモートログインを削除する  
 次の例では、リモートサーバーのエントリを削除 `ACCOUNTS` します。したがって、ローカルサーバー上のログインとリモートサーバー上のリモートログインの間のすべてのマッピングが削除されます。  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. ログインマッピングを削除する  
 次の例では、リモート サーバー `ACCOUNTS` からのリモート ログインとローカル ログイン `Albert` をマップしているエントリを削除します。  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. リモートユーザーを削除する  
 次の例では、 `Chris` `ACCOUNTS` ローカルログインにマップされているリモートサーバー上のリモートログインのログインを削除し `salesmgr` ます。  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
