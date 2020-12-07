---
description: 日付、時刻、およびタイムスタンプのリテラル
title: 日付、時刻、およびタイムスタンプのリテラル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10fb362a8ab61595a9b7205492de9c1115ae7013
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424784"
---
# <a name="date-time-and-timestamp-literals"></a>日付、時刻、およびタイムスタンプのリテラル
日付、時刻、およびタイムスタンプリテラルのエスケープシーケンスは、  
  
 **{**  _-型_ **'** _value_ **'}**  
  
 ここで、 *リテラル型* は次の表に示すいずれかの値です。  
  
|*リテラル-型*|説明|*値*の形式|  
|---------------------|-------------|-----------------------|  
|**d**|Date|*yyyy* -*mm* -*dd*|  
|**\t**|ごと|*hh*:*mm*:*ss*[1]|  
|**鏡**|Timestamp|*yyyy* -*mm* -*dd* *hh*:*mm*:*ss*[.*f...*]1|  
  
 [1] 秒の部分を含む時間またはタイムスタンプの間隔リテラルの小数点の右側の桁数は、SQL_DESC_PRECISION 記述子フィールドに含まれる秒の有効桁数に依存します。 (詳細については、「 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」を参照してください)。  
  
 日付、時刻、およびタイムスタンプエスケープシーケンスの詳細については、「付録 C: SQL 文法」の「 [日付、時刻、およびタイムスタンプエスケープシーケンス](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) 」を参照してください。  
  
 たとえば、次の SQL ステートメントはどちらも、Orders テーブルの sales order 1023 の open date を更新します。 最初のステートメントでは、エスケープシーケンス構文を使用します。 2番目のステートメントでは、DATE 列に対して Oracle Rdb ネイティブ構文を使用し、相互運用できません。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日付、時刻、またはタイムスタンプリテラルのエスケープシーケンスは、日付、時刻、またはタイムスタンプパラメーターにバインドされた文字変数に配置することもできます。 たとえば、次のコードでは、文字変数にバインドされた日付パラメーターを使用して、Orders テーブルの sales order 1023 の open date を更新しています。  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 ただし、通常は、パラメーターを日付構造体に直接バインドする方が効率的です。  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 ドライバーで日付、時刻、またはタイムスタンプのリテラルの ODBC エスケープシーケンスがサポートされているかどうかを判断するために、アプリケーションは **SQLGetTypeInfo**を呼び出します。 データソースが日付、時刻、またはタイムスタンプデータ型をサポートしている場合は、対応するエスケープシーケンスもサポートする必要があります。  
  
 データソースは、ANSI SQL-92 仕様で定義されている datetime リテラルをサポートすることもできます。これは、日付、時刻、またはタイムスタンプリテラルの ODBC エスケープシーケンスとは異なります。 データソースが ANSI リテラルをサポートしているかどうかを判断するために、アプリケーションは SQL_ANSI_SQL_DATETIME_LITERALS オプションを指定して **SQLGetInfo** を呼び出します。  
  
 ドライバーが interval リテラルの ODBC エスケープシーケンスをサポートするかどうかを判断するために、アプリケーションは **SQLGetTypeInfo**を呼び出します。 データソースが datetime interval データ型をサポートしている場合は、対応するエスケープシーケンスもサポートする必要があります。  
  
 データソースは、ANSI SQL-92 仕様で定義されている datetime リテラルをサポートすることもできます。これは、datetime interval リテラルの ODBC エスケープシーケンスとは異なります。 データソースが ANSI リテラルをサポートしているかどうかを判断するために、アプリケーションは SQL_ANSI_SQL_DATETIME_LITERALS オプションを指定して **SQLGetInfo** を呼び出します。
