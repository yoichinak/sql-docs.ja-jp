---
title: "ENCRYPTBYPASSPHRASE (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0fa00253d9f707e844baca9dc1baa807533ba2ed
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  キーの長さが 128 ビットの TRIPLE DES アルゴリズムを使用して、パスフレーズでデータを暗号化します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引数  
 *passphrase*  
 対称キーを生成するパスフレーズを指定します。  
  
 @passphrase  
 対象キーを生成するためのパスフレーズを含む、**nvarchar**、**char**、**varchar**、**binary**、**varbinary**、または **nchar** 型の変数を指定します。  
  
 *cleartext*  
 暗号化するクリア テキストを指定します。  
  
 @cleartext  
 クリア テキストを含む、**nvarchar**、**char**、**varchar**、**binary**、**varbinary**、または **nchar** 型の変数を指定します。最大サイズは 8,000 バイトです。  
  
 *add_authenticator*  
 クリア テキストと共に認証子を暗号化するかどうかを指定します。 認証子を追加する場合は 1 を指定します。 **int**です。  
  
 @add_authenticator  
 クリア テキストと共にハッシュを暗号化するかどうかを指定します。  
  
 *authenticator*  
 認証子の取得元となるデータを指定します。 **sysname**です。  
  
 @authenticator  
 認証子の取得元となるデータを含む変数を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 **varbinary** (最大サイズは 8,000 バイト)  
  
## <a name="remarks"></a>解説  
 パス フレーズは空白を含むパスワードです。 パスフレーズを使用する利点は、比較的長い文字列を覚えるより、意味のある句やセンテンスを覚える方が簡単であるという点です。  
  
 この関数ではパスワードの複雑性はチェックされません。  
  
## <a name="examples"></a>使用例  
 次の例では、`SalesCreditCard` テーブルのレコードを更新し、認証子として主キーを使用して、列 `CardNumber_EncryptedbyPassphrase` に格納されるクレジット カードの番号を暗証化します。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase varbinary(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT( varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DECRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
