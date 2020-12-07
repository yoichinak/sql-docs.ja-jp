---
description: SQL から C データ型へのデータ変換
title: SQL から C データ型へのデータ変換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c1306564a9e4a5c1cbd9cac74508529a1e6df9a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429694"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>SQL から C データ型へのデータ変換
アプリケーションが **Sqlfetch**、 **sqlfetchscroll**、または **SQLGetData**を呼び出すと、ドライバーはデータソースからデータを取得します。 必要に応じて、ドライバーがデータを取得したデータ型から、 **SQLBindCol**または SQLGetData の*TargetType*引数で指定されたデータ型にデータを変換し**ます。** 最後に、 **SQLBindCol**または**SQLGetData**の*targetvalueptr*引数によって示される場所にデータを格納します (との SQL_DESC_DATA_PTR フィールド)。  
  
 次の表は、ODBC SQL データ型から ODBC C データ型へのサポートされている変換を示しています。 塗りつぶされた円は、SQL データ型の既定の変換を示します ( *TargetType* の値が SQL_C_DEFAULT のときにデータが変換される C データ型)。 白抜きの円は、サポートされている変換を示します。  
  
 *Odbc 2.x アプリケーションで*odbc 2.x ドライバーを使用している場合、ドライバー固有のデータ型からの変換がサポートされていない可能性が*あります。*  
  
 変換されたデータの形式は、Windows®の国設定の影響を受けません。  
  
 次のセクションの表では、ドライバーまたはデータソースがデータソースから取得したデータを変換する方法について説明します。ドライバーは、サポートする ODBC SQL データ型からすべての ODBC C データ型への変換をサポートするために必要です。 特定の ODBC SQL データ型の場合、テーブルの最初の列には、 **SQLBindCol**と**SQLGetData**の*TargetType*引数の有効な入力値が一覧表示されます。 2番目の列には、多くの場合、テストの結果が一覧表示されます。 **SQLBindCol**または**SQLGetData**で指定された*bufferlength*引数を使用して、ドライバーがデータを変換できるかどうかを判断します。 3番目と4番目の列には、 **SQLBindCol**または**SQLGetData**で指定された、 *StrLen_or_IndPtr* *targetvalueptr ptr*によって指定されたバッファーに格納されている値と、ドライバーがデータを変換しようとした後の値が一覧表示されます。 ( *StrLen_or_IndPtr* 引数は、の SQL_DESC_OCTET_LENGTH_PTR のフィールドに対応します)。最後の列には、 **Sqlfetch**、 **sqlfetchscroll**、または **SQLGetData**によって結果ごとに返される SQLSTATE が一覧表示されます。  
  
 **SQLBindCol**または**SQLGetData**の*TargetType*引数に、特定の odbc SQL データ型のテーブルに示されていない odbc C データ型の識別子が含まれている場合、 **sqlfetch**、 **sqlfetchscroll**、または**SQLGetData**は SQLSTATE 07006 (制限されたデータ型の属性違反) を返します。 *TargetType*引数に、ドライバー固有の SQL データ型から ODBC C データ型への変換を指定する識別子が含まれていて、この変換がドライバーでサポートされていない場合、 **sqlfetch**、 **Sqlfetchscroll**、または**SQLGetData**は SQLSTATE HYC00 を返します (省略可能な機能は実装されていません)。  
  
 テーブルには表示されませんが、ドライバーは、SQL データ値が NULL のときに *StrLen_or_IndPtr* 引数で指定されたバッファー内の SQL_NULL_DATA を返します。 *StrLen_or_IndPtr*の使用方法の詳細については、「 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)関数の説明」を参照してください。 SQL データを文字 C データに変換する場合、StrLen_or_IndPtr で返される文字数には、 \* *StrLen_or_IndPtr* null 終了バイトは含まれません。 *Targetvalueptr*が null ポインターの場合、 **SQLGETDATA**は SQLSTATE HY009 (Null ポインターの無効な使用) を返します。**SQLBindCol**では、これによって列がバインド解除されます。  
  
 テーブルでは、次の用語と規約が使用されます。  
  
-   **データのバイト長** は、データがアプリケーションに返される前に切り捨てられるかどうかにかかわらず、**targetvalueptr*で返すことができる C データのバイト数です。 文字列データの場合は、null 終端文字のスペースは含まれません。  
  
-   **文字のバイト長** は、文字形式でデータを表示するために必要な合計バイト数です。 これは、[ [表示サイズ](../../../odbc/reference/appendixes/display-size.md)] セクションの各 C データ型に対して定義されています。ただし、文字のバイト長はバイト単位であり、表示サイズは文字単位です。  
  
-   *斜体*の単語は、関数の引数または SQL 文法の要素を表します。 文法要素の構文については、「 [付録 C: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQL から C へ: 文字](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL から C へ: 数値](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL から C へ: bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL から C へ: Binary](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL から C へ: Date](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL から C へ: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL から C へ: Time](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL から C へ: Timestamp](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL から C へ: 年月の間隔](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL から C へ: 日付と時刻の間隔](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL から C へのデータ変換の例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
