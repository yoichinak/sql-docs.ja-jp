---
description: sys.service_message_types (Transact-sql)
title: sys.service_message_types (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 9ce8898f707a1c82f98e88a04f52ffd706cd7fb4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204493"
---
# <a name="sysservice_message_types-transact-sql"></a>sys.service_message_types (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このカタログビューには、service broker に登録されているメッセージの種類ごとに1行が含まれています。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|メッセージ型の名前。データベース内で一意です。 NULL 値は許容されません。|  
|**message_type_id**|**int**|メッセージ型の識別子。データベース内で一意です。 NULL 値は許容されません。|  
|**principal_id**|**int**|このメッセージ型を所有するデータベースプリンシパルの識別子。 NULLABLE.|  
|**validation**|**char(2)**|この型のメッセージを送信する前に、ブローカーによって実行される検証。 NULL 値は許容されません。 つぎのいずれかです。<br /><br /> N = なし<br /><br /> X = XML<br /><br /> E = 空|  
|**validation_desc**|**nvarchar(60)**|この型のメッセージを送信する前に、ブローカーで実行される検証の説明。 NULLABLE. つぎのいずれかです。<br /><br /> NONE<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|XML スキーマを使用する検証の場合、使用されるスキーマ コレクションの識別子。<br /><br /> それ以外の場合は NULL。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
