---
description: SQUARE (Transact-SQL)
title: SQUARE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- SQUARE
- SQUARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: 007b6b12-da86-4229-8f5c-fdd4fa839f5f
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7517f8ca9049bdde045e18d97a71c2b5c73fc7b7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99177972"
---
# <a name="square-transact-sql"></a>SQUARE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  指定した浮動小数点値の 2 乗を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
SQUARE ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *float_expression*  
 **float** 型、または暗黙的に float 型に変換できる [式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 **float**  
  
## <a name="examples"></a>例  
 次の例では、半径が `1` インチで高さが `5` インチの円柱の体積を返します。  
  
```sql  
DECLARE @h FLOAT, @r FLOAT;  
SET @h = 5;  
SET @r = 1;  
SELECT PI()* SQUARE(@r)* @h AS 'Cyl Vol';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Cyl Vol  
--------------------------  
15.707963267948966  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、`volume` テーブル内の `containers` 列の値の 2 乗を返します。  
  
```sql  
-- Uses AdventureWorks  
  
CREATE TABLE Containers (  
    ID INT NOT NULL,  
    Name VARCHAR(20),  
    Volume FLOAT(24));  
  
INSERT INTO Containers VALUES (1, 'Cylinder', '125.22');  
INSERT INTO Containers VALUES (2, 'Cube', '23.98');  
  
SELECT Name, SQUARE(Volume) AS VolSquared   
FROM Containers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Name           VolSquared
-------------  ----------
Cylinder       15680.05
Cube             575.04
```  
  
## <a name="see-also"></a>参照  
 [数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

