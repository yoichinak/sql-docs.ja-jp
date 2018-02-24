---
title: "VERIFYSIGNEDBYCERT (TRANSACT-SQL) |Microsoft ドキュメント"
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
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6267b5ca34c3e69af9611c2cdb4a607a7d539f00
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  デジタル署名付きデータが、署名された後に変更されているかどうかをテストします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
## <a name="arguments"></a>引数  
 *Cert_ID*  
 データベース内の証明書の ID を指定します。 *Cert_ID*は**int**です。  
  
 *signed_data*  
 証明書を使用して署名されたデータを含む、**nvarchar**、**char**、**varchar**、または **nchar** 型の変数を指定します。  
  
 *signature*  
 署名付きデータにアタッチされた署名を指定します。 *signature*は**varbinary**です。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
 署名付きデータが変更されていない場合は 1、変更されている場合は 0 が返されます。  
  
## <a name="remarks"></a>解説  
 **VerifySignedBycert**指定された証明書の公開キーを使用して、データの署名を復号化し、データの新しく計算された MD5 ハッシュを復号化された値を比較します。 値が一致すると、その署名が有効であることが確認されます。  
  
## <a name="permissions"></a>権限  
 証明書に対する VIEW DEFINITION 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>A. 署名付きデータが変更されていないことを確認する  
 次の例では、`Signed_Data` 内の情報が、`Shipping04` という証明書を使用して署名された後に変更されているかどうかをテストします。署名は `DataSignature` に格納されています。証明書 `Shipping04` を `Cert_ID` に渡すと、データベース内の証明書の ID が返されます。`VerifySignedByCert` で 1 が返された場合、署名は正しいことになります。`VerifySignedByCert` で 0 が返された場合、`Signed_Data` 内のデータは、`DataSignature` の生成に使用されたデータではありません。この場合、`Signed_Data` は署名された後に変更されたか、別の証明書を使用して署名されています。  
  
```  
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>B. 有効な署名が含まれるレコードのみを返す  
 次のクエリでは、証明書 `Shipping04` を使用して署名された後、変更されていないレコードだけを返します。  
  
```  
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
