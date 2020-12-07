---
description: 数値関数
title: 数値関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7575d55ad6632ffa511da32a7155ab8c4d0edf3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425024"
---
# <a name="numeric-functions"></a>数値関数
次の表では、ODBC スカラー関数セットに含まれる数値関数について説明します。 SQL_NUMERIC_FUNCTIONS の*情報の種類*を使用して**SQLGetInfo**を呼び出すことによって、ドライバーでサポートされている数値関数をアプリケーションで特定できます。  
  
 すべての数値関数は、データ型 SQL_FLOAT の値を返します。ただし、ABS、ROUND、TRUNCATE、SIGN、FLOOR、および切り上げは、入力パラメーターと同じデータ型の値を返します。  
  
 *Numeric_exp*として指定される引数には、列の名前、別のスカラー関数の結果、また*は、基*になるデータ型を SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL、SQL_DOUBLE として表すことができます。  
  
 *Float_exp*として指定される引数には、列の名前、別のスカラー関数の結果、または、基になるデータ型を SQL_FLOAT として表すことができる*数値リテラル*を指定できます。  
  
 *Integer_exp*として示される引数には、列の名前、別のスカラー関数の結果、または、基になるデータ型を SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、または SQL_BIGINT として表すことができる*数値リテラル*を指定できます。  
  
 CURRENT_DATE、CURRENT_TIME、および CURRENT_TIMESTAMP スカラー関数が、SQL-92 に合わせて ODBC 3.0 に追加されました。  
  
|機能|説明|  
|--------------|-----------------|  
|**ABS (** _numeric_exp_ **)**  (ODBC 1.0)|*Numeric_exp*の絶対値を返します。|  
|**ACOS (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*のアークコサインをラジアンで表した角度として返します。|  
|**アークサイン (** _float_exp_ **)**  (ODBC 1.0)|ラジアンで表された角度として *float_exp* のアークサインを返します。|  
|**ATAN (** _float_exp_ **)**  (ODBC 1.0)|ラジアンで表された角度として *float_exp* のアークタンジェントを返します。|  
|**ATAN2 (** _float_exp1_、 _float_exp2_**)**  (ODBC 2.0)|*Float_exp1*と*float_exp2*によって指定された*x*座標と*y*座標のアークタンジェントをラジアンで表した角度として返します。|  
|**切り上げ (** _numeric_exp_ **)**  (ODBC 1.0)|*Numeric_exp*以上の最小の整数を返します。 戻り値は、入力パラメーターと同じデータ型です。|  
|**COS (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*のコサインを返します。 *float_exp*はラジアンで表された角度です。|  
|**COT (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*のコタンジェントを返します。 *float_exp*はラジアンで表された角度です。|  
|**度 (** _numeric_exp_ **)**  (ODBC 2.0)|*Numeric_exp*ラジアンから変換された角度の数を返します。|  
|**EXP (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*の指数値を返します。|  
|**FLOOR (** _numeric_exp_ **)**  (ODBC 1.0)|*Numeric_exp*以下の最大の整数を返します。 戻り値は、入力パラメーターと同じデータ型です。|  
|**ログ (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*の自然対数を返します。|  
|**LOG10 (** _float_exp_ **)**  (ODBC 2.0)|*Float_exp*の10を底とする対数を返します。|  
|**MOD (** _integer_exp1_、 _integer_exp2_**)**  (ODBC 1.0)|*Integer_exp2*で割った*integer_exp1*の剰余 (剰余) を返します。|  
|**PI ()**  (ODBC 1.0)|浮動小数点値として pi の定数値を返します。|  
|**POWER (** _numeric_exp_、 _integer_exp_**)**  (ODBC 2.0)|*Integer_exp*の*numeric_exp*の値を返します。|  
|**ラジアン (** _numeric_exp_ **)**  (ODBC 2.0)|*Numeric_exp*度から変換されたラジアン数を返します。|  
|**RAND (**[*integer_exp*]**)**  (ODBC 1.0)|*Integer_exp*を省略可能なシード値として使用して、ランダムな浮動小数点値を返します。|  
|**ROUND (** _numeric_exp_、 _integer_exp_**)**  (ODBC 2.0)|小数点の右側の*integer_exp*の位置に丸められた*numeric_exp*を返します。 *Integer_exp*が負の値の場合、 *numeric_exp*は、小数点の左側に &#124;*integer_exp*&#124; に丸められます。|  
|**SIGN (** _numeric_exp_ **)**  (ODBC 1.0)|*Numeric_exp*の符号を示すインジケーターを返します。 *Numeric_exp*が0未満の場合は、-1 が返されます。 *Numeric_exp*が0の場合は、0が返されます。 *Numeric_exp*が0より大きい場合は、1が返されます。|  
|**SIN (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*のサインを返します。 *float_exp*はラジアンで表された角度です。|  
|**SQRT (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*の平方根を返します。|  
|**TAN (** _float_exp_ **)**  (ODBC 1.0)|*Float_exp*のタンジェントを返します。 *float_exp*はラジアンで表された角度です。|  
|**TRUNCATE (** _numeric_exp_、 _integer_exp_**)**  (ODBC 2.0)|小数点の右側の*integer_exp*の位置に切り捨てられた*numeric_exp*を返します。 *Integer_exp*が負の値の場合、 *numeric_exp*は小数点の左側の&#124; *integer_exp* &#124;に切り捨てられます。|
