---
description: MSdatatype_mappings (Transact-SQL)
title: MSdatatype_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: bbafdd41f1c1c3c10425a3d5f63af103a23dc9a6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160408"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdatatype_mappings** ビューでは、SQL Server データ型が、非 SQL Server データベース管理システム (DBMS) によって使用されるデータ型にマップされます。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|DBMS の名前を指定します。 使用可能な値とその説明を次に示します。<br /><br /> **MSSQLSERVER**: 転送先は SQL Server データベースです。<br />**Oracle**: 変換先は oracle データベースです。<br />**Db2**: 変換先は IBM DB2 データベースです。<br />**Sybase**: コピー先は sybase データベースです。|  
|**sql_type**|**nvarchar(128)**|SQL Server データ型です。|  
|**dest_type**|**nvarchar(128)**|非 SQL Server データ型の名前。|  
|**dest_prec**|**bigint**|非 SQL Server データ型の有効桁数です。|  
|**dest_create_params**|**int**|内部使用のみ。|  
|**dest_nullable**|**bit**|非 SQL Server データ型が NULL 値をサポートしているかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
