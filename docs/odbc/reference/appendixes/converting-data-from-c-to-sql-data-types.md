---
description: C から SQL データ型へのデータ変換
title: データを C から SQL データ型に変換する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56af1e376edffa0268a2e27c840f035e5cda9763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429714"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>C から SQL データ型へのデータ変換
アプリケーションが **Sqlexecute** または **SQLExecDirect**を呼び出すと、ドライバーは、アプリケーションのストレージの場所から **SQLBindParameter** にバインドされているすべてのパラメーターのデータを取得します。 アプリケーションが **SQLSetPos**を呼び出すと、ドライバーは、 **SQLBindCol**にバインドされた列から更新操作または追加操作のデータを取得します。 実行時データパラメーターの場合、アプリケーションは **Sqlputdata**を使用してパラメーターデータを送信します。 必要に応じて、ドライバーは、 **SQLBindParameter**の*ValueType*引数で指定されたデータ型から、 **SQLBindParameter**の*ParameterType*引数で指定されたデータ型にデータを変換し、データをデータソースに送信します。  
  
 次の表は、ODBC C データ型から ODBC SQL データ型へのサポートされている変換を示しています。 塗りつぶされた円は、SQL データ型の既定の変換を示します ( *ValueType* の値または SQL_DESC_CONCISE_TYPE 記述子フィールドが SQL_C_DEFAULT の場合、データの変換元となる C データ型)。 白抜きの円は、サポートされている変換を示します。  
  
 変換されたデータの形式は、Windows®の国設定の影響を受けません。  
  
 ![サポートされる ODBC C から SQL へのデータ型の変換](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 次のセクションの表では、ドライバーまたはデータソースがデータソースに送信されるデータを変換する方法について説明します。ドライバーは、すべての ODBC C データ型から、サポートする ODBC SQL データ型への変換をサポートするために必要です。 特定の ODBC C データ型の場合、テーブルの最初の列には、 **SQLBindParameter**の*ParameterType*引数の有効な入力値が一覧表示されます。 2番目の列には、データを変換できるかどうかを判断するためにドライバーが実行するテストの結果が一覧表示されます。 3番目の列には、 **SQLExecDirect**、 **sqlexecute**、 **sqlbulkoperations**、 **SQLSetPos**、または **sqlputdata**によって結果ごとに返される SQLSTATE が一覧表示されます。 SQL_SUCCESS が返された場合にのみ、データがデータソースに送信されます。  
  
 **SQLBindParameter**の*ParameterType*引数に、特定の C データ型の表に示されていない ODBC SQL データ型の識別子が含まれている場合、 **SQLBindParameter**は SQLSTATE 07006 (制限されたデータ型の属性違反) を返します。 *ParameterType*引数にドライバー固有の識別子が含まれていて、ドライバーが特定の ODBC C データ型からそのドライバー固有の SQL データ型への変換をサポートしていない場合、 **SQLBINDPARAMETER**は SQLSTATE HYC00 を返します (省略可能な機能は実装されていません)。  
  
 **SQLBindParameter**で指定された*parametervalueptr*引数と*StrLen_or_IndPtr*引数が両方とも null ポインターの場合、その関数は SQLSTATE HY009 (null ポインターの無効な使用) を返します。 テーブルには表示されませんが、アプリケーションは、 **SQLBindParameter**の*StrLen_or_IndPtr*引数によって示される長さ/インジケーターバッファーの値、または**sqlputdata**の*StrLen_or_IndPtr*引数の値を SQL_NULL_DATA に設定して、NULL の SQL データ値を指定します。 ( *StrLen_or_IndPtr*引数は、APD の SQL_DESC_OCTET_LENGTH_PTR フィールドに対応します)。アプリケーションはこれらの値を SQL_NTS に設定して、 \* Sqlputdata の*parametervalueptr*の値**SQLBindParameter** \* *DataPtr* (APD の SQL_DESC_DATA_PTR フィールドが指す) の値が null で終わる文字列**SQLPutData**であることを指定します。  
  
 テーブルでは、次の用語が使用されます。  
  
-   **データのバイト長** -データがデータソースに送信される前にデータが切り捨てられるかどうかにかかわらず、データソースに送信できる SQL データのバイト数。 文字列データの場合、これには null 終端文字のスペースは含まれません。  
  
-   **列バイト長** -データソースにデータを格納するために必要なバイト数。  
  
-   **文字バイト長** -文字形式でデータを表示するために必要な最大バイト数。 これは、 [表示サイズ](../../../odbc/reference/appendixes/display-size.md)における各 SQL データ型に対して定義されているとおりです。ただし、文字のバイト長はバイト単位ですが、表示サイズは文字単位です。  
  
-   **数字の数** -マイナス記号、小数点、および指数 (必要な場合) を含む、数値を表すために使用される文字数。  
  
-   **単語**   
     ***斜体***  -SQL 文法の要素。 文法要素の構文については、「 [付録 C: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [C から SQL へ: 文字](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C から SQL へ: 数値](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C から SQL へ: bit](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C から SQL へ: Binary](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C から SQL へ: Date](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C から SQL へ: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C から SQL へ: Time](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C から SQL へ: Timestamp](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C から SQL へ: 年月の間隔](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C から SQL へ: 日付と時刻の間隔](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [C から SQL へのデータ変換の例](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
