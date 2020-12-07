---
description: sysdatatypemappings (Transact-SQL)
title: msdb.dbo.sysdatatypemappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad4a6df1ae2dbdd418e133053330095a389bdf24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427534"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Msdb.dbo.sysdatatypemappings**ビューは、SQL Server データベース管理システム (DBMS) の SQL Server データ型とデータ型の間のマッピングを示すために使用されます。 このビューは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|データ型マッピングの ID。|  
|**source_dbms**|**sysname**|データ型のマップ元となる DBMS の名前を示します。次のいずれかの値を指定できます。<br /><br /> **MSSQLSERVER** = ソースは SQL Server データベースです。<br /><br /> **Oracle** = ソースは oracle データベースです。|  
|**source_version**|**sysname**|ソース DBMS の製品バージョンを示します。|  
|**source_type**|**sysname**|ソース DBMS に一覧表示されているデータ型を示します。|  
|**source_length_min**|**bigint**|マップ元 DBMS におけるデータ型の最小の長さ。値 NULL は長さが使用されないことを示します。|  
|**source_length_max**|**bigint**|ソース DBMS でのデータ型の最大長。値が NULL の場合は、長さが使用されていないことを示します。|  
|**source_precision_min**|**bigint**|ソース DBMS でのデータ型の最小有効桁数。値 NULL は、有効桁数が使用されないことを示します。|  
|**source_precision_max**|**bigint**|ソース DBMS でのデータ型の最大有効桁数。値 NULL は、有効桁数が使用されないことを示します。|  
|**source_scale_min**|**int**|ソース DBMS でのデータ型の最小小数点以下桁数。値 NULL は、小数点以下桁数が使用されないことを示します。|  
|**source_scale_max**|**int**|マップ元 DBMS におけるデータ型の最大小数点以下桁数。値 NULL は小数点以下桁数が使用されないことを示します。|  
|**source_nullable**|**bit**|変換先のデータ型で null 値がサポートされている場合に指定します。|  
|**source_createparams**|**int**|内部使用のみです。|  
|**destination_dbms**|**sysname**|マップ先 DBMS の名前を示します。次の値のいずれかになります。<br /><br /> **MSSQLSERVER** = 変換先は SQL Server データベースです。<br /><br /> **Oracle** = 変換先は、oracle データベースです。<br /><br /> **Db2** = 変換先は IBM DB2 データベースです。<br /><br /> **Sybase** = コピー先は sybase データベースです。|  
|**destination_version**|**sysname**|マップ先 DBMS の製品バージョンです。|  
|**destination_type**|**sysname**|マップ先 DBMS のデータ型です。|  
|**destination_length**|**bigint**|マップ先 DBMS のデータ型の長さです。|  
|**destination_precision**|**bigint**|マップ先 DBMS でのデータ型の有効桁数です。|  
|**destination_scale**|**int**|マップ先 DBMS のデータ型の小数点以下桁数です。|  
|**destination_nullable**|**bit**|マップ先 DBMS のデータ型で null 値がサポートされているかどうかを示します。|  
|**destination_createparams**|**int**|内部使用のみです。|  
|**データ損失**|**bit**|ソース DBMS とマップ先 DBMS でデータ型をマッピングするときに、データの損失が発生するかどうかを示します。|  
|**is_default**|**bit**|データ型マッピングが既定で使用されるかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
