---
description: sys.remote_service_bindings (Transact-SQL)
title: sys.remote_service_bindings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.remote_service_bindings_TSQL
- remote_service_bindings_TSQL
- remote_service_bindings
- sys.remote_service_bindings
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_service_bindings catalog view
ms.assetid: 4e1a885d-eed1-4993-9c87-e6fd781f437d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0ea8bd821e577f50f70bb141a17739afb41d4121
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203437"
---
# <a name="sysremote_service_bindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このカタログビューには、リモートサービスバインドごとに1行が含まれています。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|このリモートサービスバインドの名前。 NULL 値は許容されません。|  
|**remote_service_binding_id**|**int**|このリモートサービスバインドの ID。 NULL 値は許容されません。|  
|**principal_id**|**int**|このリモートサービスバインドを所有するデータベースプリンシパルの ID。 NULLABLE.|  
|**remote_service_name**|**nvarchar (256)**|このバインディングが適用されるリモートサービスの名前。 NULLABLE.|  
|**service_contract_id**|**int**|このバインディングが適用されるコントラクトの ID。 値0は、このバインディングがサービスのすべてのコントラクトに適用されることを意味するワイルドカードです。 NULL 値は許容されません。|  
|**remote_principal_id**|**int**|リモートサービスバインドで指定されたユーザーの ID。 Service Broker では、このユーザーが所有する証明書を使用して、指定したコントラクトに基づき、指定したサービスと通信します。 NULLABLE.|  
|**is_anonymous_on**|**bit**|このリモートサービスバインドは、匿名セキュリティを使用します。 メッセージ交換を開始するユーザーの id が、発信先サービスに提供されていません。 NULL 値は許容されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
