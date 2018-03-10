---
title: "DATEFROMPARTS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/29/2017
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
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs: TSQL
helpviewer_keywords: DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 73d2edfd6f0d19c4383b0bdbe1271d74a0ef2b6f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

指定された年、月、および日を表す **date** 値を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>引数  
*year*  
年を指定する整数式。
  
*month*  
1 ～ 12 の月を指定する整数式。
  
*day*  
日を指定する整数式。
  
## <a name="return-types"></a>戻り値の型
**date**
  
## <a name="remarks"></a>解説  
**DATEFROMPARTS** は、日付部分が指定の年月日に設定され、時間部分が既定値に設定されている **date** の値を返します。 引数が有効でない場合は、エラーが発生します。 必要な引数が null の場合は、null が返されます。
  
この関数は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以上のサーバーに対してリモート処理が可能です。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] より前のバージョンのサーバーには、リモート処理が行われません。
  
## <a name="examples"></a>使用例  
次の例では、**DATEFROMPARTS** 関数を示します。
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照
[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  

