---
description: sys.cryptographic_providers (Transact-SQL)
title: sys.cryptographic_providers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cryptographic_providers
- sys.cryptographic_providers
- sys.cryptographic_providers_TSQL
- cryptographic_providers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.cryptographic_providers catalog view
ms.assetid: 9da0da95-792e-48b4-9f60-47f0729c279c
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 305ea4a72855dd5ba136740dcc9b4321826384ad
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384807"
---
# <a name="syscryptographic_providers-transact-sql"></a>sys.cryptographic_providers (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  登録されている暗号プロバイダーごとに 1 行を返します。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|暗号化サービスプロバイダーの識別番号。|  
|**name**|**sysname**|暗号化サービスプロバイダーの名前。|  
|**guid**|**uniqueidentifier**|一意のプロバイダー GUID。|  
|**version**|**nvarchar (50)**|プロバイダーのバージョンを ' *aa.bb.cccc.dd* ' の形式で指定します。|  
|**dll_path**|**nvarchar(512)**|拡張キー管理 (EKM) アプリケーションプログラムインターフェイス (API) を実装する DLL へのパス。|  
|**is_enabled**|**bit**|サーバーでプロバイダーが有効になっているかどうか。<br /><br /> 0 = 無効 (既定値)<br /><br /> 1 = 有効|  
  
## <a name="permissions"></a>アクセス許可  
 **Sys.cryptographic_providers** ビューはパブリックに表示されます。  
  
## <a name="see-also"></a>参照  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
  
