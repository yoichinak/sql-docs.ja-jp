---
description: sys.dm_cryptographic_provider_sessions (Transact-SQL)
title: sys.dm_cryptographic_provider_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8af82a9be0181aa5668ee59dc3c82e20233023d1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195120"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  暗号プロバイダーの開いているセッションに関する情報を返します。  
 
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>引数  
 *session_identifier*  
 返されるセッションを示す整数。  
  
 0 = 現在の接続のみ  
  
 1 = すべての暗号接続  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|暗号化サービスプロバイダーの識別番号。|  
|**session_handle**|**varbytes (8)**|暗号化セッションハンドル。|  
|**identity**|**nvarchar(128)**|暗号化サービスプロバイダーでの認証に使用する id。|  
|**spid**|**short**|接続のセッション ID SPID。 詳細については、「[@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 パブリックサーバーロールのメンバーは、 **sys.dm_cryptographic_provider_sessions** を使用して、現在の接続に関する情報を返すことができます。 すべての暗号化接続を表示するには、 **CONTROL** server 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
