---
description: Interval データ型での既定の先頭有効桁数と秒小数部分のオーバーライド
title: Interval データ型の先頭および秒の有効桁数を上書きする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97375bf23a8530d78dea65dc75ce487cc4f807dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425004"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Interval データ型での既定の先頭有効桁数と秒小数部分のオーバーライド
**SQLBindCol**または**SQLSetDescField**のいずれかを呼び出すことによって、の SQL_DESC_TYPE フィールドが Datetime または interval C 型に設定されている場合、SQL_DESC_PRECISION フィールド (秒の有効桁数を含む) は次の既定値に設定されます。  
  
-   6 timestamp の場合は6、2番目のコンポーネントの場合はすべての interval データ型。  
  
-   他のすべてのデータ型の場合は0。  
  
 すべての interval データ型について、SQL_DESC_DATETIME_INTERVAL_PRECISION 記述子フィールドには、先頭のフィールド有効桁数が含まれていますが、既定値は2に設定されています。  
  
 APD の SQL_DESC_TYPE フィールドが、 **SQLBindParameter** または **SQLSetDescField**のいずれかを呼び出すことによって Datetime または interval C 型に設定されている場合、APD 内の SQL_DESC_PRECISION フィールドと SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドは、前に示した既定値に設定されます。 これは入力パラメーターに対しては true ですが、入力/出力パラメーターまたは出力パラメーターには当てはまりません。  
  
 **SQLSetDescRec**を呼び出すと、間隔の先頭の有効桁数が既定値に設定されますが、間隔 (秒) の有効桁数 (SQL_DESC_PRECISION フィールド) は、*有効桁数*の引数の値に設定されます。  
  
 以前に指定した既定値のいずれかがアプリケーションで許容されない場合は、 **SQLSetDescField**を呼び出して、SQL_DESC_PRECISION または SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドを設定する必要があります。  
  
 アプリケーションが **SQLGetData** を呼び出して、データを datetime または interval C 型に返す場合は、既定の間隔の先頭の有効桁数と間隔の秒の有効桁数が使用されます。 既定値を使用できない場合は、アプリケーションで **SQLSetDescField** を呼び出して、いずれかの記述子フィールドを設定するか、または **SQLSetDescRec** を SQL_DESC_PRECISION に設定する必要があります。 記述子フィールドの値を使用するには、 **SQLGetData** の呼び出しに SQL_ARD_TYPE の *TargetType* が必要です。  
  
 **Sqlputdata**が呼び出されると、間隔の先頭の有効桁数と間隔の秒の有効桁数が、実行時データパラメーターまたは列に対応する記述子レコードのフィールドから読み取られます。これは、 **Sqlexecute**または**SQLExecDirect**の呼び出しの APD フィールドであるか、 **sqlputdata**または**SQLSetPos**の呼び出しのフィールドです。
