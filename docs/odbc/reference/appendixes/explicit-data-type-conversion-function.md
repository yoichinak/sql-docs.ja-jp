---
description: データ型の明示的な変換用関数
title: 明示的なデータ型変換関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da897469d26cd0403dc023cfcd3f3e03bfceeba4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466189"
---
# <a name="explicit-data-type-conversion-function"></a>データ型の明示的な変換用関数
明示的なデータ型の変換は、SQL データ型定義の観点から指定されます。  
  
 明示的なデータ型変換関数の ODBC 構文では、変換は制限されません。 あるデータ型から別のデータ型への特定の変換の有効性は、ドライバー固有の各実装によって決まります。 ドライバーは ODBC 構文をネイティブ構文に変換するので、ODBC 構文で有効であってもデータソースではサポートされていない変換を拒否します。 ODBC 関数 **SQLGetInfo**は、変換オプション (SQL_CONVERT_BIGINT、SQL_CONVERT_BINARY、SQL_CONVERT_INTERVAL_YEAR_MONTH など) と共に、データソースによってサポートされている変換について照会する手段を提供します。  
  
 **CONVERT**関数の形式は次のとおりです。  
  
 **CONVERT (** _value_exp_、 _data_type_**)**  
  
 関数は、指定された*data_type*に変換*value_exp*によって指定された値を返します。 *data_type*は、次のいずれかのキーワードです。  

:::row:::
    :::column:::
        SQL_BIGINT  
        SQL_BINARY  
        SQL_BIT  
        SQL_CHAR  
        SQL_DATE  
        SQL_DECIMAL  
        SQL_DOUBLE  
        SQL_FLOAT  
        SQL_GUID  
        SQL_INTEGER  
        SQL_INTERVAL_DAY  
        SQL_INTERVAL_DAY_TO_HOUR  
    :::column-end:::
    :::column:::
        SQL_INTERVAL_DAY_TO_MINUTE  
        SQL_INTERVAL_DAY_TO_SECOND  
        SQL_INTERVAL_HOUR  
        SQL_INTERVAL_HOUR_TO_MINUTE  
        SQL_INTERVAL_HOUR_TO_SECOND  
        SQL_INTERVAL_MINUTE  
        SQL_INTERVAL_MINUTE_TO_SECOND  
        SQL_INTERVAL_MONTH  
        SQL_INTERVAL_SECOND  
        SQL_INTERVAL_YEAR  
        SQL_INTERVAL_YEAR_TO_MONTH  
        SQL_LONGVARBINARY  
    :::column-end:::
    :::column:::
        SQL_LONGVARCHAR  
        SQL_NUMERIC  
        SQL_REAL  
        SQL_SMALLINT  
        SQL_TIME  
        SQL_TIMESTAMP  
        SQL_TINYINT  
        SQL_VARBINARY  
        SQL_VARCHAR  
        SQL_WCHAR  
        SQL_WLONGVARCHAR  
        SQL_WVARCHAR  
    :::column-end:::
:::row-end:::

 明示的なデータ型変換関数の ODBC 構文では、変換形式の指定はサポートされていません。 明示的な形式の指定が基になるデータソースでサポートされている場合、ドライバーは既定値を指定するか、形式指定を実装する必要があります。  
  
 引数 *value_exp* には、列名、別のスカラー関数の結果、または数値または文字列リテラルを指定できます。 次に例を示します。  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 CURDATE スカラー関数の出力を文字列に変換します。  
  
 ODBC では、スカラー関数からの戻り値のデータ型が必須ではないため (関数はデータソースに固有のものであるため)、データ型の変換を強制するために、可能な場合は常に CONVERT スカラー関数を使用する必要があります。  
  
 次の2つの例は、 **CONVERT** 関数の使用方法を示しています。 これらの例では、EMPLOYEES という名前のテーブルが存在することを前提としています。 SQL_SMALLINT 型の EMPNO 列と SQL_CHAR 型の EMPNO 列が含まれています。  
  
 アプリケーションで次の SQL ステートメントを指定する場合:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Driver for ORACLE は、SQL ステートメントを次のように変換します。  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server のドライバーは、SQL ステートメントを次のように変換します。  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 アプリケーションで次の SQL ステートメントを指定する場合:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Driver for ORACLE は、SQL ステートメントを次のように変換します。  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server のドライバーは、SQL ステートメントを次のように変換します。  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres のドライバーは、SQL ステートメントを次のように変換します。  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
