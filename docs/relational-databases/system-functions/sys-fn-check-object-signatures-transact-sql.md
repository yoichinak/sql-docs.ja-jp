---
description: sys.fn_check_object_signatures (Transact-SQL)
title: fn_check_object_signatures (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7dc2f5c8700bef804b77e97917250152988baf7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481829"
---
# <a name="sysfn_check_object_signatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  署名可能なすべてのオブジェクトの一覧を返し、オブジェクトが、指定した証明書または非対称キーで署名されているかどうかを示します。 オブジェクトが、指定した証明書または非対称キーによって署名されている場合は、オブジェクトの署名が有効かどうかも返されます。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>引数  
 { '\@*クラス*'}  
 提供される拇印の種類を識別します。  
  
-   'certificate'  
  
-   'asymmetric key'  
  
 \@*class* は **sysname** です。  
  
 { \@ *thumbprint* }  
 キーの暗号化で使用された証明書の SHA-1 ハッシュ。または、キーの暗号化で使用された非対称キーの GUID。 \@*拇印* は **varbinary (20)** です。  
  
## <a name="tables-returned"></a>返されるテーブル  
 次の表に、 **fn_check_object_signatures** が返す列を示します。  
  
|Column|種類|説明|  
|------------|----------|-----------------|  
|type|**nvarchar(120)**|型の説明またはアセンブリを返します。|  
|entity_id|**int**|評価対象のオブジェクトのオブジェクト ID を返します。|  
|is_signed|**int**|指定された拇印によってオブジェクトが署名されていない場合は0を返します。 指定されたサムプリントによってオブジェクトが署名されている場合は1を返します。|  
|is_signature_valid|**int**|is_signed の値が 1 の場合、署名が有効ではないときは 0 を返します。 署名が有効な場合は1を返します。<br /><br /> is_signed の値が 0 の場合は、常に 0 を返します。|  
  
## <a name="remarks"></a>解説  
 **Fn_check_object_signatures**を使用して、悪意のあるユーザーがオブジェクトを改ざんしていないことを確認します。  
  
## <a name="permissions"></a>アクセス許可  
 証明書または非対称キーに対する VIEW DEFINITION が必要です。  
  
## <a name="examples"></a>例  
 次の例では、データベースのスキーマ署名証明書を検索 `master` し、 `is_signed` `is_signature_valid` スキーマ署名証明書によって署名され、有効な署名を持つオブジェクトについて、値1と値1を返します。  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [IS_OBJECTSIGNED &#40;Transact-sql&#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
