---
description: sys.dm_cryptographic_provider_properties (Transact-SQL)
title: sys.dm_cryptographic_provider_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_properties_TSQL
- sys.dm_cryptographic_provider_properties
- sys.dm_cryptographic_provider_properties_TSQL
- dm_cryptographic_provider_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_properties dynamic management view
ms.assetid: 024b0095-6766-4189-a39a-d316c5ec2874
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 419793e94cc85a8dba1e29f4b79694820518eaad
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384673"
---
# <a name="sysdm_cryptographic_provider_properties-transact-sql"></a>sys.dm_cryptographic_provider_properties (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  登録されている暗号化サービスプロバイダーに関する情報を返します。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|暗号化サービスプロバイダーの識別番号。|  
|guid|**uniqueidentifier**|一意のプロバイダー GUID。|  
|provider_version|**nvarchar (256)**|プロバイダーのバージョンを ' *aa.bb.cccc.dd* ' の形式で指定します。|  
|sqlcrypt_version|**nvarchar (256)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]' *Aa.bb.cccc.dd* ' 形式の暗号化 API のメジャーバージョン。|  
|friendly_name|**nvarchar(2048)**|プロバイダーによって指定された名前。|  
|authentication_type|**nvarchar (256)**|WINDOWS、BASIC、またはその他。|  
|symmetric_key_support|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_export|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_import|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_persistance|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|asymmetric_key_support|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|asymmetric_key_export|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_import|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
|symmetric_key_persistance|**tinyint**|0 (サポートされていません)<br /><br /> 1 (サポートされています)|  
  
## <a name="permissions"></a>アクセス許可  
 **Sys.dm_cryptographic_provider_properties** ビューはパブリックに表示されます。  
  
## <a name="see-also"></a>参照  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
