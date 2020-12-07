---
description: sp_msx_set_account (Transact-sql)
title: sp_msx_set_account (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_set_account
- sp_msx_set_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_set_account
ms.assetid: 314ec720-3a37-48f7-bb6b-8d5b894bf843
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f9329879f37ee8508f45f4734a0968596348d5cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535065"
---
# <a name="sp_msx_set_account-transact-sql"></a>sp_msx_set_account (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ターゲット サーバーに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター サーバーのアカウント名とパスワードを設定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>引数  
`[ @credential_name = ] 'credential_name'` マスターサーバーへのログインに使用する資格情報の名前。 既存の資格情報の名前を指定する必要があります。 *Credential_name*または*credential_id*のいずれかを指定する必要があります。  
  
`[ @credential_id = ] credential_id` マスターサーバーへのログインに使用する資格情報の識別子。 既存の資格情報の識別子を指定する必要があります。 *Credential_name*または*credential_id*のいずれかを指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、資格情報を使用して、対象サーバーがマスターサーバーへのログインに使用するユーザー名とパスワードの情報を格納します。 このプロシージャでは、ターゲット サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがマスター サーバーへのログインで使用する資格情報を設定します。  
  
 既存の資格情報を指定する必要があります。 資格情報の作成の詳細については、「 [CREATE credential &#40;transact-sql&#41;](../../t-sql/statements/create-credential-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_msx_set_account**の実行権限は、既定では**sysadmin**固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、マスター サーバーへのログインで資格情報 `MsxAccount` を使用するように、サーバーを設定します。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_get_account &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  
