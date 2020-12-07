---
description: sp_update_proxy (Transact-sql)
title: sp_update_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 052f78652c02b7486d930dbb7071a6b2a981074b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473499"
---
# <a name="sp_update_proxy-transact-sql"></a>sp_update_proxy (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  既存のプロキシのプロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_id = ] id` 変更するプロキシのプロキシ識別番号を指定します。 *Proxy_id*は**int**,、既定値は NULL です。  
  
`[ @proxy_name = ] 'proxy_name'` 変更するプロキシの名前。 *Proxy_name*は**sysname**で、既定値は NULL です。  
  
`[ @credential_name = ] 'credential_name'` プロキシの新しい資格情報の名前。 *Credential_name*は**sysname**で、既定値は NULL です。 *Credential_name*または*credential_id*のいずれかを指定できます。  
  
`[ @credential_id = ] credential_id` プロキシの新しい資格情報の識別番号を指定します。 *Credential_id*は**int**,、既定値は NULL です。 *Credential_name*または*credential_id*のいずれかを指定できます。  
  
`[ @new_name = ] 'new_name'` プロキシの新しい名前。 *New_name*は**sysname**で、既定値は NULL です。 このプロシージャを指定すると、プロキシの名前が *new_name*に変更されます。 この引数が NULL の場合、プロキシの名前は変更されません。  
  
`[ @enabled = ] is_enabled` プロキシが有効かどうかを指定します。 *Is_enabled*フラグは**tinyint**,、既定値は NULL です。 *Is_enabled*が**0**の場合、プロキシは有効ではなく、ジョブステップでは使用できません。 この引数が NULL の場合、プロキシの状態は変更されません。  
  
`[ @description = ] 'description'` プロキシの新しい説明。 *説明*は**nvarchar (512)**,、既定値は NULL です。 この引数が NULL の場合、プロキシの説明は変更されません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 ** \@ Proxy_name**または** \@ proxy_id**のいずれかを指定する必要があります。 両方の引数を指定する場合は、両方とも同じプロキシを参照する必要があります。異なるプロキシを参照する場合、ストアド プロシージャは失敗します。  
  
 プロキシの資格情報を変更するには、 ** \@ credential_name**または** \@ credential_id**のいずれかを指定する必要があります。 両方の引数を指定する場合は、両方とも同じ資格情報を参照する必要があります。異なる資格情報を参照する場合、ストアド プロシージャは失敗します。  
  
 このプロシージャでプロキシが変更されますが、プロキシへのアクセスは変更されません。 プロキシへのアクセスを変更するには、 **sp_grant_login_to_proxy** と **sp_revoke_login_from_proxy**を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定セキュリティロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、プロキシ `Catalog application proxy` の enabled の値を `0` に設定します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server エージェントセキュリティを実装する](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
