---
description: xp_grantlogin (Transact-sql)
title: xp_grantlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 185532cdcade18b6902fe1c3e8d1c8ab3eb568b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419266"
---
# <a name="xp_grantlogin-transact-sql"></a>xp_grantlogin (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Windows グループまたはユーザーにへのアクセスを許可 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login'` 追加する Windows ユーザーまたはグループの名前を指定します。 Windows ユーザーまたはグループは、*ドメイン*ユーザーという形式の windows ドメイン名で修飾されている必要があり \\ *User*ます。 *login* は **sysname**,、既定値はありません。  
  
`[ @logintype = ] 'logintype'` アクセス権が付与されているログインのセキュリティレベルを示します。 *logintype* は **varchar (5)**,、既定値は NULL です。 指定できるのは **管理者** だけです。 **Admin**を指定した場合、*ログイン*にはへのアクセスが許可され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin**固定サーバーロールのメンバーとして追加されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **xp_grantlogin** は、拡張ストアドプロシージャではなく、システムストアドプロシージャになりました。 **xp_grantlogin** は **sp_grantlogin** と **sp_addsrvrolemember**を呼び出します。  
  
## <a name="permissions"></a>アクセス許可  
 **Securityadmin**固定サーバーロールのメンバーシップが必要です。 *Logintype*を変更する場合は、 **sysadmin**固定サーバーロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;の一般的な拡張ストアドプロシージャ ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
