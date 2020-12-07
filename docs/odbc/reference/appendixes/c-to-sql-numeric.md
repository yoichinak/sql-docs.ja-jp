---
description: 'C から SQL へ: 数値'
title: 'C から SQL: Numeric |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 111d2bedf6b988255a569587fd766406b6b4176a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421516"
---
# <a name="c-to-sql-numeric"></a>C から SQL へ: 数値
数値の ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 次の表は、数値 C データの変換先となる ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|桁数 <= 列バイト長<br /><br /> 列のバイト長 > 桁数|該当なし<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|文字数 <= 列文字の長さ<br /><br /> 列文字の長さ > 文字数|該当なし<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|切り捨てなしで変換されたデータ、または小数部の桁が切り捨てられたデータ<br /><br /> 整数の切り捨てで変換されたデータ|該当なし<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|データは、数値が変換されるデータ型の範囲内にあります。<br /><br /> データが、変換されるデータ型の範囲外です|該当なし<br /><br /> 22003|  
|SQL_BIT|データは0または1です<br /><br /> データが0より大きく、2未満、1以外の値です。<br /><br /> データが0未満か、または2以上です。|該当なし<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|データが切り捨てられていません。<br /><br /> データが切り捨てられました。|該当なし<br /><br /> 22015|  
  
 [a] これらの変換は、完全な数値データ型 (SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_SSHORT、SQL_C_USHORT、SQL_C_SLONG、SQL_C_ULONG、または SQL_C_NUMERIC) に対してのみサポートされています。 概数データ型 (SQL_C_FLOAT または SQL_C_DOUBLE) ではサポートされていません。 正確な数値 C データ型は、間隔の有効桁数が1つのフィールドではない interval SQL 型に変換することはできません。  
  
 [b] "n/a" の場合、ドライバーは必要に応じて SQL_SUCCESS_WITH_INFO を返し、小数部が切り捨てられたときに01S07 を返すことができます。  
  
 数値の C データ型からデータを変換する場合、ドライバーは長さ/インジケーターの値を無視し、データバッファーのサイズが数値の C データ型のサイズであることを前提としています。 長さ/インジケーターの値は、 **Sqlputdata**の*StrLen_or_Ind*引数と、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定されたバッファーに渡されます。 データバッファーは、 **Sqlputdata**の*DataPtr*引数と**SQLBindParameter**の*parametervalueptr*引数を使用して指定します。
