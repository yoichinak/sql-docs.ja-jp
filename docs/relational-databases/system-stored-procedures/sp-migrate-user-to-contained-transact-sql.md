---
description: sp_migrate_user_to_contained (Transact-SQL)
title: sp_migrate_user_to_contained (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: edabb8a59a672c3ebfe04a799df7901b402fb5b3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543196"
---
# <a name="sp_migrate_user_to_contained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログインにマップされているデータベースユーザーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、パスワードを持つ包含データベースユーザーに変換します。 包含データベースでは、データベースがインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの依存関係を削除するには、このプロシージャを使用します。 **sp_migrate_user_to_contained** では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パスワードや既定の言語などの設定を包含データベースに対して個別に管理できるように、ユーザーを元のログインから分離します。 **sp_migrate_user_to_contained** は、包含データベースをの別のインスタンスに移動する前に、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 現在のインスタンスログインに対する依存関係をなくすために使用でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!NOTE]
> 効果を逆にすることはできないため、 **sp_migrate_user_to_contained**を使用する場合は注意してください。 このプロシージャは、包含データベースでのみ使用されます。 詳細については、「 [包含データベース](../../relational-databases/databases/contained-databases.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>引数  
 [** @username =** ] **N '***ユーザー***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインにマップされた、現在の包含データベースのユーザーの名前を指定します。 値は **sysname**,、既定値は **NULL**です。  
  
 [** @rename =** ] **N '***copy_login_name***'**  | **N '***keep_name***'**  
 ログインに基づくデータベースユーザーがログイン名とは異なるユーザー名を持っている場合は、 *keep_name* を使用して、移行中にデータベースユーザー名を保持します。 *Copy_login_name*を使用して、ユーザーではなく、ログインの名前を持つ新しい包含データベースユーザーを作成します。 ログインに基づくデータベース ユーザーがログイン名と同じユーザー名を持つ場合は、どちらのオプションでも、名前を変更することなく包含データベース ユーザーが作成されます。  
  
 [** @disablelogin =** ] **N '***disable_login***'**  | **N '***do_not_disable_login***'**  
 *disable_login* 、master データベース内のログインを無効にします。 ログインが無効になっているときに接続するには、接続文字列の一部として、包含データベース名を **初期カタログ** として指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_migrate_user_to_contained** は、ログインのプロパティまたは権限に関係なく、パスワードを持つ包含データベースユーザーを作成します。 たとえば、ログインが無効になっている場合、またはデータベースへの **CONNECT** 権限がユーザーに拒否された場合、プロシージャは成功します。  
  
 **sp_migrate_user_to_contained** には次の制限があります。  
  
-   データベース内に存在しないユーザー名を指定する必要がある。  
  
-   Dbo や guest などの組み込みユーザーは変換できません。  
  
-   ユーザーを、署名されたストアドプロシージャの **EXECUTE as** 句で指定することはできません。  
  
-   ユーザーは、 **EXECUTE AS OWNER** 句を含むストアドプロシージャを所有することはできません。  
  
-   **sp_migrate_user_to_contained** をシステムデータベースで使用することはできません。  
  
## <a name="security"></a>セキュリティ  
 ユーザーを移行する場合は、のインスタンスからすべての管理者ログインを無効にしたり削除したりしないように注意して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ください。 すべてのログインが削除された場合は、「 [システム管理者がロックアウトされた場合の SQL Server への接続](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)」を参照してください。  
  
 **BUILTIN\Administrators**ログインが存在する場合、管理者は [**管理者として実行**] オプションを使用してアプリケーションを起動して接続できます。  
  
### <a name="permissions"></a>アクセス許可  
 **CONTROL SERVER** 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-migrating-a-single-user"></a>A. 単一のユーザーを移行する  
 次の例では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、という名前のログインを `Barry` 、パスワードを持つ包含データベースユーザーに移行します。 この例では、ユーザー名を変更しません。ログインは有効として保持されます。  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. ログインのあるすべてのデータベースユーザーを、ログインのない包含データベースユーザーに移行する  
 次の例では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに基づくすべてのユーザーを、パスワードを持つ包含データベース ユーザーに移行します。 有効になっていないログインは除外します。 この例は、包含データベースで実行する必要があります。  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>参照  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [包含データベース](../../relational-databases/databases/contained-databases.md)  
  
  
