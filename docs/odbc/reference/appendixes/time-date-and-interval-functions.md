---
description: 時刻、日付、および間隔を扱う関数
title: Time、Date、および Interval 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dcbdf9f40a9cd1f1296920e3d2ea71fcb5ce6b39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386378"
---
# <a name="time-date-and-interval-functions"></a>時刻、日付、および間隔を扱う関数
次の表は、ODBC スカラー関数セットに含まれている日付と時刻の関数を示しています。 アプリケーションでは、SQL_TIMEDATE_FUNCTIONS の*情報の種類*を指定して**SQLGetInfo**を呼び出すことによって、ドライバーによってサポートされる時刻と日付の関数を特定できます。  
  
 *Timestamp_exp*として指定される引数には、列の名前、別のスカラー関数の結果、または*odbc-time escape*、odbc *-date-escape*、または odbc- *timestamp-escape*があります。この場合、基になるデータ型を SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、SQL_TYPE_DATE、または SQL_TYPE_TIMESTAMP として表すことができます。  
  
 *Date_exp*として示される引数には、列の名前、別のスカラー関数の結果、または、基になるデータ型を SQL_CHAR、SQL_VARCHAR、SQL_TYPE_DATE、または SQL_TYPE_TIMESTAMP として表すことができる、 *odbc の日付*と*時刻*のデータ型を使用できます。  
  
 *Time_exp*として示される引数には、列の名前、別のスカラー関数の結果、または、基になるデータ型を SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、または SQL_TYPE_TIMESTAMP として表すことができる、 *odbc タイム*スタンプまたは*odbc タイムスタンプエスケープ*を使用できます。  
  
 SQL-92 に合わせて、CURRENT_DATE、CURRENT_TIME、および CURRENT_TIMESTAMP timedate スカラー関数が ODBC 3.0 に追加されました。  
  
|機能|説明|  
|--------------|-----------------|  
|**CURRENT_DATE ()** (ODBC 3.0)|現在の日付を返します。|  
|**CURRENT_TIME [(** *時間精度* **)]** (ODBC 3.0)|現在のローカル時間を返します。 *時間精度*引数は、返される値の秒の有効桁数を決定します。|  
|**CURRENT_TIMESTAMP**<br /> **[(** *タイムスタンプ-有効桁数* **)]** (ODBC 3.0)|現在の現地日時をタイムスタンプ値として返します。 *タイムスタンプ精度*引数は、返されるタイムスタンプの秒の有効桁数を決定します。|  
|**Curdate ()** (ODBC 1.0)|現在の日付を返します。|  
|**Curtime ()** (ODBC 1.0)|現在のローカル時間を返します。|  
|**Dayname (** *date_exp* **)** (ODBC 2.0)|日付のデータソース固有の名前 (たとえば、日曜日 ~ 土曜日または太陽) を含む文字列を返します。 - Sat. 英語を使用するデータソース、または *date_exp*の日部分にドイツ語を使用するデータソースの Sonntag から使った)。|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の月のフィールドに基づいて、1-31 の範囲の整数値として、月の日付を返します。|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の週のフィールドに基づいて、1-7 の範囲の整数値として曜日を返します。1は日曜日を表します。|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の年のフィールドに基づいて、1-366 の範囲の整数値として、年の通算日を返します。|  
|抽出 **(** 抽出*元**からフィールドを*抽出 **)** (ODBC 3.0)|*抽出ソース*の*抽出フィールド*部分を返します。 *抽出元*の引数は datetime または interval 式です。 *抽出フィールド*引数には、次のいずれかのキーワードを指定できます。<br /><br /> 年月の1分の1秒<br /><br /> 戻り値の有効桁数は、実装によって定義されます。 小数点以下桁数は0以外の小数点以下桁数が0の場合、小数点以下桁数は、 *抽出元* のフィールドの秒の小数部の有効桁数よりも小さくはありません。|  
|**HOUR (** *time_exp* **)** (ODBC 1.0)|*Time_exp*の時間フィールドに基づいて、0-23 の範囲の整数値として時間を返します。|  
|**MINUTE (** *time_exp* **)** (ODBC 1.0)|*Time_exp*の分のフィールドに基づいて、0-59 の範囲の整数値として分を返します。|  
|**MONTH (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の月のフィールドに基づいて、1-12 の範囲の整数値として月を返します。|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|月のデータソース固有の名前を含む文字列を返します (たとえば、Januar *date_exp*の月部分に英語を使用するデータソース、またはドイツ語を使用しているデータソースに対して使ったから12月まで)。|  
|**NOW ()** (ODBC 1.0)|現在の日付と時刻をタイムスタンプ値として返します。|  
|**四半期 (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の四半期を1-4 の範囲の整数値として返します。1は年1月1日 ~ 3 月31日を表します。|  
|**SECOND (** *time_exp* **)** (ODBC 1.0)|*Time_exp*の2番目のフィールドに基づく2番目のフィールドを、0-59 の範囲の整数値として返します。|
|**タイムスタンプの追加 (** *interval*、 *integer_exp*、 *timestamp_exp* **)** (ODBC 2.0)|*Timestamp_exp*に*integer_exp* *interval*型の間隔を加算することによって計算されたタイムスタンプを返します。 *Interval*の有効な値は、次のキーワードです。<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 秒の小数部は、billionths の秒部分で表現されます。 たとえば、次の SQL ステートメントでは、各従業員の名前と、1年間の記念日が返されます。<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> *Timestamp_exp*が時刻値で、*間隔*が日、週、月、四半期、または年を指定する場合、 *timestamp_exp*の日付部分は、結果のタイムスタンプを計算する前に現在の日付に設定されます。<br /><br /> *Timestamp_exp*が日付値で、 *interval*に秒、秒、分、または時間の小数部が指定されている場合は、結果のタイムスタンプを計算する前に、 *timestamp_exp*の時間部分が0に設定されます。<br /><br /> アプリケーションでは、SQL_TIMEDATE_ADD_INTERVALS オプションを指定して **SQLGetInfo** を呼び出すことによって、データソースがサポートする間隔を決定します。|  
|タイム**スタンプ diff (** *interval*、 *timestamp_exp1*、 *timestamp_exp2* **)** (ODBC 2.0)|*Timestamp_exp2*が*timestamp_exp1*より大きい場合に、型の*間隔*の整数値を返します。 *Interval*の有効な値は、次のキーワードです。<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 秒の小数部は、billionths の秒部分で表現されます。 たとえば、次の SQL ステートメントでは、各従業員の名前と、その従業員が採用した年数が返されます。<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> タイムスタンプ式が時刻値で、 *interval* に日、週、月、四半期、または年が指定されている場合、タイムスタンプの差を計算する前に、そのタイムスタンプの日付部分が現在の日付に設定されます。<br /><br /> Timestamp 式が日付値で、 *interval* に秒、秒、分、時間の小数部が指定されている場合、タイムスタンプの差を計算する前に、そのタイムスタンプの時刻部分が0に設定されます。<br /><br /> アプリケーションでは、SQL_TIMEDATE_DIFF_INTERVALS オプションを指定して **SQLGetInfo** を呼び出すことによって、データソースがサポートする間隔を決定します。|  
|**WEEK (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の週のフィールドに基づいて、1-53 の範囲の整数値として、その年の週を返します。|  
|**YEAR (** *date_exp* **)** (ODBC 1.0)|*Date_exp*の年のフィールドに基づいて、整数値として年を返します。 範囲はデータソースによって異なります。|
