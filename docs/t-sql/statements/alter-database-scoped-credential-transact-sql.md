---
description: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
title: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 00cfd711ce130fa9c90c11000a6853082494e9bd
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124297"
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  データベース スコープ資格情報のプロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *credential_name*  
 変更対象のデータベース スコープ資格情報の名前を指定します。  
  
 IDENTITY **='** _identity_name_*_'_*  
 サーバーの外部に接続するときに使用するアカウントの名前を指定します。 Azure Blob Storage からファイルをインポートするには、ID 名が `SHARED ACCESS SIGNATURE` である必要があります。  Shared Access Signature の詳細については、「[Shared Access Signatures (SAS) の使用](/azure/storage/storage-dotnet-shared-access-signature-part-1)」をご覧ください。  
    
  
 SECRET **='** _secret_*_'_*  
 送信の認証に必要なシークレットを指定します。 "*シークレット*" は、Azure BLOB ストレージからファイルをインポートするために必要です。 "*シークレット*" は、他の目的では省略可能な場合があります。   
> [!WARNING]
>  SAS キーの値は '?' (疑問符) で始まる可能性があります。 SAS キーを使用する場合は、先頭の '?' を削除する必要があります。 そうしないと、作業がブロックされる可能性があります。    
  
## <a name="remarks"></a>解説  
 データベース スコープの資格情報が変更されたとき、*identity_name* の値と "*シークレット*" の値は両方ともリセットされます。 SECRET 引数を省略すると、格納されているシークレットの値は NULL に設定されます。  
  
 シークレットはサービス マスター キーを使用して暗号化されます。 サービス マスター キーが再生成された場合、シークレットは新しいサービス マスター キーを使って再暗号化されます。  
  
 データベース スコープの資格情報に関する情報は、[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) カタログ ビューで確認できます。  
  
## <a name="permissions"></a>アクセス許可  
 資格情報に対する `ALTER` 権限が必須です。  
  
## <a name="examples"></a>例  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. データベース スコープ資格情報のパスワードを変更する  
 次の例では、`Saddles` というデータベース スコープの資格情報に格納されているシークレットを変更します。 データベース スコープの資格情報には、Windows ログインが含まれています。`RettigB` とそのパスワードです。 新しいパスワードには、SECRET 句を使用して、データベース スコープの資格情報が追加されます。  
  
```sql  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 資格情報からパスワードを削除する  
 次の例では、`Frames` というデータベース スコープ資格情報からパスワードを削除します。 データベース スコープの資格情報には、Windows ログインが含まれています。`Aboulrus8` とパスワードです。 ステートメントを実行すると、SECRET オプションが指定されていないので、データベース スコープ資格情報のパスワードは NULL になります。  
  
```sql  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
