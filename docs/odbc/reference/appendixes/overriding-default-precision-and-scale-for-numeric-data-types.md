---
description: 数値データ型での既定の有効桁数と小数点以下桁数のオーバーライド
title: 数値データ型の既定の有効桁数と小数点以下桁数のオーバーライド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 798e607ff6584bde27791a29e4b20aeb1d7bb3cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466084"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>数値データ型での既定の有効桁数と小数点以下桁数のオーバーライド
**SQLBindCol**または**SQLSetDescField**のいずれかを呼び出すことによって、の SQL_DESC_TYPE フィールドが SQL_C_NUMERIC に設定されている場合、の SQL_DESC_SCALE フィールドは0に設定され、SQL_DESC_PRECISION フィールドはドライバーで定義された既定の有効桁数に設定されます。 これは、 **SQLBindParameter** または **SQLSetDescField**のいずれかを呼び出すことによって、APD の SQL_DESC_TYPE フィールドが SQL_C_NUMERIC に設定されている場合にも当てはまります。 これは、入力、入出力、または出力パラメーターの場合に当てはまります。  
  
 前述のいずれかの既定値をアプリケーションで使用できない場合、アプリケーションは **SQLSetDescField** または **SQLSetDescRec**を呼び出して、SQL_DESC_SCALE または SQL_DESC_PRECISION フィールドを設定する必要があります。  
  
 アプリケーションが **SQLGetData** を呼び出してデータを SQL_C_NUMERIC 構造に返す場合は、既定の SQL_DESC_SCALE と SQL_DESC_PRECISION のフィールドが使用されます。 既定値を使用できない場合は、アプリケーションが**SQLSetDescRec**または**SQLSetDescField**を呼び出してフィールドを設定し、SQL_ARD_TYPE の*TargetType*で**SQLGetData**を呼び出して、記述子フィールドの値を使用する必要があります。  
  
 **Sqlputdata**が呼び出されると、呼び出しでは、実行時データパラメーターまたは列に対応する記述子レコードの SQL_DESC_SCALE および SQL_DESC_PRECISION のフィールドが使用されます。これは、 **Sqlexecute**または**SQLExecDirect**の呼び出しの APD フィールドであるか、 **sqlputdata**または**SQLSetPos**の呼び出しのフィールドです。
