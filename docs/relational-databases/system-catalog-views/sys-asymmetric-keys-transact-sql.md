---
description: sys.asymmetric_keys (Transact-SQL)
title: asymmetric_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- asymmetric_keys
- sys.asymmetric_keys_TSQL
- asymmetric_keys_TSQL
- sys.asymmetric_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.asymmetric_keys catalog view
ms.assetid: bbca796a-9bb5-4a62-9ca8-1d255984553d
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d8ff4d42014f0e3b61c4087ae879edfb8f9da744
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539707"
---
# <a name="sysasymmetric_keys-transact-sql"></a>sys.asymmetric_keys (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  非対称キーごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|キーの名前。 データベース内で一意です。|  
|**principal_id**|**int**|キーを所有するデータベースプリンシパルの ID。|  
|**asymmetric_key_id**|**int**|キーの ID。 データベース内で一意です。|  
|**pvt_key_encryption_type**|**char(2)**|キーの暗号化方法。<br /><br /> NA = 暗号化されていません。<br /><br /> MK = キーはマスター キーにより暗号化されています。<br /><br /> PW = キーはユーザー定義のパスワードによって暗号化されます。<br /><br /> SK = キーはサービス マスター キーにより暗号化されています。|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|秘密キーの暗号化方法の説明。<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**拇印**|**varbinary(32)**|キーの SHA-1 ハッシュ。 ハッシュはグローバルに一意です。|  
|**アルゴリズム**|**char(2)**|キーと一緒に使用されるアルゴリズム。<br /><br /> 1R = 512 ビット RSA<br /><br /> 2R = 1024 ビット RSA<br /><br /> 3R = 2048 ビット RSA|  
|**algorithm_desc**|**nvarchar(60)**|キーで使用されるアルゴリズムの説明。<br /><br /> RSA_512<br /><br /> RSA_1024<br /><br /> RSA_2048|  
|**key_length**|**int**|キーのビット長。|  
|**sid**|**varbinary(85)**|このキーのログイン SID。 拡張キー管理キーの場合、この値は NULL になります。|  
|**string_sid**|**nvarchar(128)**|キーのログイン SID の文字列形式。 拡張キー管理キーの場合、この値は NULL になります。|  
|**public_key**|**varbinary(max)**|公開キー。|  
|**attested_by**|**nvarchar(260)**|システムでのみ使用されます。|  
|**provider_type**|**nvarchar(120)**|暗号化サービスプロバイダーの種類:<br /><br /> 暗号化サービスプロバイダー = 拡張キー管理キー<br /><br /> NULL = 拡張キー管理以外のキー|  
|**cryptographic_provider_guid**|**uniqueidentifier**|暗号化サービスプロバイダーの GUID。 拡張キー管理以外のキーの場合、この値は NULL になります。|  
|**cryptographic_provider_algid**|**sql_variant**|暗号化サービスプロバイダーのアルゴリズム ID。 拡張キー管理以外のキーの場合、この値は NULL になります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
  
