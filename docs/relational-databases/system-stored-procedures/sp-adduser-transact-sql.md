---
description: sp_adduser (Transact-sql)
title: sp_adduser (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 05aa08ee4d2b518b804db93d5a2408f690b56bbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464604"
---
# <a name="sp_adduser-transact-sql"></a>sp_adduser (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに新しいユーザーを追加します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインまたは Windows ログインの名前を指定します。 *login* は **sysname**であり、既定値はありません。 *ログイン* には、既存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログインまたは Windows ログインを指定する必要があります。  
  
`[ @name_in_db = ] 'user'` 新しいデータベースユーザーの名前を指定します。 *user* は **sysname**,、既定値は NULL です。 *User*が指定されていない場合、新しいデータベースユーザーの名前は既定で*ログイン*名になります。 *ユーザー*を指定すると、新しいユーザーには、サーバーレベルのログイン名とは異なる名前が付けられます。  
  
`[ @grpname = ] 'role'` 新しいユーザーがメンバーになるデータベースロールを指定します。 *role* の部分は **sysname**で、既定値は NULL です。 *ロール* は、現在のデータベースの有効なデータベースロールである必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 また、 **sp_adduser**では、ユーザーの名前を持つスキーマも作成されます。  
  
 ユーザーが追加されたら、GRANT、DENY、および REVOKE ステートメントを使用して、ユーザーが実行するアクティビティを制御するアクセス許可を定義します。  
  
 有効なログイン名の一覧を表示するには、 **server_principals** を使用します。  
  
 **Sp_helprole**を使用して、有効なロール名の一覧を表示します。 ロールを指定すると、そのロールに対して定義されている権限が自動的にユーザーに与えられます。 ロールが指定されていない場合は、既定の **public** ロールに付与されている権限がユーザーに与えられます。 ユーザーをロールに追加するには、 *ユーザー名* の値を指定する必要があります。 (*ユーザー名* は *login_id*と同じにすることができます)。  
  
 ユーザー **guest** はすべてのデータベースに既に存在します。 ユーザー **ゲスト** を追加すると、このユーザーが既に無効になっている場合に有効になります。 既定では、ユーザー **guest** は新しいデータベースで無効になっています。  
  
 **sp_adduser** は、ユーザー定義のトランザクション内では実行できません。  
  
 Guest ユーザーは、**すべてのデータベース**内に既に存在するため、**ゲスト**ユーザーを追加することはできません。 **ゲスト**ユーザーを有効にするには、次のように**ゲスト**接続のアクセス許可を付与します。  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>アクセス許可  
 データベースの所有権が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-adding-a-database-user"></a>A. データベースユーザーの追加  
 次の例では、 `Vidur` 既存のログインを `Recruiting` 使用して、現在のデータベースの既存のロールにデータベースユーザーを追加し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Vidur` ます。  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. 同じログイン ID を持つデータベースユーザーを追加する  
 次の例では、ユーザー `Arvind` を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログイン `Arvind` として現在のデータベースに追加します。 このユーザーは、既定の **public** ロールに属しています。  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. サーバーレベルのログインとは異なる名前のデータベースユーザーを追加する  
 次の例で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は `BjornR` 、ユーザー名がである現在のデータベースにログインを追加し、データベース `Bjorn` ユーザーを `Bjorn` データベースロールに追加し `Production` ます。  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
