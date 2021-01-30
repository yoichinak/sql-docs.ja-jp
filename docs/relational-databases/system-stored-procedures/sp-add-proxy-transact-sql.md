---
description: sp_add_proxy (Transact-SQL)
title: sp_add_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c60c3bb1ea9f96352662b72080afbfa1e76b1dce
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99192395"
---
# <a name="sp_add_proxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたエージェントプロキシを追加し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_name = ] 'proxy_name'` 作成するプロキシの名前。 *Proxy_name* は **sysname** で、既定値は NULL です。 *Proxy_name* が NULL または空の文字列の場合、プロキシの名前は既定で指定 *user_name* に設定されます。  
  
`[ @enabled = ] is_enabled` プロキシが有効かどうかを指定します。 *Is_enabled* フラグは **tinyint**,、既定値は1です。 *Is_enabled* が **0** の場合、プロキシは有効ではなく、ジョブステップでは使用できません。  
  
`[ @description = ] 'description'` プロキシの説明。 説明は **nvarchar (512)**,、既定値は NULL です。 この説明はプロキシを記述する場合の参照情報として利用できますが、それ以外の目的では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによってこの説明が使用されることはありません。 このため、この引数は省略可能です。  
  
`[ @credential_name = ] 'credential_name'` プロキシの資格情報の名前。 *Credential_name* は **sysname** で、既定値は NULL です。 *Credential_name* または *credential_id* のいずれかを指定する必要があります。  
  
`[ @credential_id = ] credential_id` プロキシの資格情報の識別番号を指定します。 *Credential_id* は **int**,、既定値は NULL です。 *Credential_name* または *credential_id* のいずれかを指定する必要があります。  
  
`[ @proxy_id = ] id OUTPUT` 正常に作成された場合にプロキシに割り当てられたプロキシ id 番号。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 このストアドプロシージャは、 **msdb** データベースで実行する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシは、[!INCLUDE[tsql](../../includes/tsql-md.md)] サブシステム以外のサブシステムが含まれるジョブ ステップのセキュリティを管理します。 各プロキシには対応するセキュリティ資格情報が 1 つあります。 プロキシは、任意の数のサブシステムにアクセスする可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定セキュリティロールのメンバーだけです。  
  
 **Sysadmin** 固定セキュリティロールのメンバーは、任意のプロキシを使用するジョブステップを作成できます。 ストアドプロシージャ sp_grant_login_to_proxy 使用して、 [transact-sql&#41;&#40;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) し、他のログインにプロキシへのアクセスを許可します。  
  
## <a name="examples"></a>例  
 この例では、資格情報のプロキシを作成し `CatalogApplicationCredential` ます。 このコードは、資格情報が既に存在することを前提としています。 資格情報の詳細については、「 [CREATE CREDENTIAL &#40;transact-sql&#41;](../../t-sql/statements/create-credential-transact-sql.md)」を参照してください。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
