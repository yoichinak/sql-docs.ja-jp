---
description: 'C から SQL へ: 日付と時刻の間隔'
title: 'C から SQL へ: 日付と時刻の間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aba5bb40a34f100cf33d5c07fb6e796b227904dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499995"
---
# <a name="c-to-sql-day-time-intervals"></a>C から SQL へ: 日付と時刻の間隔
日付と時刻の間隔の ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 次の表は、interval C データの変換先となる ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|列のバイト長 >= 文字バイト長<br /><br /> 列のバイト長 < 文字のバイト長 [a]<br /><br /> データ値は有効な間隔リテラルではありません|該当なし<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|列の文字長 >= データの文字長<br /><br /> 列文字の長さ < データの文字の長さ [a]<br /><br /> データ値は有効な間隔リテラルではありません|該当なし<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b] SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b] SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|単一フィールドの間隔の変換によって、整数の切り捨てが行われませんでした<br /><br /> 変換の結果、整数の切り捨てが行われる|該当なし<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|データ値は、フィールドを切り捨てずに変換されました<br /><br /> 変換中に1つ以上のデータ値のフィールドが切り捨てられました|該当なし<br /><br /> 22015|  
  
 [a] すべての C interval データ型を文字データ型に変換できます。  
  
 [b] interval 構造体の type フィールドが、間隔が1つのフィールド (SQL_DAY、SQL_HOUR、SQL_MINUTE、または SQL_SECOND) である場合、C の種類の間隔は任意の正確な数値 (SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL、または SQL_NUMERIC) に変換できます。  
  
 間隔 C 型の既定の変換は、対応する日時間隔の SQL 型になります。  
  
 データを interval C データ型から変換する場合、ドライバーは長さとインジケーターの値を無視し、データバッファーのサイズが interval C データ型のサイズであることを前提としています。 長さ/インジケーターの値は、 **Sqlputdata**の*StrLen_or_Ind*引数と、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定されたバッファーに渡されます。 データバッファーは、 **Sqlputdata**の*DataPtr*引数と**SQLBindParameter**の*parametervalueptr*引数を使用して指定します。  
  
 次の例では、SQL_INTERVAL_STRUCT 構造に格納されている期間 C データをデータベース列に送信する方法を示します。 Interval 構造体には DAY_TO_SECOND の間隔が含まれます。SQL_INTERVAL_DAY_TO_MINUTE 型のデータベース列に格納されます。  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
