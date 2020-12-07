---
description: sys.dm_db_incremental_stats_properties (Transact-SQL)
title: dm_db_incremental_stats_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_incremental_stats_properties
- sys.dm_db_incremental_stats_properties_TSQL
- dm_db_incremental_stats_properties
- dm_db_incremental_stats_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_incremental_stats_properties
ms.assetid: aa0db893-34d1-419c-b008-224852e71307
author: markingmyname
ms.author: maghan
ms.openlocfilehash: caa090c1835c34bd2d1da6d6b3bcb6caa4077217
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544811"
---
# <a name="sysdm_db_incremental_stats_properties-transact-sql"></a>sys.dm_db_incremental_stats_properties (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内にある指定されたデータベース オブジェクト (テーブル) について、増分統計のプロパティを返します。 `sys.dm_db_incremental_stats_properties` (パーティション番号を含む) の使用方法は、非増分統計に使用される `sys.dm_db_stats_properties` と似ています。 
  
  この機能は [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] 、Service pack 2 および [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] service pack 1 で導入されました。
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_db_incremental_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>引数  
 *object_id*  
 増分統計のプロパティが要求された、現在のデータベース内にあるオブジェクトの ID です。 *object_id* は **int**です。  
  
 *stats_id*  
 指定された *object_id*の統計情報の ID です。 統計 ID は、 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 動的管理ビューから取得できます。 *stats_id* は **int**です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|統計オブジェクトのプロパティを返す対象であるオブジェクト (テーブル) の ID。|  
|stats_id|**int**|統計オブジェクトの ID。 テーブル内で一意です。 詳細については、「[sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)」を参照してください。|
|partition_number|**int**|テーブルのその部分を含むパーティション番号。|  
|last_updated|**datetime2**|オブジェクトが最後に更新された日付と時刻。 詳細については、このページの「[解説](#Remarks)」セクションを参照してください。|  
|rows|**bigint**|統計情報が最後に更新された時点のテーブルの行の総数。 統計がフィルター選択されている場合、またはフィルター選択されたインデックスに対応している場合は、行数がテーブルの行数よりも少なくなることがあります。|  
|rows_sampled|**bigint**|統計の計算時にサンプリングされた行の合計数。|  
|steps|**int**|ヒストグラムの区間の数。 詳細については、「[DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)」を参照してください。|  
|unfiltered_rows|**bigint**|フィルター式を適用する前のテーブル内の行の合計数 (フィルター選択された統計情報の場合)。 統計がフィルター選択されていない場合は unfiltered_rows は行の列に返される値と同じです。|  
|modification_counter|**bigint**|統計情報が前回更新されてから先頭の統計列 (構築するヒストグラムの基になる列) に対して行われた変更の総数。<br /><br /> この列には、メモリ最適化テーブルの情報が含まれません。|  
  
## <a name="remarks"></a><a name="Remarks"></a> 解説  
 `sys.dm_db_incremental_stats_properties` は、次のいずれかの条件に該当した場合に空の行セットを返します。  
  
-   `object_id` または `stats_id` が NULL です。   
-   指定したオブジェクトが見つからないか、増分統計を含むテーブルに対応しない。  
-   指定した統計 ID が、指定したオブジェクト ID の既存の統計情報に対応しない。  
-   現在のユーザーに統計オブジェクトを表示する権限がない。
 
 この動作によって、 `sys.dm_db_incremental_stats_properties` や `sys.objects` などのビュー内の行へのクロス適用時に、 `sys.stats`を安全に使用できます。 このメソッドで、各パーティションに対応する統計情報のプロパティを返すことができます。 すべてのパーティションをまとめてマージした統計情報のプロパティを表示するには、代わりに sys.dm_db_stats_properties を使用します。 

統計の更新日付は、メタデータではなく[統計 BLOB オブジェクト](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)に[ヒストグラム](../../relational-databases/statistics/statistics.md#histogram)および[密度ベクトル](../../relational-databases/statistics/statistics.md#density)と共に格納されます。 統計データを生成するためのデータが読み取られない場合、統計 blob は作成されず、日付は使用できず、 *last_updated* 列は NULL になります。 これは、述語が行を返さないフィルター選択された統計情報や、新しい空のテーブルの場合です。

## <a name="permissions"></a>アクセス許可  
 では、ユーザーが統計列に対する select 権限を持っているか、ユーザーがテーブルを所有しているか、固定 `sysadmin` サーバーロール、 `db_owner` 固定データベースロール、または固定データベースロールのメンバーである必要があり `db_ddladmin` ます。  
  
## <a name="examples"></a>例  

### <a name="a-simple-example"></a>A. 簡単な例
次の例は、「 `PartitionTable` パーティション テーブルとパーティション インデックスの作成 [」トピックで説明されている](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)テーブルの統計情報を返します。

```sql
SELECT * FROM sys.dm_db_incremental_stats_properties (object_id('PartitionTable'), 1);
``` 

その他の使用の推奨事項については、「  [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)」を参照してください。
  
## <a name="see-also"></a>参照  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [オブジェクト関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
