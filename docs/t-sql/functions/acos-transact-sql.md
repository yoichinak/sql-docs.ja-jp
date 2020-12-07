---
description: ACOS (Transact-SQL)
title: ACOS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ACOS
- ACOS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- ACOS function
- arccosine
ms.assetid: 4ec6b46e-9438-4f0f-8b96-461edd84280a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7d40695c1f9edef75f66c93e9e7cc7f3c6e8769
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96119548"
---
# <a name="acos-transact-sql"></a>ACOS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

角度 (ラジアン) を返す関数。コサインは、指定された float 式です。 これは、アークコサイン (逆余弦) とも呼ばれます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
ACOS ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*float_expression*  
**float** 型、または暗黙的に float 型に変換できる [式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 -1.00 ～ 1.00 の範囲の値のみが有効です。 この範囲外の値を指定すると、NULL が返され、ASIN がドメイン エラーを報告します。
  
## <a name="return-types"></a>戻り値の型  
**float**
  
## <a name="examples"></a>例  
この例では、指定された数値の `ACOS` 値が返されます。
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos FLOAT;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(VARCHAR, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>関連項目
[数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[関数](../../t-sql/functions/functions.md)
  
  

