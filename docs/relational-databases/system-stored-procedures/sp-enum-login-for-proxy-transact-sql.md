---
description: sp_enum_login_for_proxy (Transact-SQL)
title: sp_enum_login_for_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 7707843979bd0c741ade8e4ae6759d265eb13d06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486062"
---
# <a name="sp_enum_login_for_proxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  セキュリティプリンシパルとプロキシ間の関連付けを一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロキシを一覧表示するプリンシパル、ログイン、サーバーロール、または**msdb**データベースロールの名前を指定します。 名前は **nvarchar (256)**,、既定値は NULL です。  
  
`[ @proxy_id = ] id` 情報を一覧表示するプロキシのプロキシ識別番号を指定します。 *Proxy_id*は**int**,、既定値は NULL です。 *Id*または*proxy_name*を指定できます。  
  
`[ @proxy_name = ] 'proxy_name'` 情報を一覧表示するプロキシの名前。 *Proxy_name*は**sysname**で、既定値は NULL です。 *Id*または*proxy_name*を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|プロキシの識別番号。|  
|**proxy_name**|**sysname**|プロキシの名前。|  
|**name**|**sysname**|関連付けのセキュリティプリンシパルの名前。|  
|**flags**|**int**|セキュリティ プリンシパルの種類<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン<br /><br /> **1** = 固定システムロール<br /><br /> **2** = **msdb**のデータベースロール|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>解説  
 パラメーターが指定されていない場合、 **sp_enum_login_for_proxy** は、すべてのプロキシのインスタンス内のすべてのログインに関する情報を一覧表示します。  
  
 プロキシ id またはプロキシ名を指定すると、 **sp_enum_login_for_proxy** プロキシにアクセスできるログインが一覧表示されます。 ログイン名が指定されている場合、 **sp_enum_login_for_proxy** には、そのログインがアクセスできるプロキシが一覧表示されます。  
  
 プロキシ情報とログイン名の両方を指定すると、指定されたログインに指定されたプロキシへのアクセス権がある場合は、結果セットから行が返されます。  
  
 このストアドプロシージャは **msdb**にあります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-associations"></a>A. すべての関連付けを一覧表示する  
 次の例では、現在のインスタンスのログインとプロキシの間に確立されたすべてのアクセス許可を一覧表示します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. 指定したログインに対するプロキシを一覧表示する  
 次の例では、ログイン `terrid` がアクセスできるプロキシを一覧表示します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_help_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
