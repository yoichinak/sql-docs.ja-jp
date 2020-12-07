---
description: ENCRYPTBYCERT (Transact-SQL)
title: ENCRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYCERT
- ENCRYPTBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], encryption
- encryption [SQL Server], certificates
- ENCRYPTBYCERT function
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cbfb3932f86f7fc120ed9d2c2693848e769d2aa3
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116072"
---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

証明書の公開キーを使ってデータを暗号化します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
_certificate\_ID_  
データベース内の証明書の ID。 **int**.  
  
_cleartext_  
証明書で暗号化されるデータの文字列。  
  
**\@cleartext**  
証明書の公開キーで暗号化されるデータが含まれる次のいずれかの型の変数:

* **nvarchar** 
* **char**
* **varchar**
* **[バイナリ]** 
* **varbinary**
* **nchar**
  
## <a name="return-types"></a>戻り値の型  
**varbinary** 8,000 バイトの最大サイズ。  
  
## <a name="remarks"></a>解説  
この関数によって証明書の公開キーでデータが暗号化されます。 この暗号文は、対応する秘密キーでのみ暗号化を解除できます。 対称キーを使用した暗号化と暗号化の解除に比べ、このような非対称変換はコストが高くなります。 そのため、大きなデータセットを扱う場合、非同期暗号化は推奨されません。
  
## <a name="examples"></a>例  
次の例では、`@cleartext` という証明書を使用して、`JanainaCert02` に格納されているプレーン テキストを暗号化します。 暗号化されたデータは、テーブル `ProtectedData04` に挿入されます。  
  
```sql  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>参照  
[DECRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
[DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
