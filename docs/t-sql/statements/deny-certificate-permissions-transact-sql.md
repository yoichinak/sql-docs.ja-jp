---
description: DENY (証明書の権限の拒否) (Transact-SQL)
title: DENY (証明書の権限の拒否) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], permissions
- permissions [SQL Server], certificates
- DENY statement, certificates
- denying permissions [SQL Server], certificates
ms.assetid: 5971ff9e-d6a4-414b-ae1f-819bc2e348f5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6c4f113333b276ac976e56c43647249ddbe77aac
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99177745"
---
# <a name="deny-certificate-permissions-transact-sql"></a>DENY (証明書の権限の拒否) (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  証明書に対する権限を拒否します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
  
DENY permission  [ ,...n ]   
    ON CERTIFICATE :: certificate_name   
    TO principal [ ,...n ]  
    [ CASCADE ]  
    [ AS denying_principal ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *permission*  
 証明書に対して拒否できる権限を指定します。 以下に一覧を示します。  
  
 ON CERTIFICATE **::** _certificate_name_  
 権限を拒否する証明書を指定します。 スコープ修飾子 "::" が必要です。  
  
 *database_principal*  
 権限を拒否するプリンシパルを指定します。 次のいずれかになります。  
  
-   データベース ユーザー  
  
-   データベース ロール (database role)  
  
-   アプリケーション ロール (application role)  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
 CASCADE  
 このプリンシパルによって権限が許可されている他のプリンシパルに対しても、同じ権限を拒否することを示します。  
  
 *denying_principal*  
 このクエリを実行するプリンシパルが権限を拒否する権利を取得した、元のプリンシパルを指定します。 次のいずれかになります。  
  
-   データベース ユーザー  
  
-   データベース ロール (database role)  
  
-   アプリケーション ロール (application role)  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>注釈  
 証明書は、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次に、証明書で拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に一覧で示します。  
  
|証明書の権限|権限が含まれる証明書権限|権限が含まれるデータベース権限|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CERTIFICATE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 証明書に対する CONTROL 権限が必要です。 AS 句が使用されている場合、指定したプリンシパルが証明書を所有している必要があります。  
  
## <a name="see-also"></a>参照  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
