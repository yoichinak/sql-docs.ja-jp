---
title: "ABS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs: TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9f96d651f179120fab6fabfb78d08cca84404bd1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定した数値式の絶対値 (正値) を返す数学関数です。 (`ABS` は負の値を正の値を変更します。 `ABS` は 0 または正の値には影響を与えません)。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>引数  
*numeric_expression*  
真数型または概数型の式を指定します。
  
## <a name="return-types"></a>戻り値の型  
*numeric_expression*と同じ型を返します。
  
## <a name="examples"></a>使用例  
次の例では、3 つの異なる値に対して `ABS` 関数を使用した結果を示します。
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
`ABS` 関数では、数値の絶対値が指定のデータ型で表現できる最大値を超えている場合、オーバーフロー エラーが返されることがあります。 たとえば、`int` データ型では `-2,147,483,648` ～ `2,147,483,647` の範囲の値のみを表現できますが、 符号付整数値 `-2,147,483,648` の絶対値を計算すると `int` データ型の正数の範囲を超えるので、オーバーフロー エラーが発生します。
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
次にエラー メッセージを示します。
  
"メッセージ 8115、レベル 16、状態 2、行 3"
  
"式をデータ型 int に変換中に演算のオーバーフロー エラーが発生しました"

  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[数学関数と #40 です。TRANSACT-SQL と #41 です。](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[組み込み関数 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

