---
description: sys.dm_cryptographic_provider_keys (Transact-sql)
title: sys.dm_cryptographic_provider_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys
- sys.dm_cryptographic_provider_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_keys dynamic management function
ms.assetid: 5a8c1421-c56b-44b5-96e5-4f01782a0c7c
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 508240f27248cb4cc618441948c40b72c9311398
ms.sourcegitcommit: 58e7069b5b2b6367e27b49c002ca854b31b1159d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2021
ms.locfileid: "99552611"
---
# <a name="sysdm_cryptographic_provider_keys-transact-sql"></a>sys.dm_cryptographic_provider_keys (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  拡張キー管理 (EKM: Extensible Key Management) プロバイダーによって提供されるキーに関する情報を返します。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!IMPORTANT]
> この動的管理ビューは、現在、SQL Server EKM コネクタではサポートされていません。 SQL Server 製品チームはこの問題を認識しており、今後この問題に対処する予定です。

## <a name="syntax"></a>構文  
  
```  
  
dm_cryptographic_provider_keys ( provider_id )  
```  
  
## <a name="arguments"></a>引数  
 *provider_id*  
 EKM プロバイダーの識別番号。既定値はありません。  
  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**key_id**|**int**|プロバイダーのキーの識別番号。|  
|**key_name**|**nvarchar(512)**|プロバイダーのキーの名前。|  
|**key_thumbprint**|**varbinary(32)**|キーのプロバイダーからの拇印。|  
|**algorithm_id**|**int**|プロバイダーのアルゴリズムの識別番号。|  
|**algorithm_tag**|**int**|プロバイダーのアルゴリズムのタグ|  
|**key_type**|**nchar(256)**|プロバイダーのキーの型。|  
|**key_length**|**int**|プロバイダーのキーの長さ|  
  
## <a name="permissions"></a>アクセス許可  
 このビューに対してクエリを実行すると、プロバイダーによるユーザーコンテキストの認証と、ユーザーに表示されるすべてのキーの列挙が行われます。  
  
 ユーザーが EKM プロバイダーで認証できない場合、キー情報は返されません。  
  
## <a name="examples"></a>使用例  
 次の例は、の識別番号を持つプロバイダーのキープロパティを示して `1234567` います。  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
