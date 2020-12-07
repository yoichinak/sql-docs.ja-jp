---
description: 列サイズ、10進数、転送オクテット長、および表示サイズ-ODBC
title: 列サイズ、10進数字、転送オクテット長、表示サイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d00a23fb38bdece97ffcbde0974b7bdf893a5133
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421506"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>列サイズ、10進数、転送オクテット長、および表示サイズ-ODBC
データ型は、列 (またはパラメーター) のサイズ、10進数、長さ、および表示サイズによって特徴付けられます。 次の ODBC 関数は、SQL ステートメントのパラメーターまたはデータソースの SQL データ型に対してこれらの属性を返します。 各 ODBC 関数は、次のように、これらの属性の異なるセットを返します。  
  
-   **SQLDescribeCol** は、列のサイズと、それが記述する列の10進数を返します。  
  
-   **SQLDescribeParam** は、記述されているパラメーターのサイズと小数点以下桁数を返します。 **SQLBindParameter** は、SQL ステートメントのパラメーターのサイズと小数点以下桁数を設定します。  
  
-   カタログ関数 **Sqlcolumns**、 **SQLProcedureColumns**、および **SQLGetTypeInfo** は、テーブル内の列、結果セット、またはプロシージャパラメーターとデータソース内のデータ型のカタログ属性の属性を返します。 **Sqlcolumns** は、列のサイズ、10進数、および指定されたテーブル内の列の長さ (ベーステーブル、ビュー、システムテーブルなど) を返します。 **SQLProcedureColumns** は、プロシージャ内の列のサイズ、10進数、および長さを返します。 **SQLGetTypeInfo** は、列の最大サイズと、データソースの SQL データ型の最小および最大の小数点以下桁数を返します。  
  
 これらの関数によって列またはパラメーターのサイズに対して返される値は、ODBC 2 で定義されている "有効桁数" に対応します。*x*。 ただし、値は必ずしも SQL_DESC_PRECISION またはその他の1つの記述子フィールドで返される値に対応しているわけではありません。 これは、ODBC 2 で定義されている "scale" に対応する10進数字にも当てはまります。*x*。 SQL_DESC_SCALE またはその他の1つの記述子フィールドで返される値に必ずしも対応しているわけではありませんが、データ型に応じて異なる記述子フィールドから取得されます。 詳細については、「 [列のサイズ](../../../odbc/reference/appendixes/column-size.md) と [小数点以下桁数](../../../odbc/reference/appendixes/decimal-digits.md)」を参照してください。  
  
 同様に、転送オクテット長の値は SQL_DESC_LENGTH からは取得されません。 これらは、すべての文字型およびバイナリ型の記述子のフィールドの SQL_DESC_OCTET_LENGTH から取得されます。 他の型については、この情報を保持する記述子フィールドはありません。  
  
 すべてのデータ型の表示サイズ値は、1つの記述子フィールドの値 SQL_DESC_DISPLAY_SIZE に対応します。  
  
 記述子フィールドは、結果セットの特性を記述します。 記述子フィールドには、ステートメントを実行する前のデータに関する有効な値が含まれていません。 一方、 **Sqlcolumns**、 **SQLProcedureColumns**、および **SQLGetTypeInfo**によって返される列サイズ、10進数字、および表示サイズの値は、データソースのカタログに存在するテーブル列やデータ型などのデータベースオブジェクトの特性を返します。 同様に、結果セットでは、 **Sqlcolattribute** によって、列のサイズ、10進数、およびデータソースの列の転送オクテット長が返されます。これらの値は、必ずしも SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_OCTET_LENGTH 記述子フィールドの値と同じではありません。  
  
 これらの記述子フィールドの詳細については、「 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」を参照してください。  
  
 関連トピック:  
  
-   [列サイズ](../../../odbc/reference/appendixes/column-size.md)  
-   [10 進数字](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [転送オクテット長](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [表示サイズ](../../../odbc/reference/appendixes/display-size.md)
