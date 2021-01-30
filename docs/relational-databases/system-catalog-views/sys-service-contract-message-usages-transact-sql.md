---
description: sys.service_contract_message_usages (Transact-SQL)
title: sys.service_contract_message_usages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 33677382cd6dcf71bc6da8525747712fe8b83721
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99161382"
---
# <a name="sysservice_contract_message_usages-transact-sql"></a>sys.service_contract_message_usages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このカタログビューには、(コントラクト、メッセージ型) のペアごとに1行が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|メッセージ型を使用するコントラクトの識別子。 NULL 値は許容されません。|  
|**message_type_id**|**int**|コントラクトによって使用されるメッセージ型の識別子。 NULL 値は許容されません。|  
|**is_sent_by_initiator**|**bit**|メッセージの種類は、メッセージ交換の発信側から送信できます。 NULL 値は許容されません。|  
|**is_sent_by_target**|**bit**|メッセージの種類は、メッセージ交換のターゲットによって送信できます。 NULL 値は許容されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
