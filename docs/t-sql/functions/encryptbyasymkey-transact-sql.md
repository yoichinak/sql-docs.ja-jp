---
description: ENCRYPTBYASYMKEY (Transact-SQL)
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 42ffb61535beefeee149124adf7873cce78c1535
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128505"
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

この関数は非対称キーでデータを暗号化します。  
  
 ![記事リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*asym_key_ID*  
データベース内の非対称キーの ID。 *asym_key_ID* には、**int** データ型が与えられます。  
  
*cleartext*  
`ENCRYPTBYASYMKEY` が非対称キーで暗号化するデータの文字列。 *cleartext* のデータ型には
 
+ **[バイナリ]**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
or
  
+ **varchar**
 
があります。  
  
**\@plaintext**  
`ENCRYPTBYASYMKEY` が非対称キーで暗号化する値を保持する変数。 **\@plaintext** のデータ型には
  
+ **[バイナリ]**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
or
  
+ **varchar**
 
があります。  
  
## <a name="return-types"></a>戻り値の型  
最大サイズが 8,000 バイトの **varbinary**。  
  
## <a name="remarks"></a>解説  
非対称キーを使用する暗号化操作と復号操作は大量のリソースを消費します。そのため、対称キーの暗号化と復号に比べ、高くつきます。 データベース テーブルに格納されているユーザー データ データベースなど、データセットが大規模になる場合、非対称キーで暗号化/復号することは開発者にお勧めしていません。 代わりに、強力な対称キーでデータを暗号化し、その対称キーを非対称キーで暗号化することをお勧めしています。  
  
アルゴリズムにもよりますが、`ENCRYPTBYASYMKEY` は、入力が特定のバイト数を超えると、**NULL** を返します。 具体的な制限:

+ 512 ビット RSA キーで暗号化できるのは 53 バイトまで
+ 1024 ビット キーで暗号化できるのは 117 バイトまで
+ 2048 ビット キーで暗号化できるのは 245 バイトまで

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、証明書と非対称キーの両方が RSA キーのラッパーとして機能します。  
  
## <a name="examples"></a>例  
この例では、`@cleartext` に格納されているテキストを非対称キー `JanainaAsymKey02` を使用して暗号化します。 このステートメントは、`ProtectedData04` テーブルに暗号化されたデータを挿入します。  
  
```sql  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
