---
description: REVOKE (非対称キーの権限の取り消し) (Transact-SQL)
title: REVOKE (非対称キーの権限の取り消し) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- REVOKE statement, asymmetric keys
ms.assetid: 1a1063e8-ffc7-4775-a40d-e155740ad7b2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54c17df591c9e4364d2efa037e6072fa4024dce6
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88496628"
---
# <a name="revoke-asymmetric-key-permissions-transact-sql"></a>REVOKE (非対称キーの権限の取り消し) (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  非対称キーの権限を取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
  
REVOKE [ GRANT OPTION FOR ] { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 GRANT OPTION FOR  
 指定した権限を与える許可を取り消すことを示します。  
  
> [!IMPORTANT]  
>  指定した権限が GRANT オプションなしでプリンシパルに許可されている場合は、その権限自体が取り消されます。  
  
 *permission*  
 アセンブリで取り消すことができる権限を指定します。 以下に一覧を示します。  
  
 ON ASYMMETRIC KEY **::** _asymmetric_key_name_  
 権限を取り消す非対称キーを指定します。 スコープ修飾子 **::** が必要です。  
  
 *database_principal*  
 権限を取り消すプリンシパルを指定します。 次のいずれかになります。  
  
-   データベース ユーザー  
  
-   データベース ロール  
  
-   アプリケーション ロール  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
 CASCADE  
 このプリンシパルによって権限が許可または拒否されている他のプリンシパルからも、同じ権限が取り消されることを示します。 権限自体は取り消されません。  
  
> [!CAUTION]  
>  WITH GRANT OPTION で許可されている権限を CASCADE で取り消すと、その権限の GRANT および DENY の両方が取り消されます。  
  
 AS *revoking_principal*  
 このクエリを実行するプリンシパルが権限を取り消す権利を取得した、元のプリンシパルを指定します。 次のいずれかになります。  
  
-   データベース ユーザー  
  
-   データベース ロール  
  
-   アプリケーション ロール  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>注釈  
 非対称キーは、データベース レベルの保護可能なアイテムで、権限の階層で親となっているデータベースに含まれています。 次に、非対称キーで取り消すことができる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|非対称キーの権限|権限が含まれる非対称キー権限|権限が含まれるデータベース権限|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 非対称キーに対する CONTROL 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
