---
description: 'SQL から C へ: 文字'
title: 'SQL から C へ: Character |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dff2b456e995aa344fcd928a48a5aaa09c484e89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456530"
---
# <a name="sql-to-c-character"></a>SQL から C へ: 文字

文字の ODBC SQL データ型の識別子は次のとおりです。

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

次の表は、SQL データの変換先となる ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  

|C 型識別子|テスト|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|データ < *bufferlength*のバイト長<br /><br /> データ >のバイト長 = *Bufferlength*|データ<br /><br /> 切り捨てられたデータ|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)|該当なし<br /><br /> 01004|  
|SQL_C_WCHAR|データ < *bufferlength*の文字長<br /><br /> データ >の文字長 = *Bufferlength*|データ<br /><br /> 切り捨てられたデータ|データの長さ (文字数)<br /><br /> データの長さ (文字数)|該当なし<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|切り捨てなしで変換されたデータ [b]<br /><br /> 小数部の桁の切り捨てで変換されたデータ [a]<br /><br /> データを変換すると、(小数点ではなく) 全体が失われることになります。<br /><br /> データが *数値リテラル*ではない [b]|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。<br /><br /> 未定義。|C データ型のバイト数<br /><br /> C データ型のバイト数<br /><br /> 未定義。<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|データは、数値が変換されるデータ型の範囲内にある [a]<br /><br /> データが、数値を変換するデータ型の範囲外です [a]<br /><br /> データが *数値リテラル*ではない [b]|データ<br /><br /> 未定義。<br /><br /> 未定義。|C データ型のサイズ<br /><br /> 未定義。<br /><br /> 未定義。|該当なし<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|データは0または1です<br /><br /> データが0より大きく、2未満、1以外の値です。<br /><br /> データが0未満か、または2以上です。<br /><br /> データが*数値リテラル*ではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。<br /><br /> 未定義。|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義。<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 切り捨てられたデータ|データの長さ (バイト単位)<br /><br /> データの長さ|該当なし<br /><br /> 01004|  
|SQL_C_TYPE_DATE|データ値は有効な *日付値*です [a]<br /><br /> データ値は有効な *タイムスタンプ値*です。時間部分がゼロ [a]<br /><br /> データ値は有効な *タイムスタンプ値*です。時刻部分が0以外の場合 [a]、[c]<br /><br /> データ値が有効な *日付値* または *タイムスタンプ値*ではありません [a]|データ<br /><br /> データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定義。|該当なし<br /><br /> 該当なし<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|データ値は有効な *時刻値で、秒の小数部の値は 0*[a] です<br /><br /> データ値は有効な *タイムスタンプ値または有効な時刻値*です。秒の小数部がゼロ [a]、[d]<br /><br /> データ値は有効な *タイムスタンプ値*です。秒の小数部はゼロ以外 [a]、[d]、[e]<br /><br /> データ値が有効な *時刻値* または *タイムスタンプ値*ではありません [a]|データ<br /><br /> データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定義。|該当なし<br /><br /> 該当なし<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|データ値は有効な *タイムスタンプ値または有効な時刻値*です。秒の小数部が切り捨てられない [a]<br /><br /> データ値は有効な *タイムスタンプ値または有効な時刻値*です。秒の小数部が切り捨てられました [a]<br /><br /> データ値は有効な *日付値*です [a]<br /><br /> データ値は有効な *時刻値*[a] です<br /><br /> データ値が有効な *日付値*、 *時刻値*、または *タイムスタンプ値*[a] ではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> データ [f]<br /><br /> データ [g]<br /><br /> 未定義。|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 該当なし<br /><br /> 該当なし<br /><br /> 22018|  
|すべての C 間隔の種類|データ値は有効な *間隔の値*です。切り捨てなし<br /><br /> データ値は有効な *間隔の値*です。1つまたは複数の末尾のフィールドの切り捨て<br /><br /> データは有効な間隔です。先頭のフィールドの有意精度が失われる<br /><br /> データ値が有効な間隔の値ではありません|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。<br /><br /> 未定義。|該当なし<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [b] これは、対応する C データ型のサイズです。  
  
 [c] *タイムスタンプ値* の時刻部分が切り捨てられています。  
  
 [d] *タイムスタンプ値* の日付部分は無視されます。  
  
 [e] タイムスタンプの秒部分の小数部は切り捨てられます。  
  
 [f] タイムスタンプ構造の時刻フィールドが0に設定されています。  
  
 [g] タイムスタンプ構造の日付フィールドが現在の日付に設定されています。  

**余分なスペース**

SQL 文字データが次のいずれかの型に変換される場合、先頭と末尾のスペースは無視されます。

- date
- numeric
- time
- timestamp
- 間隔 C データ
