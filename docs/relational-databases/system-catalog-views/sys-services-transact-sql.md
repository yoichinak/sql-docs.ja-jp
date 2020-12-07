---
description: sys. services (Transact-sql)
title: sys. services (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.services
- services
- services_TSQL
- sys.services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.services catalog view
ms.assetid: 16d0b0c5-5cce-469b-aa3d-4b9248e0c085
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 27653c3cbc38f8d7cd2bdc46c4800fd3db4067db
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539517"
---
# <a name="sysservices-transact-sql"></a>sys. services (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このカタログビューには、データベース内のサービスごとに1行のデータが含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|サービスの名前。大文字と小文字が区別されます。データベース内で一意です。 NULL 値は許容されません。|  
|**service_id**|**int**|サービスの識別子。 NULL 値は許容されません。|  
|**principal_id**|**int**|このサービスを所有するデータベースプリンシパルの識別子。 NULLABLE.|  
|**service_queue_id**|**int**|このサービスが使用するキューのオブジェクト id。 NULL 値は許容されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
