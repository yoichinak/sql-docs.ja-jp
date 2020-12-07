---
description: sys.dm_db_stats_histogram (Transact-SQL)
title: dm_db_stats_histogram (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_stats_histogram
- sys.dm_db_stats_histogram_TSQL
- dm_db_stats_histogram
- dm_db_stats_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_histogram dynamic management function
ms.assetid: 1897fd4a-8d51-461e-8ef2-c60be9e563f2
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af4e3e3739475ff3beac61802606499874fdff58
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91117002"
---
# <a name="sysdm_db_stats_histogram-transact-sql"></a>sys.dm_db_stats_histogram (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

現在のデータベース内の指定されたデータベースオブジェクト (テーブルまたはインデックス付きビュー) の統計ヒストグラムを返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 `DBCC SHOW_STATISTICS WITH HISTOGRAM` に似ています。

> [!NOTE] 
> この DMF は、SP1 CU2 以降で使用できます。 [!INCLUDE[ssSQL15](../../includes/ssSQL15-md.md)]

## <a name="syntax"></a>構文  
  
```  
sys.dm_db_stats_histogram (object_id, stats_id)  
```  
  
## <a name="arguments"></a>引数  
 *object_id*  
 統計のプロパティが要求された、現在のデータベース内にあるオブジェクトの ID です。 *object_id* は **int**です。  
  
 *stats_id*  
 指定された *object_id*の統計情報の ID です。 統計 ID は、 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 動的管理ビューから取得できます。 *stats_id* は **int**です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id |**int**|統計オブジェクトのプロパティを返す対象のオブジェクト (テーブルまたはインデックス付きビュー) の ID。|  
|stats_id |**int**|統計オブジェクトの ID。 テーブルまたはインデックス付きビュー内で一意です。 詳細については、「[sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)」を参照してください。|  
|step_number |**int** |ヒストグラムのステップ数。 |
|range_high_key |**sql_variant** |ヒストグラム区間の上限の列値。 この列値はキー値とも呼ばれます。|
|range_rows |**real** |ヒストグラム区間内 (上限は除く) に列値がある行の予測数。 |
|equal_rows |**real** |ヒストグラム区間の上限と列値が等しい行の予測数。 |
|distinct_range_rows |**bigint** |ヒストグラム区間内 (上限は除く) にある個別の列値を持つ行の予測数。 |
|average_range_rows |**real** |上限を除く、ヒストグラムのステップ内で重複する列値を持つ行の平均数 ( `RANGE_ROWS / DISTINCT_RANGE_ROWS` の場合 `DISTINCT_RANGE_ROWS > 0` )。 |
  
 ## <a name="remarks"></a>解説  
 
 の resultset は `sys.dm_db_stats_histogram` 、と同様の情報を返し `DBCC SHOW_STATISTICS WITH HISTOGRAM` ます。また、、、およびも含まれ `object_id` `stats_id` `step_number` ます。

 列 `range_high_key` は sql_variant のデータ型であるため、 `CAST` 述語が `CONVERT` 文字列以外の定数と比較する場合は、またはを使用する必要がある場合があります。

### <a name="histogram"></a>ヒストグラム
  
 ヒストグラムでは、データセットの個別の値ごとに出現頻度を測定します。 クエリ オプティマイザーでは、統計オブジェクトの最初のキー列の列値に基づいてヒストグラムを計算し、行を統計的にサンプリングするかテーブルまたはビュー内のすべての行でフル スキャンを実行することによって列値を選択します。 サンプリングされた行のセットからヒストグラムを作成する場合、格納される行の総数および個別の値の数は推定値であり、必ずしも整数にはなりません。  
  
 ヒストグラムを作成するには、クエリ オプティマイザーで列値を並べ替え、個別の列値ごとに一致する値の数を計算し、列値を最大 200 の連続したヒストグラム区間に集計します。 各区間には、上限の列値までの列値の範囲が含まれます。 この範囲には、境界値の間 (境界値自体は除く) のすべての有効な列値が含まれます。 格納される最小の列値は、最初のヒストグラム区間の上限境界値になります。  
  
 次の図は、6 つの区間があるヒストグラムを示しています。 最初の上限境界値の左側にある領域が最初の区間です。  
  
 ![ヒストグラム](../../relational-databases/system-dynamic-management-views/media/histogram-2.svg "ヒストグラム")  
  
 ヒストグラムの各区間は、以下のように表されます。  
  
-   太線は、上限境界値 (*range_high_key*) およびその出現回数 (*equal_rows*) を表します。  
  
-   *range_high_key* の左にある領域は、列値の範囲、およびそれぞれの列値の平均出現回数 (*average_range_rows*) を表します。 最初のヒストグラム区間の *average_range_rows* は常に 0 です。  
  
-   点線は、範囲内にある個別の値の総数 (*distinct_range_rows*) および範囲内の値の総数 (*range_rows*) を推定するために使用されるサンプリングされた値を表します。 クエリ オプティマイザーでは、*range_rows* および *distinct_range_rows* を使用して *average_range_rows* を計算します。サンプリングされた値は格納されません。  
  
 クエリ オプティマイザーでは、統計的有意性に応じてヒストグラム区間を定義します。 区間幅を最大にするアルゴリズムを使用して境界値の差を最大にし、ヒストグラムの区間の数を最小限に抑えます。 区間の最大数は 200 です。 ヒストグラムの区間の数は、境界点が 200 より少ない列でも、個別の値の数より少なくなることがあります。 たとえば、個別の値が 100 個ある列のヒストグラムの境界点が 100 より少なくなる場合もあります。  
  
## <a name="permissions"></a>アクセス許可  

では、ユーザーが統計列に対する select 権限を持っているか、ユーザーがテーブルを所有しているか、固定 `sysadmin` サーバーロール、 `db_owner` 固定データベースロール、または固定データベースロールのメンバーである必要があり `db_ddladmin` ます。

## <a name="examples"></a>例  

### <a name="a-simple-example"></a>A. 簡単な例    
次の例では、単純なテーブルを作成して設定します。 次に、列に対して統計を作成し `Country_Name` ます。

```sql
CREATE TABLE Country
(Country_ID int IDENTITY PRIMARY KEY,
Country_Name varchar(120) NOT NULL);
INSERT Country (Country_Name) VALUES ('Canada'), ('Denmark'), ('Iceland'), ('Peru');

CREATE STATISTICS Country_Stats  
    ON Country (Country_Name) ;  
```   
主キーは `stat_id` 数値1を占有するため、数値2を呼び出して、 `sys.dm_db_stats_histogram` `stat_id` テーブルの統計ヒストグラムを返し `Country` ます。    
```sql     
SELECT * FROM sys.dm_db_stats_histogram(OBJECT_ID('Country'), 2);
```

### <a name="b-useful-query"></a>B. 便利なクエリ:   
```sql  
SELECT hist.step_number, hist.range_high_key, hist.range_rows, 
    hist.equal_rows, hist.distinct_range_rows, hist.average_range_rows
FROM sys.stats AS s
CROSS APPLY sys.dm_db_stats_histogram(s.[object_id], s.stats_id) AS hist
WHERE s.[name] = N'<statistic_name>';
```

### <a name="c-useful-query"></a>C. 便利なクエリ:
次の例では、列の述語を含むテーブルからを選択し `Country` `Country_Name` ます。

```sql  
SELECT * FROM Country 
WHERE Country_Name = 'Canada';
```

次の例では、 `Country` 上記のクエリの述語に `Country_Name` 一致するヒストグラムのステップのテーブルと列に対して以前に作成した統計を確認します。

```sql  
SELECT ss.name, ss.stats_id, shr.steps, shr.rows, shr.rows_sampled, 
    shr.modification_counter, shr.last_updated, sh.range_rows, sh.equal_rows
FROM sys.stats ss
INNER JOIN sys.stats_columns sc 
    ON ss.stats_id = sc.stats_id AND ss.object_id = sc.object_id
INNER JOIN sys.all_columns ac 
    ON ac.column_id = sc.column_id AND ac.object_id = sc.object_id
CROSS APPLY sys.dm_db_stats_properties(ss.object_id, ss.stats_id) shr
CROSS APPLY sys.dm_db_stats_histogram(ss.object_id, ss.stats_id) sh
WHERE ss.[object_id] = OBJECT_ID('Country') 
    AND ac.name = 'Country_Name'
    AND sh.range_high_key = CAST('Canada' AS CHAR(8));
```
  
## <a name="see-also"></a>参照  
[DBCC SHOW_STATISTICS (Transact-sql)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
[オブジェクト関連の動的管理ビューおよび関数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
