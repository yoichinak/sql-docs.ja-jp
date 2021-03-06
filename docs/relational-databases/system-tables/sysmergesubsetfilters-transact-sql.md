---
description: sysmergesubsetfilters (Transact-sql)
title: sysmergesubsetfilters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
author: cawrites
ms.author: chadam
ms.openlocfilehash: bd623b860391768ef8a691feb0a5f651847778a2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99209197"
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パーティション分割されたアーティクルの結合フィルター情報を格納します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**filtername**|**sysname**|アーティクルを作成するときに使用したフィルターの名前。|  
|**join_filterid**|**int**|結合フィルターを表すオブジェクトの ID。|  
|**pubid**|**uniqueidentifier**|パブリケーションの ID です。|  
|**artid**|**uniqueidentifier**|アーティクルの ID です。|  
|**art_nickname**|**int**|アーティクルのニックネーム。|  
|**join_articlename**|**sysname**|行が属しているかどうかを判断するために結合するテーブルの名前。|  
|**join_nickname**|**int**|行が属しているかどうかを判断するために結合するテーブルのニックネーム。|  
|**join_unique_key**|**int**|**Join_tablename** の一意のキーの結合を示します。<br /><br /> 0 = 一意キーではない<br /><br /> 1 = 一意キー|  
|**expand_proc**|**sysname**|サブスクライバーから送信または削除する必要がある行を識別するためにマージエージェントによって使用されるストアドプロシージャの名前。|  
|**join_filterclause**|**nvarchar(1000)**|結合に使用されるフィルター句。|  
|**filter_type**|**tinyint**|フィルターの種類。次のいずれかになります。<br /><br /> 1 = 結合フィルター。<br /><br /> 2 = 論理レコードのリンク。<br /><br /> 3 = 結合フィルターと論理レコードリンクの両方。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
