---
description: sp_change_users_login (Transact-sql)
title: sp_change_users_login (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c82241030646e2ef20c978cb1905cf836f9a589b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447414"
---
# <a name="sp_change_users_login-transact-sql"></a>sp_change_users_login (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  既存のデータベースユーザーをログインにマップ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 
  
 > [!IMPORTANT]
 > [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) を使用してください。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @Action =] '*action*'  
 プロシージャにより実行されるアクションの説明です。 *action* は **varchar (10)** です。 *アクション* には、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**Auto_Fix**|現在のデータベース内の sys.database_principals システム カタログ ビューにあるユーザー エントリを、同じ名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインにリンクします。 同じ名前のログインが存在しない場合は、新しく作成されます。 **Auto_Fix**ステートメントの結果を調べて、正しいリンクが実際に作成されていることを確認します。 セキュリティを重視する状況では **Auto_Fix** を使用しないようにしてください。<br /><br /> **Auto_Fix**を使用する場合は、ログインがまだ存在しない場合は*ユーザー*と*パスワード*を指定する必要があります。そうでない場合は、*ユーザー*を指定する必要がありますが、*パスワード*は無視されます。 *ログイン* は NULL にする必要があります。 *ユーザー* は、現在のデータベースの有効なユーザーである必要があります。 ログインに別のユーザーをマップすることはできません。|  
|**Report**|現在のデータベース内で、どのログインにもリンクされていないユーザーと、対応するセキュリティ識別子 (SID) を一覧表示します。 *ユーザー*、 *ログイン*、および *パスワード* は NULL であるか、指定されていません。<br /><br /> システムテーブルを使用するクエリでレポートオプションを置き換えるには、 **server_prinicpals** 内のエントリを、 **database_principals**のエントリと比較します。|  
|**Update_One**|現在のデータベース内の指定された *ユーザー* を既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *ログイン*にリンクします。 *ユーザー* と *ログイン* を指定する必要があります。 *パスワード* は NULL であるか、指定されていません。|  
  
 [ @UserNamePattern =] '*ユーザー*'  
 現在のデータベース内のユーザーの名前を指定します。 *user* の部分は **sysname**で、既定値は NULL です。  
  
 [ @LoginName =] '*login*'  
 ログインの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
 [ @Password =] '*パスワード*'  
 Auto_Fix を指定して作成された新しいログインに割り当てられたパスワードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定します。 **Auto_Fix** 一致するログインが既に存在する場合、ユーザーとログインはマップされ、 *パスワード* は無視されます。 一致するログインが存在しない場合、sp_change_users_login によって新しいログインが作成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *パスワード* が新しいログインのパスワードとして割り当てられます。 *パスワード* は **sysname**であり、NULL にすることはできません。  
  
> **重要!!** 常に[強力なパスワード](../../relational-databases/security/strong-passwords.md)を使用してください。
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|データベースユーザー名。|  
|UserSID|**varbinary (85)**|ユーザーのセキュリティ識別子。|  
  
## <a name="remarks"></a>解説  
 sp_change_users_login は、現在のデータベースのデータベース ユーザーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとリンクする場合に使用します。 ユーザーのログインが既に変更されている場合は、sp_change_users_login を使用してユーザーを新しいログインにリンクすれば、ユーザーの権限が失われることはありません。 新しい *ログイン* を sa にすることはできません。また、 *ユーザー* を dbo、guest、または INFORMATION_SCHEMA ユーザーにすることはできません。  
  
 sp_change_users_login は、データベース ユーザーを Windows レベルのプリンシパル、証明書、または非対称キーにマップする場合は使用できません。  
  
 sp_change_users_login は、Windows プリンシパルから作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインや、CREATE USER WITHOUT LOGIN を使用して作成されたユーザーでは使用できません。  
  
 ユーザー定義のトランザクション内では、sp_change_users_login は実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。 **Auto_Fix**オプションを指定できるのは、sysadmin 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. 現在のユーザーとログインの対応関係を示すレポートを表示する  
 次の例では、現在のデータベース内のユーザーと各ユーザーのセキュリティ識別子 (SID) を示すレポートを作成します。  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. 新しい SQL Server ログインへのデータベースユーザーのマッピング  
 次の例では、データベースユーザーが新しいログインに関連付けられて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] います。 `MB-Sales`最初に別のログインにマップされるデータベースユーザーは、ログインに再マップされ `MaryB` ます。  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. ユーザーをログインに自動的にマップし、必要に応じて新しいログインを作成する  
 次の例では、を使用して、 `Auto_Fix` 既存のユーザーを同じ名前のログインにマップする方法、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが存在しない場合にパスワードを持つログインを作成する方法を示し `Mary` `B3r12-3x$098f6` `Mary` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
