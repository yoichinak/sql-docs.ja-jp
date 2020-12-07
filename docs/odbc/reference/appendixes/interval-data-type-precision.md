---
description: Interval データ型の精度
title: Interval データ型の有効桁数 |Microsoft Docs
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
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 138cb4cae21b1c1fc0fd742cefac1b6f3a3e5978
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483278"
---
# <a name="interval-data-type-precision"></a>Interval データ型の精度
Interval データ型の有効桁数には、間隔の先頭の有効桁数、間隔の有効桁数、および秒の有効桁数が含まれます。  
  
 間隔の先頭フィールドは符号付き数値です。 先頭フィールドの桁数の最大値は、データ型宣言の一部である *interval の有効桁数* と呼ばれる数量によって決まります。 たとえば、という宣言では、INTERVAL HOUR (5) から MINUTE までの有効桁数は5です。HOUR フィールドには、-99999 ~ 99999 の値を指定できます。 間隔の先頭の有効桁数は、記述子レコードの SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドに含まれています。  
  
 Interval データ型が構成されているフィールドの一覧は、 *間隔の有効桁数*と呼ばれます。 "Precision" という用語は数値ではありません。 たとえば、型間隔の日の間隔の有効桁数は、日、時、分、秒のリストになります。 この値を保持する記述子フィールドはありません。間隔の有効桁数は、常に interval データ型によって決定できます。  
  
 2番目のフィールドを持つ interval データ型には、 *秒の有効桁数*があります。 秒の値の小数部に使用できる10進数の桁数です。 これは、他のデータ型の場合とは異なります。有効桁数は、小数点の前の桁数を示します。 Interval データ型の秒の有効桁数は、小数点の後の桁数です。 たとえば、秒の有効桁数が6に設定されている場合、分数フィールドの123456の数値は. 123456 と解釈され、1230は001230として解釈されます。 その他のデータ型の場合、これを "スケール" と呼びます。 間隔 (秒) の有効桁数は、記述子の SQL_DESC_PRECISION フィールドに含まれています。 SQL interval 値の秒部分の小数部の有効桁数が、C の間隔構造体に保持できる値よりも大きい場合、SQL の間隔の秒の値が C の間隔構造体に変換されるときに、その値が丸められるか、または切り捨てられるかをドライバーで定義します。  
  
 SQL_DESC_CONCISE_TYPE フィールドが interval データ型に設定されている場合、SQL_DESC_TYPE フィールドは SQL_INTERVAL に設定され、SQL_DESC_DATETIME_INTERVAL_CODE は interval データ型のコードに設定されます。 [SQL_DESC_DATETIME_INTERVAL_PRECISION] フィールドは自動的に既定の間隔である2に設定され、[SQL_DESC_PRECISION] フィールドは自動的に既定の間隔 (秒の有効桁数 6) に設定されます。 これらの値のいずれかが適切でない場合、アプリケーションは **SQLSetDescField**の呼び出しを使用して記述子フィールドを明示的に設定する必要があります。
