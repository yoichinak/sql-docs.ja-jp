---
description: sp_grant_login_to_proxy (Transact-sql)
title: sp_grant_login_to_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: e5e1c8ad821aeee5eff2a7671636941bad816405
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493285"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-sql)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プロキシへのセキュリティプリンシパルアクセスを許可します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>引数  
`[ @login_name = ] 'login_name'` アクセス権を付与するログイン名。 *Login_name*は**nvarchar (256)**,、既定値は NULL です。 ** \@ Login_name**、 ** \@ fixed_server_role**、または** \@ msdb_role**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
`[ @fixed_server_role = ] 'fixed_server_role'` アクセス権を付与する固定サーバーロール。 *Fixed_server_role*は**nvarchar (256)**,、既定値は NULL です。 ** \@ Login_name**、 ** \@ fixed_server_role**、または** \@ msdb_role**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
`[ @msdb_role = ] 'msdb_role'` アクセスを許可する **msdb** データベースのデータベースロール。 *Msdb_role*は**nvarchar (256)**,、既定値は NULL です。 ** \@ Login_name**、 ** \@ fixed_server_role**、または** \@ msdb_role**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
`[ @proxy_id = ] id` アクセス権を付与するプロキシの識別子。 *Id*は**int**,、既定値は NULL です。 ** \@ Proxy_id**または** \@ proxy_name**のいずれかを指定する必要があります。指定しない場合、ストアドプロシージャは失敗します。  
  
`[ @proxy_name = ] 'proxy_name'` アクセス権を付与するプロキシの名前。 *Proxy_name*は**nvarchar (256)**,、既定値は NULL です。 ** \@ Proxy_id**または** \@ proxy_name**のいずれかを指定する必要があります。指定しない場合、ストアドプロシージャは失敗します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_grant_login_to_proxy** は、 **msdb** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_grant_login_to_proxy**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、ログイン `adventure-works\terrid` に対してプロキシ `Catalog application proxy` の使用を許可します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
