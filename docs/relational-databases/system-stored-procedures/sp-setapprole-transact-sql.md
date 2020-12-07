---
description: sp_setapprole (Transact-sql)
title: sp_setapprole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0513878f65513e57a6e26bb52d8101ba6c5d672c
ms.sourcegitcommit: 2144a22ad4380182133e87664a907fe6f06b5f95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2020
ms.locfileid: "94570959"
---
# <a name="sp_setapprole-transact-sql"></a>sp_setapprole (Transact-sql)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベースのアプリケーションロールに関連付けられている権限をアクティブにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>引数

`[ @rolename = ] 'role'` 現在のデータベースで定義されているアプリケーションロールの名前を指定します。 *role* の型は **sysname** で、既定値はありません。 *ロール* は現在のデータベースに存在している必要があります。  
  
`[ @password = ] { encrypt N'password' }` アプリケーションロールをアクティブ化するために必要なパスワードを指定します。 *パスワード* は **sysname** ,、既定値はありません。 ODBC **encrypt** 関数を使用すると、 *パスワード* を難読化できます。 **Encrypt** 関数を使用する場合は、最初の引用符の前に **N** を配置することで、パスワードを Unicode 文字列に変換する必要があります。  
  
 [暗号化] オプションは、 **SqlClient** を使用している接続ではサポートされていません。  
  
> [!IMPORTANT]  
> ODBC **encrypt** 関数では、暗号化は提供されません。 ネットワーク経由で転送されるパスワードを保護するために、この機能に依存しないでください。 この情報がネットワーク経由で送信される場合は、TLS または IPSec を使用します。
  
 **@encrypt = ' none '**  
 暗号化を使用しないことを示します。 パスワードはプレーンテキストとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に渡されます。 これは既定値です。  
  
 **@encrypt= ' odbc '**  
 Odbc がパスワードをに送信する前に ODBC **encrypt** 関数を使用してパスワードを難読化することを指定し [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ます。 これは、ODBC クライアントまたは OLE DB Provider for SQL Server のいずれかを使用している場合にのみ指定できます。  
  
`[ @fCreateCookie = ] true | false` クッキーを作成するかどうかを指定します。 **true** は、暗黙的に1に変換されます。 **false** は暗黙的に0に変換されます。  
  
`[ @cookie = ] @cookie OUTPUT` クッキーを格納する出力パラメーターを指定します。 クッキーは、 **\@ fCreateCookie** の値が **true** の場合にのみ生成されます。 **varbinary(8000)**  
  
> [!NOTE]  
> **sp_setapprole** のクッキーの **OUTPUT** パラメーターは現在、適切な最大長である **varbinary(8000)** としてドキュメントに記載されています。 ただし、現在の実装では **varbinary(50)** を返します。 アプリケーションは、今後のリリースでクッキーの戻り値のサイズが増加した場合にアプリケーションが引き続き正常に動作するように、 **varbinary (8000)** を引き続き予約する必要があります。
  
## <a name="return-code-values"></a>リターン コードの値

 0 (成功) と 1 (失敗)  
  
## <a name="remarks"></a>注釈

 **Sp_setapprole** を使用してアプリケーションロールをアクティブ化した後は、ユーザーがサーバーとの接続を切断するか **sp_unsetapprole** を実行するまで、ロールはアクティブのままになります。 **sp_setapprole** は、直接の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、アドホックレベル、およびユーザー定義のトランザクション内ではなく、アドホックレベルでのみ実行できます。  
  
 アプリケーションロールの概要については、「 [アプリケーションロール](../../relational-databases/security/authentication-access/application-roles.md)」を参照してください。  
  
> [!IMPORTANT]  
> ネットワーク経由で転送されるときにアプリケーションロールのパスワードを保護するには、アプリケーションロールを有効にするときに、常に暗号化された接続を使用する必要があります。
> [!INCLUDE[msCoName](../../includes/msconame-md.md)]ODBC の **encrypt** オプションは、 **SqlClient** ではサポートされていません。 資格情報を格納する必要がある場合は、Crypto API 関数を使用して暗号化します。 パラメーターの *パスワード* は、一方向のハッシュとして格納されます。 以前のバージョンのとの互換性を維持するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **sp_addapprole** によってパスワードの複雑さのポリシーは適用されません。 パスワードの複雑さのポリシーを適用するには、[ [アプリケーションロールの作成](../../t-sql/statements/create-application-role-transact-sql.md)] を使用します。  
  
## <a name="permissions"></a>アクセス許可

**Public** のメンバーシップと、ロールのパスワードに関する知識が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. 暗号化オプションを使用せずにアプリケーションロールをアクティブ化する

 次の例では、アプリケーション ロール `SalesAppRole` をアクティブにします。このロールには、プレーンテキストのパスワード `AsDeF00MbXX` が設定されており、現在のユーザーが使用するアプリケーション用に特別に設計された権限が与えられています。

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. Cookie を使用してアプリケーションロールをアクティブ化し、元のコンテキストに戻す

 次の例では、パスワード `Sales11` が設定されているアプリケーション ロール `fdsd896#gfdbfdkjgh700mM` をアクティブ化し、クッキーを作成します。 この例では、現在のユーザーの名前が返されます。その後、`sp_unsetapprole` を実行して元のコンテキストに戻します。  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>参照

 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_unsetapprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
