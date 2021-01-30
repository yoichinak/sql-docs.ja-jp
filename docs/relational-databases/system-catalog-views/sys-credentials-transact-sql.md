---
description: sys. 資格情報 (Transact-sql)
title: sys. credentials (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs:
- TSQL
helpviewer_keywords:
- sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d1b850ea878f4018886b8a546653ae7a270b60fe
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211310"
---
# <a name="syscredentials-transact-sql"></a>sys. 資格情報 (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  サーバーレベルの資格情報ごとに1つの行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|資格情報の ID。 はサーバー内で一意です。|  
|name|**sysname**|資格情報の名前。 はサーバー内で一意です。|  
|credential_identity|**nvarchar (4000)**|使用する識別情報の名前。 通常、これは Windows ユーザーです。 一意である必要はありません。|  
|create_date|**datetime**|資格情報が作成された日時。|  
|modify_date|**datetime**|資格情報が最後に変更された時刻。|  
|target_type|**nvarchar (100)**|資格情報の種類。 暗号化サービスプロバイダーにマップされている資格情報の暗号化サービスプロバイダー (従来の資格情報) の場合は NULL を返します。 外部キー管理プロバイダーの詳細については、「 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)」を参照してください。|  
|target_id|**int**|資格情報がマップされているオブジェクトの ID。 暗号化サービスプロバイダーにマップされている資格情報の場合は、従来の資格情報の場合は0、それ以外の場合は0を返します。 外部キー管理プロバイダーの詳細については、「 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)」を参照してください。|  

## <a name="remarks"></a>コメント  
データベースレベルの資格情報については、「 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)」を参照してください。
  
## <a name="permissions"></a>アクセス許可  
 `VIEW ANY DEFINITION`アクセス許可または `ALTER ANY CREDENTIAL` アクセス許可のいずれかが必要です。 また、プリンシパルに対して権限を拒否することはできません `VIEW ANY DEFINITION` 。  
  
## <a name="see-also"></a>参照  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
