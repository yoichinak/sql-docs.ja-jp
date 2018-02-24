---
title: "TRY_CAST (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
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
- TRY_CAST_TSQL
- TRY_CAST
dev_langs: TSQL
helpviewer_keywords: TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d5fa1af5399fcc790b7e4c542e2c90314daa36d6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="trycast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  キャストが成功した場合は、指定したデータ型にキャストされた値を返します。それ以外の場合は null を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>引数  
 *expression*  
 キャストされる値。 任意の有効な式。  
  
 *data_type*  
 *expression* をキャストするデータ型。  
  
 *length*  
 対象のデータ型の長さを指定する整数 (省略可能)。  
  
 許容される値の範囲は、*data_type* の値によって決まります。  
  
## <a name="return-types"></a>戻り値の型  
 キャストが成功した場合は、指定したデータ型にキャストされた値を返します。それ以外の場合は null を返します。  
  
## <a name="remarks"></a>解説  
 **TRY_CAST** は渡された値を使用して、指定された *data_type* への変換を試みます。 キャストが成功した場合、**TRY_CAST** は指定された *data_type* と同じ値を返します。エラーが発生した場合は null が返されます。 ただし、明示的に許可されない変換を要求すると、**TRY_CAST** はエラーが発生して失敗します。  
  
 **TRY_CAST** は予約された新しいキーワードではなく、すべての互換性レベルで使用可能です。 **TRY_CAST** がリモート サーバーに接続するときのセマンティクスは、**TRY_CONVERT** と同じです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-trycast-returns-null"></a>A. TRY_CAST が null を返す  
 キャストに失敗して TRY_CAST が null を返す場合の例を次に示します。  
  
```tsql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 次の例は、式を求められている形式にする必要があることを示しています。  
  
```tsql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-trycast-fails-with-an-error"></a>B. TRY_CAST でエラーが発生して失敗する  
 キャストが明示的に許可されていないときに TRY_CAST がエラーを返す場合の例を次に示します。  
  
```tsql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 このステートメントの結果はエラーです。整数を xml データ型にキャストすることはできないからです。  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>C. TRY_CAST が成功する  
 次の例は、式を求められている形式にする必要があることを示しています。  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
