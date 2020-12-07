---
description: sysarticlecolumns (Transact-sql)
title: sysarticlecolumns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 142ed0bfaad34607422b69929450ae9f7b09bd9e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540227"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns**テーブルには、スナップショットパブリケーションまたはトランザクションパブリケーションでパブリッシュされるテーブル列ごとに1つの行が含まれ、各列がアーティクルにマップされます。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルを識別します。|  
|**colid**|**smallint**|アーティクル内の列を識別します。|  
|**is_udt**|**bit**|列がユーザー定義データ型 (UDT) 列であるかどうかを示します。 値 **1** は UDT 列を示します。|  
|**is_xml**|**bit**|列が **xml** 列かどうかを示します。 値 **1** は xml 列を示します。|  
|**is_max**|**bit**|列が大きな値のデータ型の列、 **varchar (max)**、 **nvarchar (max)**、および **varbinary (max)** であるかどうかを示します。 値 **1** は大きな値の列を示します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
