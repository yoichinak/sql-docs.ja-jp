---
description: MSmerge_altsyncpartners (Transact-sql)
title: MSmerge_altsyncpartners (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_altsyncpartners_TSQL
- MSmerge_altsyncpartners
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_altsyncpartners system table
ms.assetid: da51b0f8-5ad0-4aeb-96ed-2b3672a2a6e2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ccec6fa369580fd68af0089c7e581ef1e915e868
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545665"
---
# <a name="msmerge_altsyncpartners-transact-sql"></a>MSmerge_altsyncpartners (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_altsyncpartners**テーブルは、パブリッシャーの現在の同期パートナーとの関連付けを追跡します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|元のパブリッシャーの識別子。|  
|**alternate_subid**|**uniqueidentifier**|代替同期パートナーであるサブスクライバーの識別子。|  
|**description**|**nvarchar (255)**|代替同期パートナーの説明|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
