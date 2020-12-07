---
description: 文字列関数
title: 文字列関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42a5301f49a033dbc6e84a5fe43d68c794a76e84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386478"
---
# <a name="string-functions"></a>文字列関数
次の表に、文字列操作関数の一覧を示します。 アプリケーションでは、SQL_STRING_FUNCTIONS の*情報の種類*を指定して**SQLGetInfo**を呼び出すことによって、ドライバーによってサポートされる文字列関数を特定できます。  
  
## <a name="remarks"></a>解説  
 *String_exp*として示される引数には、列の名前、*文字文字列リテラル*、または別のスカラー関数の結果を指定できます。この場合、基になるデータ型を SQL_CHAR、SQL_VARCHAR、または SQL_LONGVARCHAR として表すことができます。  
  
 *Character_exp*として表される引数は可変長文字列です。  
  
 *開始*、*長さ*、または*カウント*として示される引数には、*数値リテラル*または別のスカラー関数の結果を指定できます。この場合、基になるデータ型を SQL_TINYINT、SQL_SMALLINT、または SQL_INTEGER として表すことができます。  
  
 ここに示されている文字列関数は1から始まるです。つまり、文字列の最初の文字は1文字です。  
  
 SQL-92 に合わせて、BIT_LENGTH、CHAR_LENGTH、CHARACTER_LENGTH、OCTET_LENGTH、および位置の文字列スカラー関数が ODBC 3.0 に追加されました。  
  
|機能|説明|  
|--------------|-----------------|  
|**ASCII (** _string_exp_ **)**  (ODBC 1.0)|*String_exp*の左端の文字の ASCII コード値を整数として返します。|  
|**BIT_LENGTH (** _string_exp_ **)**  (ODBC 3.0)|文字列式の長さ (ビット単位) を返します。<br /><br /> は文字列データ型に対してのみ機能しないため、 *string_exp* を文字列に暗黙的に変換するのではなく、指定されたデータ型の (内部) サイズを返します。|  
|**CHAR (** _コード_ **)**  (ODBC 1.0)|*コード*によって指定された ASCII コード値を持つ文字を返します。 *コード*の値は 0 ~ 255 の範囲で指定する必要があります。それ以外の場合、戻り値はデータソースに依存します。|  
|**CHAR_LENGTH (** _string_exp_ **)**  (ODBC 3.0)|文字列式が文字データ型の場合、文字列式の文字数を返します。それ以外の場合は、文字列式の長さをバイト単位で返します (ビット数を8で割った最小の整数)。 (この関数は CHARACTER_LENGTH 関数と同じです)。|  
|**CHARACTER_LENGTH (** _string_exp_ **)**  (ODBC 3.0)|文字列式が文字データ型の場合、文字列式の文字数を返します。それ以外の場合は、文字列式の長さをバイト単位で返します (ビット数を8で割った最小の整数)。 (この関数は CHAR_LENGTH 関数と同じです)。|  
|**CONCAT (** _string_exp1_、_string_exp2_**)**  (ODBC 1.0)|*String_exp1*に*string_exp2*を連結した結果である文字列を返します。 結果の文字列は DBMS に依存します。 たとえば、 *string_exp1* によって表される列に null 値が含まれている場合、DB2 は null を返しますが、SQL Server は null 以外の文字列を返します。|  
|**相違点 (** _string_exp1_、_string_exp2_**)**  (ODBC 2.0)|*String_exp1*と*string_exp2*に対して SOUNDEX 関数によって返された値の差を示す整数値を返します。|  
|**INSERT (** _string_exp1_、 *start*、 *length*、 _string_exp2_**)**  (ODBC 1.0)|*開始時*から、 *string_exp2*が*string_exp*に挿入された*string_exp1*から*長さ*文字が削除された文字列を返し*ます。*|  
|**LCASE (** _string_exp_ **)** (ODBC 1.0)|*String_exp*のに等しい文字列を返します。大文字はすべて小文字に変換されます。|  
|**LEFT (** _string_exp_, _count_**)** (ODBC 1.0)|*String_exp*の左端の文字*数*を返します。|  
|**長さ (** _string_exp_ **)** (ODBC 1.0)|*String_exp*内の文字数を返します。末尾の空白は除きます。<br /><br /> **長さ** は文字列のみを受け入れます。 したがって、によって *string_exp* が文字列に暗黙的に変換され、この文字列の長さ (データ型の内部サイズではない) が返されます。|  
|**検索 (** _string_exp1_、 *string_exp2*[、 *開始*]**)** (ODBC 1.0)|*String_exp2*内で最初に見つかった*string_exp1*の開始位置を返します。 最初に見つかった*string_exp1*の検索は、省略可能な引数*start*が指定されていない限り、 *string_exp2*の最初の文字位置から始まります。 *Start*を指定した場合は、 *start*の値で示される文字位置から検索が開始されます。 *String_exp2*内の最初の文字位置は、値1で示されます。 *String_exp2*内に*string_exp1*が見つからない場合は、値0が返されます。<br /><br /> アプリケーションで、 *string_exp1*、 *string_exp2*、および *開始* 引数を指定して [スカラーの検索] 関数を呼び出すことができる場合、 **SQLGetInfo** が SQL_STRING_FUNCTIONS の *オプション* で呼び出されたときに、ドライバーは SQL_FN_STR_LOCATE を返します。 アプリケーションで、 *string_exp1*引数と*string_exp2*引数だけを指定して [スカラーの検索] 関数を呼び出すことができる場合、SQL_STRING_FUNCTIONS の*オプション*を指定して**SQLGetInfo**を呼び出すと、ドライバーは SQL_FN_STR_LOCATE_2 を返します。 2つまたは3つの引数を指定した検索関数の呼び出しをサポートするドライバーは、SQL_FN_STR_LOCATE と SQL_FN_STR_LOCATE_2 の両方を返します。|  
|**LTRIM (** _string_exp_ **)** (ODBC 1.0)|先頭の空白が削除された *string_exp*の文字を返します。|  
|**OCTET_LENGTH (** _string_exp_ **)** (ODBC 3.0)|文字列式の長さ (バイト単位) を返します。 結果は、ビット数を 8 で割った値以上の最小の整数になります。<br /><br /> は文字列データ型に対してのみ機能しないため、 *string_exp* を文字列に暗黙的に変換するのではなく、指定されたデータ型の (内部) サイズを返します。|  
|**位置 (** _character_exp_**内の** _character_exp_ **)** (ODBC 3.0)|2番目の文字式の最初の文字式の位置を返します。 結果は、実装定義の有効桁数と小数点以下桁数が0の正確な数値になります。|  
|**REPEAT (** _string_exp,_ _count_**)** (ODBC 1.0)|*String_exp*繰り返し*カウント*回数で構成される文字列を返します。|  
|**REPLACE (** _string_exp1_、 *string_exp2*、 _string_exp3_**)** (ODBC 1.0)|*String_exp2*の*string_exp1*を検索し、を*string_exp3*に置き換えます。|  
|**RIGHT (** _string_exp_, _count_**)** (ODBC 1.0)|*String_exp*の右端の文字*数*を返します。|  
|**RTRIM (** _string_exp_ **)** (ODBC 1.0)|末尾の空白が削除された *string_exp* の文字を返します。|  
|**SOUNDEX (** _string_exp_ **)** (ODBC 2.0)|*String_exp*内の単語のサウンドを表すデータソースに依存する文字列を返します。 たとえば、SQL Server は4桁の SOUNDEX コードを返します。Oracle は、各単語の発音表現を返します。|  
|**SPACE (** _count_ **)** (ODBC 2.0)|*カウント*スペースで構成される文字列を返します。|  
|**SUBSTRING (** _string_exp_、 *start*、length **)** (ODBC 1.0)|*String_exp*から派生した文字列を返します。*開始*文字の先頭に指定された*文字位置*から開始されます。|  
|**UCASE (** _string_exp_ **)** (ODBC 1.0)|*String_exp*のに等しい文字列を返します。小文字はすべて大文字に変換されます。|
