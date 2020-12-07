---
description: dm_db_xtp_memory_consumers (Transact-sql)
title: dm_db_xtp_memory_consumers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers_TSQL
- sys.dm_db_xtp_memory_consumers_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_memory_consumers dynamic management view
ms.assetid: f7ab2eaf-e627-464d-91fe-0e170b3f37bc
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 321297a2590a18ed7e51364b3f532076f90ce740
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542238"
---
# <a name="sysdm_db_xtp_memory_consumers-transact-sql"></a>dm_db_xtp_memory_consumers (Transact-sql)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベース エンジンのデータベース レベルのメモリ コンシューマーを報告します。 ビューは、データベースエンジンが使用するメモリコンシューマーごとに1行のデータを返します。 この DMV を使用して、さまざまな内部オブジェクト間でメモリがどのように分散されているかを確認します。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|memory_consumer_id|**bigint**|メモリコンシューマーの ID (内部)。|  
|memory_consumer_type|**int**|メモリコンシューマーの種類。<br /><br /> 0=集計  (2 つ以上のコンシューマーのメモリ使用量を集計します。 表示することはできません)<br /><br /> 2 = VARHEAP (可変長ヒープのメモリ使用量を追跡します)<br /><br /> 3=HASH (インデックスのメモリ使用量を追跡します)<br /><br /> 5 = DB ページプール (実行時操作に使用されるデータベースページプールのメモリ使用量を追跡します。 たとえば、テーブル変数および一部のシリアル化可能なスキャンが対象になります。 この種類のメモリコンシューマーはデータベースごとに1つだけ存在します。)|  
|memory_consumer_type_desc|**nvarchar (64)**|メモリ コンシューマーの種類: VARHEAP、HASH、PGPOOL。<br /><br /> 0-(表示されません。)<br /><br /> 2-VARHEAP<br /><br /> 3-ハッシュ<br /><br /> 5 - PGPOOL|  
|memory_consumer_desc|**nvarchar (64)**|メモリ コンシューマー インスタンスの説明。<br /><br /> VARHEAP <br />データベースヒープ。 データベース (行) のユーザーデータを割り当てるために使用します。<br />データベースシステムヒープ。 メモリ ダンプに含められ、ユーザー データを含まないデータベース データを割り当てるために使用します。<br />範囲インデックスヒープ。 BW ページを割り当てるために範囲インデックスによって使用されるプライベート ヒープ。<br /><br /> HASH: object_id はテーブルとハッシュインデックス自体 index_id を示すため、説明はありません。<br /><br /> PGPOOL: データベースには、ページプールデータベース64K ページプールが1つだけ存在します。|  
|object_id|**bigint**|割り当てられたメモリに属性を適用する対象のオブジェクト ID。 システムオブジェクトに対して負の値を指定します。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルのオブジェクト ID。|  
|index_id|**int**|コンシューマーのインデックス ID (存在する場合)。 ベーステーブルの場合は NULL です。|  
|allocated_bytes|**bigint**|このコンシューマーのために予約されたバイト数。|  
|used_bytes|**bigint**|このコンシューマーによって使用されているバイト数。 VARHEAP のみに適用されます。|  
|allocation_count|**int**|割り当ての数。|  
|partition_count|**int**|内部使用のみです。|  
|sizeclass_count|**int**|内部使用のみです。|  
|min_sizeclass|**int**|内部使用のみです。|  
|max_sizeclass|**int**|内部使用のみです。|  
|memory_consumer_address|**varbinary**|コンシューマーの内部アドレス。 内部使用のみ。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルに対応するインメモリ OLTP オブジェクト ID。|  
  
## <a name="remarks"></a>解説  
 出力では、データベース レベルのアロケーターは、ユーザー テーブル、インデックス、およびシステム テーブルを参照します。 object_id = NULL の VARHEAP は、可変長列を含むテーブルに割り当てられたメモリを参照します。  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限を持っている場合は、すべての行が返されます。 それ以外の場合は、空の行セットが返されます。  
  
 VIEW DATABASE 権限がない場合は、SELECT 権限を持っているテーブル内の行に対するすべての列が返されます。  
  
 システム テーブルは、VIEW DATABASE STATE 権限を持つユーザーにのみ返されます。  
  
## <a name="general-remarks"></a>全般的な解説  
 メモリ最適化テーブルに列ストアインデックスがある場合、システムでは、一部のメモリを消費する内部テーブルを使用して、列ストアインデックスのデータを追跡します。 これらの内部テーブルと、メモリ使用量を示すサンプルクエリの詳細については、「 [memory_optimized_tables_internal_attributes (transact-sql)](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md)」を参照してください。
 
  
## <a name="examples"></a>例  
  
```  
-- memory consumers (database level)  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_memory_consumers;  
```  
  
## <a name="user-scenario"></a>ユーザーシナリオ  
  
```  
-- memory consumers (database level)  
  
select  convert(char(10), object_name(object_id)) as Name,   
convert(char(10),memory_consumer_type_desc ) as memory_consumer_type_desc, object_id,index_id, allocated_bytes,  used_bytes   
from sys.dm_db_xtp_memory_consumers  
```  
  
 列の一部の出力例を次に示します。 データベースレベルのアロケーターは、ユーザーテーブル、インデックス、およびシステムテーブルを参照します。 Object_id = NULL (最後の行) の VARHEAP は、テーブルのデータ行に割り当てられたメモリを参照します (この例では t1)。 割り当てられたバイト数は、MB 換算で 1340 MB です。  
  
```  
Name       memory_consumer_type_desc object_id   index_id    allocated_bytes      used_bytes  
---------- ------------------------- ----------- ----------- -------------------- --------------------  
t3         HASH                      629577281   2           8388608              8388608  
t2         HASH                      597577167   2           8388608              8388608  
t1         HASH                      565577053   2           1048576              1048576  
NULL       HASH                      -6          1           2048                 2048  
NULL       VARHEAP                   -6          NULL        0                    0  
NULL       HASH                      -5          3           8192                 8192  
NULL       HASH                      -5          2           8192                 8192  
NULL       HASH                      -5          1           8192                 8192  
NULL       HASH                      -4          1           2048                 2048  
NULL       VARHEAP                   -4          NULL        0                    0  
NULL       HASH                      -3          1           2048                 2048  
NULL       HASH                      -2          2           8192                 8192  
NULL       HASH                      -2          1           8192                 8192  
NULL       VARHEAP                   -2          NULL        196608               26496  
NULL       HASH                      0           1           2048                 2048  
NULL       PGPOOL                    0           NULL        0                    0  
NULL       VARHEAP                   NULL        NULL        1405943808           1231220560  
  
(17 row(s) affected)  
```  
  
 この DMV から割り当てられて使用されるメモリの合計は、 [sys. dm_db_xtp_table_memory_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)のオブジェクトレベルと同じです。  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
        sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1358                 1191  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
