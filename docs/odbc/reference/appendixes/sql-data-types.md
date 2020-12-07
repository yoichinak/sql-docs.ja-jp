---
description: SQL データ型
title: SQL データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209463c3c316a5bd2e45a2d7b08eb65b3cb113d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483155"
---
# <a name="sql-data-types"></a>SQL データ型
各 DBMS は、独自の SQL 型を定義します。 各 ODBC ドライバーは、関連付けられている DBMS が定義する SQL データ型のみを公開します。 ドライバーが DBMS SQL 型を ODBC 定義の SQL 型識別子にマップする方法と、ドライバーが DBMS SQL 型を独自のドライバー固有の SQL 型識別子にマップする方法については、 **SQLGetTypeInfo**を呼び出すことによって返されます。 また、ドライバーは、 **Sqlcolattribute**、 **sqlcolumns**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **SQLProcedureColumns**、および **sql 列**の呼び出しを通じて、列およびパラメーターのデータ型を記述するときに、SQL データ型を返します。  
  
> [!NOTE]  
>  SQL データ型は、実装記述子の SQL_DESC_ CONCISE_TYPE、SQL_DESC_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE の各フィールドに含まれています。 SQL データ型の特性は、実装記述子の SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、および SQL_DESC_OCTET_LENGTH の各フィールドに含まれています。 詳細については、この付録の「 [データ型の識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 」を参照してください。  
  
 特定のドライバーとデータソースは、必ずしもこの付録で定義されているすべての SQL データ型をサポートしているわけではありません。 ドライバーが SQL データ型をサポートするかどうかは、ドライバーが準拠している SQL-92 のレベルによって異なります。 アプリケーションでは、ドライバーでサポートされている SQL 92 文法のレベルを確認するために、SQL_SQL_CONFORMANCE 情報の種類を使用して **SQLGetInfo** を呼び出します。 また、特定のドライバーとデータソースでは、ドライバー固有のその他の SQL データ型をサポートする場合もあります。 ドライバーがサポートしているデータ型を確認するために、アプリケーションは **SQLGetTypeInfo**を呼び出します。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。 特定のデータソースのデータ型の詳細については、そのデータソースのドキュメントを参照してください。  
  
> [!IMPORTANT]  
>  この付録の表は単なるガイドラインであり、一般的に使用される SQL データ型の名前、範囲、および制限を示しています。 特定のデータソースでサポートされているデータ型の一部だけがサポートされている場合があります。また、サポートされるデータ型の特性は、記載されているものとは異なる場合があります。  
  
 次の表に、すべての SQL データ型の有効な SQL 型識別子を示します。 また、SQL-92 (存在する場合) の対応するデータ型の名前と説明も表示されます。  
  
|SQL 型識別子 [1]|標準的な SQL データ<br /><br /> 種類 [2]|一般的な型の説明|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|*固定長文字列の文字列。*|  
|SQL_VARCHAR|VARCHAR (*n*)|最大文字列長 *n*の可変長文字列。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可変長文字データ。 最大長は、データソースに依存します。ませ|  
|SQL_WCHAR|WCHAR (*n*)|固定長文字列の Unicode 文字列の長さ *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|最大文字列長を持つ Unicode 可変長文字列 *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode 可変長文字データ。 最大長はデータソースに依存します|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|少なくとも *p* と scale s の有効桁数を持つ符号付きの正確な数値 *。* (最大有効桁数はドライバーで定義されています)。(1 <= *p* <= 15;*s*  <= *p*)。4/4|  
|SQL_NUMERIC|NUMERIC (*p*,*s*)|精度が*p*で小数点以下桁数が*s*の符号付きの正確な数値 (1 <= *p* <= 15;*s*  <= *p*)。4/4|  
|SQL_SMALLINT|SMALLINT|精度が5および小数点以下桁数が0の numeric 値 (符号付き:-32768 <= *n* <= 32767、unsigned: 0 <= *n* <= 65535) [3]。|  
|SQL_INTEGER|INTEGER|有効桁数が10および小数点以下桁数が0の正確な数値 (符号付き:-2 [31] <= *n* <= 2 [31]-1、符号なし: 0 <= *n* <= 2 [32]-1) [3]。|  
|SQL_REAL|real|バイナリ精度 24 (0 または絶対値が 10 [-38] ~ 10 [38]) の符号付き概数値。|  
|SQL_FLOAT|FLOAT (*p*)|少なくとも *p*のバイナリ有効桁数を持つ、符号付きの概数型の数値。 (最大有効桁数はドライバーで定義されています)。5/5|  
|SQL_DOUBLE|DOUBLE PRECISION|バイナリ精度 53 (0 または絶対値が 10 [-308] ~ 10 [308]) の符号付き概数。数値。|  
|SQL_BIT|BIT|1ビットのバイナリデータ。8|  
|SQL_TINYINT|TINYINT|精度3および小数点以下桁数が0の正確な数値 (符号付き:-128 <= *n* <= 127、符号なし: 0 <= *n* <= 255) [3]。|  
|SQL_BIGINT|bigint|精度が 19 (符号付きの場合) または 20 (符号なしの場合) および小数点以下桁数 0 (符号付きの場合) およびスケール 0 (符号付き:-2 [63] <= *n* <= 2 [63]-1、符号なし: 0 <= *n* <= 2 [64]-1) [3]、[9]|  
|SQL_BINARY|バイナリ (*n*)|固定長 *n*のバイナリデータ。ませ|  
|SQL_VARBINARY|VARBINARY (*n*)|最大長 *n*の可変長バイナリデータ。 最大値は、ユーザーによって設定されます。ませ|  
|SQL_LONGVARBINARY|LONG VARBINARY|可変長バイナリ データ。 最大長は、データソースに依存します。ませ|  
|SQL_TYPE_DATE [6]|DATE|グレゴリオ暦の規則に準拠した年、月、日の各フィールド。 (この付録の後半の「 [グレゴリオ暦の制約](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)」を参照してください)。|  
|SQL_TYPE_TIME [6]|時間 (*p*)|時間、分、および秒のフィールド。有効な値は 00 ~ 23 の時間、00 ~ 59 の有効な値、および 00 ~ 61 の秒の有効な値です。 有効桁数 *p* 秒の有効桁数を示します。|  
|SQL_TYPE_TIMESTAMP [6]|タイムスタンプ (*p*)|日付と時刻のデータ型に対して定義されている有効な値を持つ、年、月、日、時、分、および秒の各フィールド。|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|Year、month、day、hour、minute、second、utchour、utcminute の各フィールド。 Utchour フィールドと utcminute フィールドの精度は1/10 マイクロ秒です。|  
|SQL_TYPE_UTCTIME|UTCTIME|Hour、minute、second、utchour、utcminute の各フィールド。 Utchour フィールドと utcminute フィールドの精度は1/10 マイクロ秒です。|  
|SQL_INTERVAL_MONTH [7]|間隔月 (*p*)|2つの日付の間の月数。 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_YEAR [7]|間隔の年 (*p*)|2つの日付間の年数 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|間隔の年 (*p*) から月|2つの日付間の年と月の数。 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_DAY [7]|間隔の日 (*p*)|2つの日付の間の日数 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_HOUR [7]|間隔 (時間) (*p*)|2つの日付/時刻の間の時間数。 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_MINUTE [7]|間隔 (分) (*p*)|2つの日付/時刻の間の分数 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_SECOND [7]|INTERVAL 秒 (*p*,*q*)|2つの日付/時刻の間の秒数。 *p* は間隔の先頭の有効桁数で、 *q* は間隔の秒の有効桁数です。|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|間隔の日 (*p*) から時間|2つの日付/時刻の間の日数/時間。 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|間隔の日 (*p*) から分|2つの日付/時刻の間の日数/時間/分 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|間隔の日 (*p*) から秒 (*q*)|2つの日付/時刻の間の日数/時間/分/秒 *p* は間隔の先頭の有効桁数で、 *q* は間隔の秒の有効桁数です。|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|INTERVAL 時間 (*p*) から分|2つの日付/時刻の間の時間数/分 *p* は、間隔の有効桁数です。|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|INTERVAL 時間 (*p*) から秒 (*q*)|2つの日付/時刻の間の時間数/分/秒。 *p* は間隔の先頭の有効桁数で、 *q* は間隔の秒の有効桁数です。|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|間隔 (分) (*p*) から秒 (*q*)|2つの日付/時刻の間の分数 (秒単位)。 *p* は間隔の先頭の有効桁数で、 *q* は間隔の秒の有効桁数です。|  
|SQL_GUID|GUID|固定長 GUID。|  
  
 [1] **SQLGetTypeInfo**を呼び出すことによって DATA_TYPE 列に返される値です。  
  
 [2] **SQLGetTypeInfo**を呼び出すことによって、NAME および CREATE PARAMS 列に返される値です。 NAME 列は指定値を返します。たとえば、CHAR-の場合、CREATE PARAMS 列は、有効桁数、小数点以下桁数、長さなど、作成パラメーターのコンマ区切りのリストを返します。  
  
 [3] アプリケーションでは、 **SQLGetTypeInfo** または **sqlcolattribute** を使用して、特定のデータ型または結果セット内の特定の列が符号なしであるかどうかを判断します。  
  
 [4] SQL_DECIMAL および SQL_NUMERIC のデータ型の精度は異なります。 DECIMAL (*p*,*s*) の有効桁数は、実装で定義された10進数の有効桁数で、 *p*未満ではなく、数値 (*p*,*s*) の有効桁数は *p*と完全に一致します。  
  
 [5] 実装によっては、SQL_FLOAT の有効桁数は24または53のいずれかになります。24の場合、SQL_FLOAT データ型は SQL_REAL と同じになります。53の場合、SQL_FLOAT のデータ型は SQL_DOUBLE と同じになります。  
  
 [6] ODBC 3.x では、SQL date、time、および timestamp の各データ型はそれぞれ SQL_TYPE_DATE、SQL_TYPE_TIME、および SQL_TYPE_TIMESTAMP に*なります。**ODBC 2.x では、データ*型は SQL_DATE、SQL_TIME、および SQL_TIMESTAMP です。  
  
 [7] interval SQL データ型の詳細については、この付録の後半の「 [Interval データ型](../../../odbc/reference/appendixes/interval-data-types.md) 」を参照してください。  
  
 [8] SQL_BIT データ型は、SQL-92 のビット型とは異なる特性を持っています。  
  
 [9] このデータ型には、SQL-92 に対応するデータ型がありません。  
  
 ここでは、次の例について説明します。  
  
-   [SQLGetTypeInfo 結果セットの例](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
