---
title: "KEY_NAME (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
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
- KEY_NAME_TSQL
- KEY_NAME
dev_langs: TSQL
helpviewer_keywords: KEY_NAME function
ms.assetid: 7b693e5d-2325-4bf9-9b45-ad6a23374b41
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db0ea5d34aae0bd3486bd6a143df187b9d5d7899
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="keyname-transact-sql"></a>KEY_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  対称キーの GUID または暗号化テキストの対称キーの名前を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
KEY_NAME ( ciphertext | key_guid )   
```  
  
## <a name="arguments"></a>引数  
 *ciphertext*  
 対称キーによって暗号化されたテキストを指定します。 *ciphertext* の型は **varbinary(8000)** です。  
  
 *key_guid*  
 対称キーの GUID を指定します。 *key_guid* の型は **uniqueidentifier** です。  
  
## <a name="returned-types"></a>戻り値の型  
 **varchar(128)**  
  
## <a name="permissions"></a>権限  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では、メタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-the-name-of-a-symmetric-key-using-the-keyguid"></a>A. key_guid を使用して対称キーの名前を表示する  
 **master** データベースには、##MS_ServiceMasterKey## という名前の対称キーが含まれています。 次の例では、sys.symmetric_keys 動的管理ビューからそのキーの GUID を取得し、変数に割り当ててからその変数を KEY_NAME 関数に渡して、GUID に対応する名前を返す方法を示します。  
  
```  
USE master;  
GO  
DECLARE @guid uniqueidentifier ;  
SELECT @guid = key_guid FROM sys.symmetric_keys  
WHERE name = '##MS_ServiceMasterKey##' ;  
-- Demonstration of passing a GUID to KEY_NAME to receive a name  
SELECT KEY_NAME(@guid) AS [Name of Key];  
```  
  
### <a name="b-displaying-the-name-of-a-symmetric-key-using-the-cipher-text"></a>B. 暗号化テキストを使用して対称キーの名前を表示する  
 次の例では、対称キーを作成してテーブルにデータを取り込む全手順を示します。 さらに、KEY_NAME に暗号化テキストに渡してキーの名前を返す方法を示します。  
  
```  
-- Create a symmetric key  
CREATE SYMMETRIC KEY TestSymKey   
   WITH ALGORITHM = AES_128,  
   KEY_SOURCE = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
   IDENTITY_VALUE = 'Pythagoras'  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Create a table for the demonstration  
CREATE TABLE DemoKey  
(IDCol int IDENTITY PRIMARY KEY,  
SecretCol varbinary(256) NOT NULL)  
GO  
-- Open the symmetric key if not already open  
OPEN SYMMETRIC KEY TestSymKey   
    DECRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
-- Insert a row into the DemoKey table  
DECLARE @key_GUID uniqueidentifier;  
SELECT @key_GUID = key_guid FROM sys.symmetric_keys  
WHERE name LIKE 'TestSymKey' ;  
INSERT INTO DemoKey(SecretCol)  
VALUES ( ENCRYPTBYKEY (@key_GUID, 'EncryptedText'))  
GO  
-- Verify the DemoKey data  
SELECT * FROM DemoKey;  
GO  
-- Decrypt the data  
DECLARE @ciphertext varbinary(256);  
SELECT @ciphertext = SecretCol  
FROM DemoKey WHERE IDCol = 1 ;  
SELECT CAST (  
DECRYPTBYKEY( @ciphertext)  
AS varchar(100) ) AS SecretText ;  
-- Use KEY_NAME to view the name of the key  
SELECT KEY_NAME(@ciphertext) AS [Name of Key] ;  
  
```  
  
## <a name="see-also"></a>参照  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEYAUTOASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)  
  
  
