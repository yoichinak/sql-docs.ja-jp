---
title: "CERTPROPERTY (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
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
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d63968d8b07a37ea49662bd0727632a1675b3913
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

指定した証明書のプロパティの値を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>引数  
*Cert_ID*  
証明書の ID を指定します。 *Cert_ID*は int です。
  
*Expiry_Date*  
証明書の有効期限日を指定します。
  
*Start_Date*  
証明書が有効になる日付です。
  
*Issuer_Name*  
証明書の発行者の名前を指定します。
  
*Cert_Serial_Number*  
証明書のシリアル番号を指定します。
  
*Subject*  
証明書のサブジェクトを指定します。
  
 *SID*  
証明書の SID を指定します。 これは、この証明書にマップされているログインまたはユーザーの SID でもあります。
  
*String_SID*  
証明書の SID を文字列で指定します。 これは、この証明書にマップされているログインまたはユーザーの SID でもあります。
  
## <a name="return-types"></a>戻り値の型
プロパティは単一引用符で囲んで指定する必要があります。
  
戻り値の型は、関数の呼び出しで指定されたプロパティによって異なります。 すべての戻り値は、戻り値の型 **sql_variant** にラップされます。
-   *Expiry_Date* および *Start_Date* では **datetime** 型が返されます。  
-   *Cert_Serial_Number*、*Issuer_Name*、*Subject*、および *String_SID* では **nvarchar** 型が返されます。  
-   *SID* では **varbinary** 型が返されます。  
  
## <a name="remarks"></a>解説  
証明書に関する情報は、[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) カタログ ビューで確認できます。
  
## <a name="permissions"></a>権限  
証明書に対する権限が必要です。呼び出し元で、証明書に対する VIEW DEFINITION 権限が拒否されていないことも条件となります。
  
## <a name="examples"></a>使用例  
次の例では、証明書のサブジェクトを返します。
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>参照
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
