---
description: column_encryption_key_values (Transact-sql)
title: column_encryption_key_values (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aee9c14d1b59055cc968e9b51fa2e07005ae94bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470016"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>column_encryption_key_values (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  列の暗号化キー (CEKs) の暗号化された値に関する情報を返します、列の暗号化キーを [作成](../../t-sql/statements/create-column-encryption-key-transact-sql.md) するか、 [ALTER column 暗号化キー &#40;transact-sql&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) ステートメントです。 各行は、列マスターキー (CMK) で暗号化された CEK の値を表します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|データベース内の CEK の ID。|  
|**column_master_key_id**|**int**|CEK 値の暗号化に使用された列マスターキーの ID。|  
|**encrypted_value**|**varbinary(8000)**|Column_master_key_id で指定された CMK で暗号化された CEK 値。|  
|**encryption_algorithm_name**|**sysname**|CEK 値の暗号化に使用されるアルゴリズムの名前。<br /><br /> 値を暗号化するために使用する暗号化アルゴリズムの名前です。 システムプロバイダーのアルゴリズムは  **RSA_OAEP**である必要があります。|  
  
## <a name="permissions"></a>アクセス許可  
 **VIEW ANY COLUMN ENCRYPTION KEY**権限が必要です。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の列暗号化キーの作成 ](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;列暗号化キーの変更 ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;列暗号化キーを削除します。 ](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-sql&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [column_encryption_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [column_master_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Secure enclaves での Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
