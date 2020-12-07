---
description: DBCC PDW_SHOWSPACEUSED (Transact-SQL)
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL)
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8c7ca98b19a801daa73367ee50df525ab43d1406
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722093"
---
# <a name="dbcc-pdw_showspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベースの特定のテーブルまたはすべてのテーブルの行数、予約済みのディスク領域、使用済みのディスク領域を表示します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文
  
```syntaxsql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>引数

 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
表示される 1 部、2 部、または 3 部構成のテーブル名。 2 部または 3 部構成のテーブル名は、二重引用符 ("") で囲む必要があります。 1 部構成のテーブル名を囲む引用符を使用することは省略できます。 テーブル名が指定されていない場合は、現在のデータベースの情報が表示されます。  
  
## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。
  
## <a name="result-sets"></a>結果セット

これは、すべてのテーブルの結果セットです。  レプリケートされた Synapse テーブルのキャッシュが作成される前に、DBCC の結果には、各ディストリビューションの基になるラウンド ロビン テーブルの合計サイズが反映されます。  キャッシュが作成された後の結果には、ラウンド ロビン テーブルとキャッシュの合計サイズが反映されます。   
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|reserved_space|bigint|データベースに使用されている合計領域 (KB 単位)。|  
|data_space|bigint|データに使用されている領域 (KB 単位)。|  
|index_space|bigint|インデックスに使用されている領域 (KB 単位)。|  
|unused_space|bigint|予約済み領域の一部で使用されていない領域 (KB 単位)。|  
|pdw_node_id|INT|データに使用されているコンピューティング ノード。|  
  
これは、1 つのテーブルの結果セットです。
  
|列|データ型|説明|Range|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|行の数。||  
|reserved_space|bigint|オブジェクトに予約されている合計領域 (KB 単位)。||  
|data_space|bigint|データに使用されている領域 (KB 単位)。||  
|index_space|bigint|インデックスに使用されている領域 (KB 単位)。||  
|unused_space|bigint|予約済み領域の一部で使用されていない領域 (KB 単位)。||  
|pdw_node_id|INT|領域の使用状況の報告に使用されるコンピューティング ノード。||  
|distribution_id|INT|領域の使用状況の報告に使用されるディストリビューション。|Parallel Data Warehouse の場合、レプリケートされたテーブルのその値は -1 です。|  
  
## <a name="examples-sssdw-and-sspdw"></a>例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED の基本的な構文  
次の例では、[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] データベースの FactInternetSales テーブルの行数、予約済みのディスク領域、使用済みのディスク領域を表示する複数の方法を示します。
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. 現在のデータベース内のすべてのテーブルで使用されているディスク領域を表示する  

 次の例では、[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] のすべてのユーザー テーブルとシステム テーブルで使用される予約済みのディスク領域を示します。  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  

## <a name="see-also"></a>参照

- [DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
- [DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)
