---
description: destination_data_spaces (Transact-sql)
title: destination_data_spaces (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.destination_data_spaces
- destination_data_spaces_TSQL
- destination_data_spaces
- sys.destination_data_spaces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.destination_data_spaces catalog view
ms.assetid: 92df932b-ad5c-43f8-81f4-b158823ab189
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6a1bf415042ea6c5a4e2c1fa996961af72247a9f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548810"
---
# <a name="sysdestination_data_spaces-transact-sql"></a>destination_data_spaces (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パーティション構成のデータ領域の転送先ごとに 1 行のデータを保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**partition_scheme_id**|**int**|データ領域にパーティション分割されているパーティション構成の ID。|  
|**destination_id**|**int**|パーティション構成内で一意な、転送先マッピングの ID (1 から始まる序数) です。|  
|**data_space_id**|**int**|この構成の転送先のデータがマッピングされるデータ領域の ID です。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
