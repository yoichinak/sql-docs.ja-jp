---
description: sp_addlogin (Transact-SQL)
title: sp_addlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 585461904b68f26d3ea71e255b24e9ed6d38786a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474562"
---
# <a name="sp_addlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザーが認証を使用してのインスタンスに接続できるようにする新しいログインを作成し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) を使用してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @loginame =] '*login*'  
 ログインの名前を指定します。 *login* は **sysname**,、既定値はありません。  
  
 [ @passwd =] '*パスワード*'  
 ログインパスワードを入力します。 *パスワード* は **sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb =] '*データベース*'  
 ログインの既定のデータベースを指定します (そのログインがログインした後に最初に接続されるデータベース)。 *データベースのデータ* 型は **sysname**で、既定値は **master**です。  
  
 [ @deflanguage =] '*language*'  
 ログインの既定の言語を設定します。 *language* は **sysname**,、既定値は NULL です。 *言語*が指定されていない場合、新しいログインの既定の*言語*は、サーバーの現在の既定の言語に設定されます。  
  
 [ @sid =] '*sid*'  
 セキュリティ ID 番号 (SID) を指定します。 *sid* は **varbinary (16)**,、既定値は NULL です。 *Sid*が NULL の場合、システムは新しいログインの sid を生成します。 **Varbinary**データ型を使用する場合でも、NULL 以外の値は長さが16バイトである必要がありますが、まだ存在していない必要があります。 *Sid*を指定すると、たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] あるサーバーから別のサーバーにログインしたり、ログインを移動したりするときに、複数のサーバーで同じ sid を使用するようにすることができます。  
  
 [ @encryptopt =] '*encryption_option*'  
 パスワードを、クリア テキストとして渡すか、またはクリア テキスト パスワードのハッシュとして渡すかを指定します。 暗号化は行われないことに注意してください。 ここでは、"暗号化" という用語を旧バージョンとの互換性のために使用しています。 クリアテキストのパスワードが渡されると、ハッシュされます。 ハッシュは保存されます。 *encryption_option* は **varchar (20)** で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|NULL|パスワードがクリア テキストで渡されます。 これは既定値です。|  
|**skip_encryption**|パスワードは既にハッシュされています。 は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 再ハッシュせずに値を格納する必要があります。|  
|**skip_encryption_old**|指定されたパスワードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンでハッシュされています。 は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 再ハッシュせずに値を格納する必要があります。 このオプションは、アップグレードのためだけに提供されています。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの長さは 1 ～ 128 文字で、英字、記号、および数字を含めることができます。 ログインには、バックスラッシュ () を含めることはできません。また、 \\ sa や public などの予約済みログイン名を指定するか、既に存在するか、NULL または空の文字列 () を指定して `''` ください。  
  
 既定のデータベースの名前が指定されている場合は、USE ステートメントを実行せずに、指定されたデータベースに接続できます。 ただし、データベース所有者 ( [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) または [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) または [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)を使用してデータベースにアクセスできるようになるまで、既定のデータベースを使用することはできません。  
  
 SID 番号は、サーバーのログインを一意に識別する GUID です。  
  
 サーバーの既定の言語を変更しても、既存のログインに関する既定の言語は変更されません。 サーバーの既定の言語を変更するには、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)を使用します。  
  
 パスワードのハッシュを抑制するために **skip_encryption** を使用すると、ログインがに追加されたときにパスワードが既にハッシュされている場合に便利です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 以前のバージョンのでパスワードがハッシュされている場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **skip_encryption_old**を使用します。  
  
 ユーザー定義のトランザクション内では、sp_addlogin を実行できません。  
  
 次の表は、sp_addlogin と共に使用されるストアド プロシージャを示しています。  
  
|ストアド プロシージャ|説明|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Windows のユーザーまたはグループを追加します。|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|ユーザーのパスワードを変更します。|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|ユーザーの既定のデータベースを変更します。|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|ユーザーの既定の言語を変更します。|  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-sql-server-login"></a>A. SQL Server ログインを作成する  
 次の例では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Victoria` `B1r12-36` 既定のデータベースを指定せずに、というパスワードを使用して、ユーザーのログインを作成します。  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. 既定のデータベースを持つ SQL Server ログインの作成  
 次の例では、パスワードとの既定のデータベースを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーのログインを作成し `Albert` `B5432-3M6` `corporate` ます。  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. 異なる既定の言語を持つ SQL Server ログインの作成  
 次の例では、パスワード `TzTodorov`、既定のデータベース `709hLKH7chjfwv`、および既定の言語 `AdventureWorks2012` を指定して、ユーザー `Bulgarian` の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを作成します。  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. 特定の SID を持つ SQL Server ログインを作成する  
 次の例では、パスワード `Michael`、既定のデータベース `B548bmM%f6`、既定の言語 `AdventureWorks2012`、および SID `us_english` を指定して、ユーザー `0x0123456789ABCDEF0123456789ABCDEF` の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを作成します。  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>参照  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
