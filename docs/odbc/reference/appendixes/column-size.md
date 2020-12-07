---
description: 列サイズ
title: 列サイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53d7934f3ac4669545e3cc24752e4a9e0f4fb589
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411118"
---
# <a name="column-size"></a>列サイズ
数値データ型の列 (またはパラメーター) のサイズは、列またはパラメーターのデータ型、またはデータの有効桁数によって使用される最大桁数として定義されます。 文字型の場合は、データの長さを文字数で示します。バイナリデータ型の場合、列のサイズはデータの長さ (バイト単位) として定義されます。 Time、timestamp、および all interval データ型の場合、このデータの文字表現に含まれる文字数です。 次の表に、各簡潔な SQL データ型に対して定義されている列サイズを示します。  
  
|SQL 型識別子|列のサイズ|  
|-------------------------|-----------------|  
|すべての文字型 [a]、[b]|列またはパラメーターの文字数で定義された、または最大の列サイズ (SQL_DESC_LENGTH 記述子フィールドに含まれる)。 たとえば、CHAR (10) として定義された1バイト文字の列の列サイズは10です。|  
|SQL_DECIMAL SQL_NUMERIC|定義されている桁数。 たとえば、NUMERIC (10, 3) として定義された列の有効桁数は10です。|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 (署名されている場合) または 20 (符号なしの場合)|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|すべてのバイナリ型 [a]、[b]|列またはパラメーターの定義済みまたは最大長 (バイト単位)。 たとえば、BINARY (10) として定義されている列の長さは10です。|  
|SQL_TYPE_DATE [c]|10 ( *yyyy-mm-dd* 形式の文字数)。|  
|SQL_TYPE_TIME [c]|8 ( *hh-mm-ss* 形式の文字数)、または 9 + *s* ( *hh: mm: ss*[...] 形式の文字数)。 *s* は秒の有効桁数です。|  
|SQL_TYPE_TIMESTAMP|16 ( *yyyy-mm-dd hh: mm* 形式の文字数)<br /><br /> 19 ( *yyyy-mm-dd* *hh: mm: ss* 形式の文字数)<br /><br /> or<br /><br /> 20 + *s* ( *yyyy-mm-dd hh: mm: ss*[...] 形式の文字数)。 *s* は秒の有効桁数です。|  
|SQL_INTERVAL_SECOND|ここで、 *p*は間隔の先頭の有効桁数、 *s*は秒の有効*桁数、s*は*s*= 0、 *p* + *s*+ 1 ( *s*>0 の場合) です。 [a|  
|SQL_INTERVAL_DAY_TO_SECOND|ここで、 *p*は間隔の先頭の有効桁数で、 *s*は秒の有効*桁数 (s* = 0 の場合) または 10 +*p* *s* + *s* ( *s*>0 の場合) です。 [a|  
|SQL_INTERVAL_HOUR_TO_SECOND|ここで、 *p*は間隔の先頭の有効桁数で、 *s*は秒の有効桁数、は 6 +*p* ( *s*= 0 の場合) または 7 +*p* + *s* ( *s*>0 の場合) です。 [a|  
|SQL_INTERVAL_MINUTE_TO_SECOND|ここで、 *p*は間隔の先頭の有効桁数で、 *s*は秒の有効桁数、3 +*p* ( *s*= 0 の場合) または 4 +*p* + *s* ( *s*>0 の場合) です。 [a|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*。ここで、 *p* は間隔の先頭の有効桁数です。a|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*( *p* は間隔の先頭の有効桁数)。a|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*。ここで、 *p* は間隔の有効桁数です。a|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*( *p* は間隔の先頭の有効桁数)。a|  
|SQL_GUID|36 ( *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 形式の文字数)|  
  
 odbc 2.0 ドライバーで**SQLSetParam**を呼び出す odbc 1.0 アプリケーションの場合、および odbc 1.0 ドライバーで**SQLBINDPARAMETER**を呼び出す odbc 2.0 アプリケーションの場合、 \* SQL_LONGVARCHAR または SQL_LONGVARBINARY の種類に対して*StrLen_or_IndPtr*が SQL_DATA_AT_EXEC 場合は、この表で定義されている有効桁数ではなく、送信されるデータの合計の長さに*columnsize*を設定する必要があります。  
  
 [b] 変数型の列またはパラメーターの長さをドライバーが判別できない場合は、SQL_NO_TOTAL を返します。  
  
 [c] **SQLBindParameter**の*Columnsize*引数は、このデータ型では無視されます。  
  
 [d] interval データ型の列の長さに関する一般的な規則については、この付録の「 [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)」を参照してください。  
  
 列 (またはパラメーター) のサイズに対して返される値は、1つの記述子フィールドの値に対応していません。 値は、次の表に示すように、データの種類に応じて、SQL_DESC_PRECISION または SQL_DESC_LENGTH のいずれかのフィールドから取得できます。  
  
|SQL 型|に対応する記述子フィールド<br /><br /> 列またはパラメーターのサイズ|  
|--------------|--------------------------------------------------------------------|  
|すべての文字型とバイナリ型|LENGTH|  
|すべての数値型|PRECISION|  
|すべての datetime 型と interval 型|LENGTH|  
|SQL_BIT|LENGTH|
