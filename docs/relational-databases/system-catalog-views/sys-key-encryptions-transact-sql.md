---
description: sys.key_encryptions (Transact-SQL)
title: key_encryptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 872b6d6abbf8a962763210524eb607c07305d85d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548746"
---
# <a name="syskey_encryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  CREATE SYMMETRIC KEY ステートメントの ENCRYPTION BY 句で指定された対称キーの暗号化ごとに 1 行のデータを返します。  

  
|列名|データ型|説明|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|暗号化されたキーの ID。|  
|**拇印**|**varbinary(32)**|キーの暗号化で使用された証明書の SHA-1 ハッシュ。または、キーの暗号化で使用された対称キーの GUID。|  
|**crypt_type**|**char (4)**|暗号化の種類。<br /><br /> ESKS = 対称キーによる暗号化<br /><br /> ESKP、ESP2、または ESP3 = パスワードで暗号化<br /><br /> EPUC = 証明書による暗号化<br /><br /> EPUA = 非対称キーによる暗号化<br /><br /> ESKM = マスターキーによる暗号化|  
|**crypt_type_desc**|**nvarchar(60)**|暗号化の種類の説明:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(以降で [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] は、CSS によって使用されるバージョン番号が含まれています)。<br /><br /> 証明書による暗号化<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> 注: Windows DPAPI は、サービスマスターキーを保護するために使用されます。|  
|**crypt_property**|**varbinary(max)**|署名された、または暗号化されたビット。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
