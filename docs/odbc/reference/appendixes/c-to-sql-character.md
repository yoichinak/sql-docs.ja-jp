---
description: 'C から SQL へ: 文字'
title: 'C から SQL へ: Character |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ab8f1c0471c6e079f792aa40119f13cb31ca9ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500025"
---
# <a name="c-to-sql-character"></a>C から SQL へ: 文字
文字 ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 次の表は、C 文字データの変換先となる ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
> [!NOTE]  
>  文字 C データを Unicode SQL データに変換する場合、Unicode データの長さは偶数である必要があります。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|データのバイト長 <= 列の長さ。<br /><br /> データ > 列長のバイト長。|該当なし<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|データの文字長 <= 列の長さ。<br /><br /> データ > 列長の文字長。|該当なし<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|切り捨てなしで変換されたデータ<br /><br /> 小数部の桁の切り捨てによって変換されたデータ [e]<br /><br /> データの変換によって、(小数点ではなく) 全体が失われることがあります [e]<br /><br /> データ値が*数値リテラル*ではありません|該当なし<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|データは、数値が変換されるデータ型の範囲内にあります。<br /><br /> データが、変換されるデータ型の範囲外です<br /><br /> データ値が*数値リテラル*ではありません|該当なし<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|データは0または1です<br /><br /> データが0より大きく、2未満、1以外の値です。<br /><br /> データが0未満か、または2以上です。<br /><br /> データが*数値リテラル*ではありません|該当なし<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(データのバイト長)/2 <= 列のバイト長<br /><br /> (データのバイト長)/2 > 列バイト長<br /><br /> データ値が16進数の値ではありません|該当なし<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|データ値は有効な*ODBC 日付リテラル*です<br /><br /> データ値は有効な *ODBC タイムスタンプリテラル*です。時間部分が0です<br /><br /> データ値は有効な *ODBC タイムスタンプリテラル*です。時刻部分が0以外の場合 [a]<br /><br /> データ値は有効な*odbc 日付リテラル*または*odbc タイムスタンプリテラル*ではありません|該当なし<br /><br /> 該当なし<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|データ値は有効な*ODBC 時刻リテラル*です<br /><br /> データ値は有効な *ODBC タイムスタンプリテラル*です。秒の小数部がゼロ [b]<br /><br /> データ値は有効な *ODBC タイムスタンプリテラル*です。秒の小数部が0以外の場合 [b]<br /><br /> データ値は有効な*odbc 時刻リテラル*または*odbc タイムスタンプリテラル*ではありません|該当なし<br /><br /> 該当なし<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|データ値は有効な *ODBC タイムスタンプリテラル*です。秒の小数部が切り捨てられていません<br /><br /> データ値は有効な *ODBC タイムスタンプリテラル*です。秒の小数部の切り捨て<br /><br /> データ値は有効な *ODBC 日付リテラル*[c] です<br /><br /> データ値は有効な *ODBC 時刻リテラル*[d] です<br /><br /> データ値は有効な*odbc の日付リテラル*、 *odbc 時刻リテラル*、または*odbc タイムスタンプリテラル*ではありません|該当なし<br /><br /> 22008<br /><br /> 該当なし<br /><br /> 該当なし<br /><br /> 22018|  
|すべての SQL interval 型|データ値は有効な *間隔の値*です。切り捨ては行われません<br /><br /> データ値は有効な *間隔の値*です。いずれかのフィールドの値が切り捨てられています<br /><br /> データ値が有効な間隔リテラルではありません|該当なし<br /><br /> 22015<br /><br /> 22018|  
  
 [a] タイムスタンプの時刻部分が切り捨てられています。  
  
 [b] タイムスタンプの日付部分は無視されます。  
  
 [c] タイムスタンプの時刻部分が0に設定されています。  
  
 [d] タイムスタンプの日付部分が現在の日付に設定されています。  
  
 [e] ドライバーまたはデータソースは、変換を実行する前に、文字列全体が受信されるまで (文字データが部分的に送信される場合で **も)、効果的に待機**します。  
  
 文字 C データを数値、日付、時刻、またはタイムスタンプの SQL データに変換する場合、先頭と末尾の空白は無視されます。  
  
 文字 C データをバイナリ SQL データに変換すると、文字データの各2バイトがバイナリデータの1バイト (8 ビット) に変換されます。 文字データの各2バイトは、16進数形式の数値を表します。 たとえば、"01" はバイナリ00000001に変換され、"FF" はバイナリ11111111に変換されます。  
  
 ドライバーは、常に16進数字のペアを個々のバイトに変換し、null 終端バイトを無視します。 このため、文字列の長さが奇数の場合、文字列の最後のバイト (存在する場合は null 終端バイトを除く) は変換されません。  
  
> [!NOTE]  
>  アプリケーション開発者は、文字 C データをバイナリ SQL データ型にバインドすることをお勧めしません。 通常、この変換は効率が悪く、遅くなります。
