---
title: "SMALLDATETIMEFROMPARTS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/04/2017
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
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs: TSQL
helpviewer_keywords: SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07eaaf385e0227f3e5ddf7d0c1ee506aecca211a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  指定された日付と時刻を表す **smalldatetime** 値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
## <a name="arguments"></a>引数  
 *year*  
 年を指定する整数式。  
  
 *month*  
 月を指定する整数式。  
  
 *day*  
 日を指定する整数式。  
  
 *hour*  
 時間を指定する整数式。  
  
 *minute*  
 分を指定する整数式。  
  
## <a name="return-types"></a>戻り値の型  
 **smalldatetime**  
  
## <a name="remarks"></a>解説  
 この関数は、完全に初期化された **smalldatetime** 値のコンストラクターとして機能します。 引数が有効でない場合は、エラーがスローされます。 必要な引数が NULL の場合は、NULL が返されます。  
  
 この関数は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以上のサーバーに対してリモート処理が可能です。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] より前のバージョンをインストールしているサーバーには、リモート処理が行われません。  
  
## <a name="examples"></a>使用例  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  

