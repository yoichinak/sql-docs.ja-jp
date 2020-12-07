---
description: MSdbms_map (Transact-SQL)
title: MSdbms_map (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 66896c98c0d02dbb7cf9276f512420688b14be0f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551017"
---
# <a name="msdbms_map-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdbms_map**テーブルには、ソースデータ型の情報に加えて、ソースとターゲットの DBMS ペアに関する既定の変換先のデータ型情報へのリンクが含まれています。 このテーブルは **msdb** データベースに格納され、異種パブリッシングに使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|データ型マッピングを一意に識別します。|  
|**src_dbms_id**|**int**|[Msdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)テーブルで**dbms_id**を指定することによって、ソース DBMS を識別します。|  
|**dest_dbms_id**|**int**|[Msdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)テーブルでその**dbms_id**を指定することによって、対象の DBMS を識別します。|  
|**src_datatype_id**|**int**|[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)テーブルからソースデータ型の**datatype_id**を識別します。|  
|**src_len_min**|**bigint**|マップ元 DBMS におけるデータ型の最小の長さ。値 NULL は長さが使用されないことを示します。|  
|**src_len_max**|**bigint**|ソース DBMS でのデータ型の最大長。値が NULL の場合は、長さが使用されていないことを示します。|  
|**src_prec_min**|**bigint**|ソース DBMS でのデータ型の最小有効桁数。値 NULL は、有効桁数が使用されないことを示します。|  
|**src_prec_max**|**bigint**|ソース DBMS でのデータ型の最大有効桁数。値 NULL は、有効桁数が使用されないことを示します。|  
|**src_scale_min**|**int**|ソース DBMS でのデータ型の最小小数点以下桁数。値 NULL は、小数点以下桁数が使用されないことを示します。|  
|**src_scale_max**|**int**|マップ元 DBMS におけるデータ型の最大小数点以下桁数。値 NULL は小数点以下桁数が使用されないことを示します。|  
|**src_nullable**|**bit**|マッピングの変換先列で NULL 値を許容するかどうかを示します。値が NULL の場合、この定義は必要ありません。|  
|**default_datatype_mapping_id**|**int**|テーブル[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)で**map_id**を指定することによって、既定のデータ型マッピングを識別します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
