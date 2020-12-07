---
description: 'SQL から C へ: 年月の間隔'
title: 'SQL から C: 年月間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 66134ca1dcd82fec5213f01ef33a1b5f050e8a8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429534"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL から C へ: 年月の間隔

年月間隔の ODBC SQL データ型の識別子は次のとおりです。

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

次の表は、SQL データが変換される月の日付を表す ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  

|C 型識別子|テスト|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|末尾のフィールド部分が切り捨てられていません<br /><br /> 末尾のフィールドの一部が切り捨てられました<br /><br /> ターゲットの先頭の有効桁数が、ソースからのデータを保持するのに十分な大きさではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|間隔の有効桁数が1つのフィールドであり、切り捨てずにデータが変換されました<br /><br /> 間隔の精度は1つのフィールドで、全体が切り捨てられました<br /><br /> 間隔の有効桁数が1つのフィールドではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> データの長さ (バイト単位)<br /><br /> C データ型のサイズ|該当なし<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_CHAR|文字のバイト長 < *Bufferlength*<br /><br /> *Bufferlength* < 整数 (小数部ではなく) の数字<br /><br /> 整数の桁数 (小数部ではなく) >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|文字の長さ < *Bufferlength*<br /><br /> *Bufferlength* < 整数 (小数部ではなく) の数字<br /><br /> 整数の桁数 (小数部ではなく) >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 年月間隔の SQL 型は、任意の年の月の C 型に変換できます。  
  
 [b] 間隔の有効桁数が1つのフィールド (年または月の1つ) の場合、interval SQL 型は任意の正確な数値 (SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG、または SQL_C_NUMERIC) に変換できます。  

## <a name="default-conversions"></a>既定の変換

Interval SQL 型の既定の変換は、対応する C interval データ型になります。 その後、アプリケーションは列またはパラメーターをバインドし (または、適切なレコードの SQL_DESC_DATA_PTR フィールドを設定して)、初期化された SQL_INTERVAL_STRUCT 構造をポイントします (または、 **SQLGetData**の呼び出しで*targetvalueptr*引数として SQL_ INTERVAL_STRUCT 構造体へのポインターを渡します)。
