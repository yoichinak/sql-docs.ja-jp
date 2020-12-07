---
description: C Interval 構造体
title: C Interval 構造体 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89962558fdbd6f0de5b5e030fe504669d51c40be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411208"
---
# <a name="c-interval-structure"></a>C Interval 構造体
「 [C データ型](../../../odbc/reference/appendixes/c-data-types.md) 」セクションに記載されている各 c interval データ型は、同じ構造を使用して間隔データを格納します。 **Sqlfetch**、 **sqlfetchscroll**、または**SQLGetData**が呼び出されると、ドライバーはデータを SQL_INTERVAL_STRUCT 構造に返し、c データ型に対してアプリケーションによって指定された値 ( **SQLBindCol**、 **SQLGetData**、または**SQLBindParameter**の呼び出し) を使用して SQL_INTERVAL_STRUCT の内容を解釈し、構造体の*interval_type*フィールドに c 型に対応する*列挙*値を設定します。 ドライバーは、間隔の種類を決定するために *interval_type* フィールドを読み取っていないことに注意してください。SQL_DESC_CONCISE_TYPE 記述子フィールドの値を取得します。 パラメーターデータに構造体が使用されている場合、ドライバーは、アプリケーションが *interval_type* フィールドの値を別の値に設定した場合でも、APD の SQL_DESC_CONCISE_TYPE フィールドにあるアプリケーションで指定された値を使用して SQL_INTERVAL_STRUCT の内容を解釈します。  
  
 この構造体は次のように定義されています。  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 SQL_INTERVAL_STRUCT の [ *interval_type* ] フィールドは、共用体に保持されている構造と、その構造のどのメンバーが関連しているかをアプリケーションに示します。 間隔の先頭フィールドが符号なしの場合、 *interval_sign* フィールドには SQL_FALSE 値があります。SQL_TRUE の場合、先頭のフィールドは負の値になります。 先頭フィールド自体の値は、 *interval_sign*の値に関係なく、常に符号なしです。 *Interval_sign*フィールドは、符号ビットとして機能します。
