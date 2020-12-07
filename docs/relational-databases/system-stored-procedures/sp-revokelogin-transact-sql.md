---
description: sp_revokelogin (Transact-sql)
title: sp_revokelogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f2ccd140079e9a585ee67ce1b7c2208b9926f963
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446772"
---
# <a name="sp_revokelogin-transact-sql"></a>sp_revokelogin (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CREATE login、 **sp_grantlogin**、または**sp_denylogin**を使用して作成された Windows ユーザーまたはグループに対して、からログインエントリを削除します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login'` Windows ユーザーまたはグループの名前を指定します。 *login* は **sysname**,、既定値はありません。 *ログイン*には、*コンピューター名* \\ *ユーザーまたはドメイン* \\ *ユーザー*の形式で、既存の Windows ユーザー名またはグループを指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_revokelogin** は、 *login* パラメーターで指定されたアカウントを使用した接続を無効にします。 ただし、Windows グループのメンバーシップによってのインスタンスへのアクセスが許可されている Windows ユーザー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、個別のアクセスが取り消された後もグループとして接続できます。 同様に、 *login* パラメーターで Windows グループの名前を指定した場合、そのグループのメンバーはのインスタンスへのアクセスが個別に許可されていて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] も接続できます。  
  
 たとえば、Windows ユーザー **ADVWORKS\john** が windows グループ **ADVWORKS\Admins**のメンバーである場合、 **sp_revokelogin** は次のアクセス権を取り消し `ADVWORKS\john` ます。  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 ユーザー **ADVWORKS\john** は、 **ADVWORKS\Admins** にのインスタンスへのアクセスが許可されている場合でも接続でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 同様に、Windows グループ **ADVWORKS\Admins** のアクセスが取り消されても、 **ADVWORKS\john** にアクセス権が付与されている場合、 **ADVWORKS\john** は引き続き接続できます。  
  
 **Sp_denylogin**を使用すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Windows グループメンバーシップに関係なく、ユーザーがのインスタンスに明示的に接続するのを防ぐことができます。  
  
 **sp_revokelogin** は、ユーザー定義のトランザクション内では実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、Windows ユーザーのログインエントリを削除し `Corporate\MollyA` ます。  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 または  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のログインを削除します。 ](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
