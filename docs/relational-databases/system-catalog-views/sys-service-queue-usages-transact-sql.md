---
description: sys.service_queue_usages (Transact-sql)
title: sys.service_queue_usages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.service_queue_usages
- sys.service_queue_usages_TSQL
- service_queue_usages
- service_queue_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queue_usages catalog view
ms.assetid: d58dcdaf-f82d-43d9-941b-f520581442bf
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 38f1bd8d054dfbc4b8a90ce9a9fa9554bee24685
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204485"
---
# <a name="sysservice_queue_usages-transact-sql"></a>sys.service_queue_usages (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サービスとサービス キュー間の参照ごとに 1 行のデータを返すカタログ ビューです。 1 つのサービスは 1 つのキューにのみ関連付けることができます。 キューは、複数のサービスに関連付けることができます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|サービスの識別子。 データベース内で一意です。 NULL 値は許容されません。|  
|**service_queue_id**|**int**|サービスによって使用されるサービスキューの識別子。 NULL 値は許容されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のサービス ](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)  
  
  
