---
description: GROUPING (Transact-SQL)
title: GROUPING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1bc82a8f0afe1b2758a7c78a88b4813b7d103b4e
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114801"
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  GROUP BY リスト内の指定した列の式が集計されるかどうかを示します。 GROUPING は結果セットで、集計される場合は 1 を、集計されない場合は 0 を返します。 GROUPING は、GROUP BY が指定されている場合に、SELECT \<select> リスト、HAVING、ORDER BY 句でのみ使用できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
GROUPING ( <column_expression> )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 \<column_expression>  
 [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 句の列が含まれた列または式です。  
  
## <a name="return-types"></a>戻り値の型  
 **tinyint**  
  
## <a name="remarks"></a>解説  
 GROUPING は、標準の null 値から、ROLLUP、CUBE、または GROUPING SETS によって返される null 値を区別するために使用します。 ROLLUP、CUBE、または GROUPING SETS の演算結果として返される NULL 値は、NULL の特別な用途です。 これは、結果セット内の列プレースホルダーとして機能し、すべてを意味します。  
  
## <a name="examples"></a>例  
 次の例では、`SalesQuota` をグループ化し、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `SaleYTD` 額を集計します。 `GROUPING` 関数は、`SalesQuota` 列に適用されます。  
  
```sql 
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 結果セットは、`SalesQuota` の下に 2 つの NULL 値を示します。 最初の `NULL` 値は、テーブル内のこの列からの NULL 値で構成されるグループを表します。 2 番目の `NULL` 値は、ROLLUP の演算によって追加された集計行にあります。 集計行は、すべての `SalesQuota` グループについての `TotalSalesYTD` の総量を表し、`Grouping` 列の `1` によって示されます。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>参照  
 [GROUPING_ID &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
