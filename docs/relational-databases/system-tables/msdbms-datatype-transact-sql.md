---
description: MSdbms_datatype (Transact-SQL)
title: MSdbms_datatype (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: cawrites
ms.author: chadam
ms.openlocfilehash: 6db79a6d76443492e4079df48c34c518db4dea0d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160457"
---
# <a name="msdbms_datatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdbms_datatype** の表には、異種データベースレプリケーションでパブリッシャーまたはサブスクライバーとして使用される、サポートされている各データベース管理システム (DBMS) のネイティブデータ型の完全な一覧が含まれています。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|一意の各データ型を識別します。|  
|**dbms_id**|**int**|型が属する DBMS を識別します。|  
|**type**|**sysname**|データ型名 (ネイティブ)。|  
|**createparams**|**int**|各データ型に適用できる長さ、有効桁数、および小数点以下桁数の組み合わせを表すビットマップです。以下の要素が含まれます。<br /><br /> **0x1** = 有効桁数。<br /><br /> **0x2** = スケール。<br /><br /> **0x4** = 長さ。|  
  
## <a name="remarks"></a>コメント  
 このテーブルには SQL Server のデータ型のエントリが含まれています。 SQL Server のインスタンスは、非 SQL Server データベースにサブスクライブし、SQL Server 以外のサブスクライバーにパブリッシュすることができます。  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
