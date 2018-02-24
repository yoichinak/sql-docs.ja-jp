---
title: "CERT_ID (TRANSACT-SQL) |Microsoft ドキュメント"
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
- CERT_ID
- CERT_ID_TSQL
dev_langs: TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3abed6a762708581344c189ecf4ef6c0fd5331d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="certid-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

証明書の ID を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>引数  
**'** *cert_name* **'**  
データベースの証明書の名前を指定します。
  
## <a name="return-types"></a>戻り値の型
 **int**  
  
## <a name="remarks"></a>解説  
証明書名は [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) カタログ ビューで確認できます。
  
## <a name="permissions"></a>権限  
証明書に対する権限が必要です。呼び出し元で、証明書に対する VIEW DEFINITION 権限が拒否されていないことも条件となります。
  
## <a name="examples"></a>使用例  
次の例では、`ABerglundCert3` という証明書の ID を返します。
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>参照
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
