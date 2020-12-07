---
description: conversation_groups (Transact-sql)
title: conversation_groups (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ffea98db7c6d1a2a673b7a8bd8d358578d81d43b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537478"
---
# <a name="sysconversation_groups-transact-sql"></a>conversation_groups (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  メッセージ交換グループごとに 1 行のデータを格納するカタログ ビューです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**conversation_group_id**|**uniqueidentifier**|メッセージ交換グループの識別子。 NULL 値は許容されません。|  
|**service_id**|**int**|このグループのメッセージ交換で使用されるサービスの識別子。 NULL 値は許容されません。|  
|**is_system**|**bit**|システム インスタンスであるかどうかを示します。 NULLABLE.|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
