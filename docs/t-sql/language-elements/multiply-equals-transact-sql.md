---
description: '*= (乗算代入) (Transact-SQL)'
title: '*= (乗算代入) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '*=_TSQL'
- '*='
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, *=
- assignment operators, *=
- augmented operators, *=
- '*= (multiply equals)'
- '*= (multiplication assignment)'
ms.assetid: 816ff5dc-9a40-4c07-8351-39c194dbc079
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 96b003987e52dbb6bf20f3606833f9d33355e727
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128225"
---
# <a name="-multiplication-assignment-transact-sql"></a>*= (乗算代入) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

2 つの数値を乗算し、値に演算の結果を設定します。 たとえば、変数 @x が 35 である場合、@x *= 2 は @x の元の値を取得し、2 を乗算して、@x にその新しい値 (70) を設定します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
expression *= expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
_式 (expression)_  
数値型に分類される任意のデータ型を持つ有効な [式](../../t-sql/language-elements/expressions-transact-sql.md)です。ただし、**bit** データ型は除きます。  
  
## <a name="result-types"></a>戻り値の型  
優先順位が高い引数のデータ型を返します。 詳細については、「[データ型の優先順位 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
詳細については、「[&#42; &#40;乗算&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[複合演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
[演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
