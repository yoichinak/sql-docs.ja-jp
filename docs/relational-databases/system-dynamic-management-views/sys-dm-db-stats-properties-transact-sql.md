---
description: sys.dm_db_stats_properties (Transact-SQL)
title: dm_db_stats_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_stats_properties_TSQL
- sys.dm_db_stats_properties
- dm_db_stats_properties_TSQL
- dm_db_stats_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_properties
ms.assetid: 8a54889d-e263-4881-9fcb-b1db410a9453
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1039850e4322003ddfedd5407d18ab6170077c42
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537034"
---
# <a name="sysdm_db_stats_properties-transact-sql"></a>sys.dm_db_stats_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベース内の指定されたデータベースオブジェクト (テーブルまたはインデックス付きビュー) の統計のプロパティを返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 パーティションテーブルについては、同様の [dm_db_incremental_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)を参照してください。 
 
## <a name="syntax"></a>構文  
  
```  
sys.dm_db_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>引数  
 *object_id*  
 統計のプロパティが要求された、現在のデータベース内にあるオブジェクトの ID です。 *object_id* は **int**です。  
  
 *stats_id*  
 指定された *object_id*の統計情報の ID です。 統計 ID は、 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 動的管理ビューから取得できます。 *stats_id* は **int**です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|統計オブジェクトのプロパティを返す対象のオブジェクト (テーブルまたはインデックス付きビュー) の ID。|  
|stats_id|**int**|統計オブジェクトの ID。 テーブルまたはインデックス付きビュー内で一意です。 詳細については、「[sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)」を参照してください。|  
|last_updated|**datetime2**|オブジェクトが最後に更新された日付と時刻。 詳細については、このページの「[解説](#Remarks)」セクションを参照してください。|  
|rows|**bigint**|統計が最後に更新されたときのテーブルまたはインデックス付きビュー内の行の合計数。 統計がフィルター選択されている場合、またはフィルター選択されたインデックスに対応している場合は、行数がテーブルの行数よりも少なくなることがあります。|  
|rows_sampled|**bigint**|統計の計算時にサンプリングされた行の合計数。|  
|steps|**int**|ヒストグラムの区間の数。 詳細については、「[DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)」を参照してください。|  
|unfiltered_rows|**bigint**|フィルター式を適用する前のテーブル内の行の合計数 (フィルター選択された統計情報の場合)。 統計がフィルター選択されていない場合は unfiltered_rows は行の列に返される値と同じです。|  
|modification_counter|**bigint**|統計情報が前回更新されてから先頭の統計列 (構築するヒストグラムの基になる列) に対して行われた変更の総数。<br /><br /> メモリ最適化テーブル: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] この列の先頭と末尾には、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 統計が最後に更新された後、またはデータベースが再起動されてからの、テーブルに対する変更の合計数が含まれます。|  
|persisted_sample_percent|**float**|サンプリングの割合を明示的に指定しない統計情報の更新に使用される永続化されたサンプルのパーセンテージです。 値がゼロの場合、永続化されたサンプルのパーセンテージがこの統計に設定されていません。<br /><br /> **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4|  
  
## <a name="remarks"></a><a name="Remarks"></a> 解説  
 **dm_db_stats_properties** は、次のいずれかの条件に該当する場合に空の行セットを返します。  
  
-   **object_id** または **stats_id** が NULL です。    
-   指定されたオブジェクトが見つからないか、テーブルまたはインデックス付きビューに対応していません。    
-   指定した統計 ID が、指定したオブジェクト ID の既存の統計情報に対応しない。    
-   現在のユーザーに統計オブジェクトを表示する権限がない。  
  
 この動作により、sys. **objects**や**sys**などのビューの行にクロス適用された場合に、 **dm_db_stats_properties**を安全に使用できるようになります。  
 
統計の更新日付は、メタデータではなく[統計 BLOB オブジェクト](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)に[ヒストグラム](../../relational-databases/statistics/statistics.md#histogram)および[密度ベクトル](../../relational-databases/statistics/statistics.md#density)と共に格納されます。 統計データを生成するためのデータが読み取られない場合、統計 blob は作成されず、日付は使用できず、 *last_updated* 列は NULL になります。 これは、述語が行を返さないフィルター選択された統計情報や、新しい空のテーブルの場合です。
  
## <a name="permissions"></a>アクセス許可  
 では、ユーザーが統計列に対する select 権限を持っているか、ユーザーがテーブルを所有しているか、固定 `sysadmin` サーバーロール、 `db_owner` 固定データベースロール、または固定データベースロールのメンバーである必要があり `db_ddladmin` ます。  
  
## <a name="examples"></a>例  

### <a name="a-simple-example"></a>A. 簡単な例
次の例では、AdventureWorks データベース内のテーブルの統計を返し `Person.Person` ます。

```sql
SELECT * FROM sys.dm_db_stats_properties (object_id('Person.Person'), 1);
``` 
  
### <a name="b-returning-all-statistics-properties-for-a-table"></a>B. テーブルのすべての統計プロパティを返す  
 次の例では、テーブルテストに存在するすべての統計のプロパティを返します。  
  
```sql  
SELECT sp.stats_id, name, filter_definition, last_updated, rows, rows_sampled, steps, unfiltered_rows, modification_counter   
FROM sys.stats AS stat   
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE stat.object_id = object_id('TEST');  
```  
  
### <a name="c-returning-statistics-properties-for-frequently-modified-objects"></a>C. 頻繁に変更されるオブジェクトの統計プロパティを返す  
 次の例では、統計が前回更新されてからの先頭列の変更が 1,000 回を超える、現在のデータベース内にあるすべてのテーブル、インデックス付きビュー、および統計を返します。  
  
```sql  
SELECT obj.name, obj.object_id, stat.name, stat.stats_id, last_updated, modification_counter  
FROM sys.objects AS obj   
INNER JOIN sys.stats AS stat ON stat.object_id = obj.object_id  
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE modification_counter > 1000;  
```  
  
## <a name="see-also"></a>参照  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [オブジェクト関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys.dm_db_incremental_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)  
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  

