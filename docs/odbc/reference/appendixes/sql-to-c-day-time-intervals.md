---
description: 'SQL から C へ: 日付と時刻の間隔'
title: 'SQL から C へ: 日付と時刻の間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3c878434a6fc3b2dcbb8b09a4acfb41ecf44a84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429574"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL から C へ: 日付と時刻の間隔

日付と時刻の間隔の ODBC SQL データ型の識別子は次のとおりです。

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

次の表は、SQL データが変換される日付と時刻の間隔を示す ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。

|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|すべての日付と時刻の C の間隔の種類|末尾のフィールド部分が切り捨てられていません<br /><br /> 末尾のフィールドの一部が切り捨てられました<br /><br /> ターゲットの先頭の有効桁数が、ソースからのデータを保持するのに十分な大きさではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの長さ<br /><br /> データの長さ<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|間隔の有効桁数が1つのフィールドであり、切り捨てずにデータが変換されました<br /><br /> 間隔の有効桁数は1つのフィールドと切り捨てられた小数部です<br /><br /> 間隔の精度は1つのフィールドで、全体が切り捨てられました<br /><br /> 間隔の有効桁数が1つのフィールドではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> データの長さ<br /><br /> データの長さ<br /><br /> C データ型のサイズ|該当なし<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 未定義。|データの長さ<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_CHAR|文字のバイト長 < *Bufferlength*<br /><br /> *Bufferlength* < 整数 (小数部ではなく) の数字<br /><br /> 整数の桁数 (小数部ではなく) >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|文字の長さ < *Bufferlength*<br /><br /> *Bufferlength* < 整数 (小数部ではなく) の数字<br /><br /> 整数の桁数 (小数部ではなく) >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 日付と時刻の間隔の SQL 型は、任意の日時の間隔 C 型に変換できます。  
  
 [b] 間隔の有効桁数が1つのフィールド (日、時、分、または秒) である場合は、SQL の期間の範囲を任意の正確な数値 (SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG、または SQL_C_NUMERIC) に変換できます。  
  
Interval SQL 型の既定の変換は、対応する C interval データ型になります。 その後、アプリケーションは列またはパラメーターをバインドし (または、適切なレコードの SQL_DESC_DATA_PTR フィールドを設定して)、初期化された SQL_INTERVAL_STRUCT 構造をポイントします (または、 **SQLGetData**の呼び出しで*targetvalueptr*引数として SQL_ INTERVAL_STRUCT 構造体へのポインターを渡します)。  
  
次の例では、DAY_TO_HOUR 間隔として返されるように、SQL_INTERVAL_DAY_TO_MINUTE 型の列から SQL_INTERVAL_STRUCT 構造体にデータを転送する方法を示します。  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
