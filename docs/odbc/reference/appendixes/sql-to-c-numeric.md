---
description: 'SQL から C へ: 数値'
title: 'SQL から C へ: Numeric |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d48706eddabc71f28c84fae5623a8c9e440d8506
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429564"
---
# <a name="sql-to-c-numeric"></a>SQL から C へ: 数値

数値の ODBC SQL データ型の識別子は次のとおりです。

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

次の表は、数値の SQL データの変換先となる ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  

|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|文字のバイト長 < *Bufferlength*<br /><br /> *Bufferlength* < 整数 (小数部ではなく) の数字<br /><br /> 整数の桁数 (小数部ではなく) >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|文字の長さ < *Bufferlength*<br /><br /> *Bufferlength* < 整数 (小数部ではなく) の数字<br /><br /> 整数の桁数 (小数部ではなく) >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの長さ (文字数)<br /><br /> データの長さ (文字数)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|切り捨てなしで変換されたデータ [a]<br /><br /> 小数部の桁の切り捨てで変換されたデータ [a]<br /><br /> データを変換すると、(小数点ではなく) 全体が失われることになります。|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|データは、数値が変換されるデータ型の範囲内にある [a]<br /><br /> データが、数値を変換するデータ型の範囲外です [a]|データ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_BIT|データが0または 1 [a]<br /><br /> データが0より大きく2未満で、1以外の値が指定されています [a]<br /><br /> データが0より小さいか、または2以上です [a]|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 未定義。|データの長さ<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] SQL_C_INTERVAL_DAY [c] SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|切り捨てられていないデータ<br /><br /> 秒の小数部の切り捨て<br /><br /> 切り捨てられた数値の部分全体|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|切り捨てられた数値の部分全体|未定義。|未定義。|22015|  
  
 [a] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [b] これは、対応する C データ型のサイズです。  
  
 [c] この変換は、正確な数値データ型 (SQL_DECIMAL、SQL_NUMERIC、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、および SQL_BIGINT) に対してのみサポートされています。 概数データ型 (SQL_REAL、SQL_FLOAT、または SQL_DOUBLE) ではサポートされていません。  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC と SQLSetDescField

 SQL_C_NUMERIC 値を使用して手動バインドを実行するには、 [SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md) が必要です。 (SQLSetDescField は ODBC 3.0 で追加されたことに注意してください)。手動バインドを実行するには、最初に記述子ハンドルを取得する必要があります。  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
