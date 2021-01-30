---
description: sys.service_queues (Transact-SQL)
title: sys.service_queues (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.service_queues
- service_queues
- service_queues_TSQL
- sys.service_queues_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queues catalog view
ms.assetid: 9fd9fa76-6128-410c-896f-741e6050143a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: f85fac244c9530a29e14b1aeaf14430feed337b3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204473"
---
# <a name="sysservice_queues-transact-sql"></a>sys.service_queues (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース内のサービスキューであるオブジェクトごとに1行のデータを格納します。 **type** = SQ。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||このビューが継承する列の一覧については、「 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|**max_readers**|**smallint**|キューで許可される同時読み取りの最大数です。|  
|**activation_procedure**|**nvarchar (776)**|3 つの要素で構成されるアクティブ化プロシージャの名前です。|  
|**execute_as_principal_id**|**int**|実行データベースプリンシパルの ID。<br /><br /> 既定では NULL、または EXECUTE AS CALLER の場合は NULL です。<br /><br /> [自己実行として実行する場合は、指定されたプリンシパルの ID \<principal> です。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**is_activation_enabled**|**bit**|1 = アクティブ化が有効になっています。|  
|**is_receive_enabled**|**bit**|1 = 受信は有効になっています。|  
|**is_enqueue_enabled**|**bit**|1 = エンキューは有効です。|  
|**is_retention_enabled**|**bit**|1 = メッセージは、ダイアログが終了するまで保持されます。|  
|**is_poison_message_handling_enabled**|**bit**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 1 = 有害なメッセージの処理が有効です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
