---
description: sys.conversation_groups (Transact-sql)
title: sys.conversation_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_groups_TSQL
- conversation_groups
- sys.conversation_groups
- sys.conversation_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_groups catalog view
ms.assetid: 3f35815e-2de4-42a2-a972-8f0141dad0b3
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8efd718c9c5ab4d7c1186d3a85c70c1ced1c51ae
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100658"
---
# <a name="sysconversation_groups-transact-sql"></a>sys.conversation_groups (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  メッセージ交換グループごとに 1 行のデータを格納するカタログ ビューです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**conversation_group_id**|**uniqueidentifier**|メッセージ交換グループの識別子。 NULL 値は許容されません。|  
|**service_id**|**int**|このグループのメッセージ交換で使用されるサービスの識別子。 NULL 値は許容されません。|  
|**is_system**|**bit**|システム インスタンスであるかどうかを示します。 NULLABLE.|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
