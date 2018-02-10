---
title: "CHECKSUM_AGG (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs: TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3499cd8fb118d12fdbf450c23f2919fd0003cee7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

グループ内にある値のチェックサムを返します。 NULL 値は無視されます。 後に、 [OVER 句](../../t-sql/queries/select-over-clause-transact-sql.md)が続く場合があります。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>引数  
**ALL**  
すべての値にこの集計関数を適用します。 ALL が既定値です。
  
DISTINCT  
CHECKSUM_AGG で、一意な値のチェックサムを返します。
  
*expression*  
整数[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 集計関数とサブクエリは許可されません。
  
## <a name="return-types"></a>戻り値の型
すべての *expression* 値のチェックサムが **int** 型で返されます。
  
## <a name="remarks"></a>解説  
CHECKSUM_AGG は、テーブル内の変更を検出する場合に使用できます。
  
テーブル内での行の順序は、CHECKSUM_AGG の結果に影響しません。 また、CHECKSUM_AGG 関数は、DISTINCT キーワードおよび GROUP BY 句と共に使用できます。
  
いずれかの式の値を変更した場合は通常、そのリストのチェックサムも変わりますが、 チェックサムが変わらない場合もわずかですがあります。
  
CHECKSUM_AGG には、他の集計関数とほぼ同じ機能があります。 詳細については、「[集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)」を参照してください。
  
## <a name="examples"></a>使用例  
次の例では、`CHECKSUM_AGG` を使って、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `ProductInventory` テーブルにある `Quantity` 列の変更を検出します。
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>参照
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
