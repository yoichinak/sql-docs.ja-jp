---
description: C から SQL へのデータ変換の例
title: C から SQL へのデータ変換の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65b0dd229139de060dd79132ee3ca7215906442a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500015"
---
# <a name="c-to-sql-data-conversion-examples"></a>C から SQL へのデータ変換の例
次の例は、ドライバーが C データを SQL データに変換する方法を示しています。  
  
|C 型識別子|C データ値|SQL 型<br /><br /> identifier|列<br /><br /> length|SQL data<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|該当なし|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde...z|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|8 [b]|1234.56|該当なし|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|該当なし|1234.56|該当なし|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|該当なし|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|該当なし|----|22003|  
|SQL_C_TYPE_DATE|1992、12、31 [c]|SQL_CHAR|10|1992-12-31|該当なし|  
|SQL_C_TYPE_DATE|1992、12、31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992、12、31 [c]|SQL_TIMESTAMP|該当なし|1992-12-31 00:00: 00.0|該当なし|  
|SQL_C_TYPE_TIMESTAMP|1992、12、31、23、45、55、120000000 [d]|SQL_CHAR|22|1992-12-31 23:45: 55.12|該当なし|  
|SQL_C_TYPE_TIMESTAMP|1992、12、31、23、45、55、120000000 [d]|SQL_CHAR|21|1992-12-31 23:45: 55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992、12、31、23、45、55、120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\ 0" は、null 終了バイトを表します。 Null 終了バイトは、データの長さが SQL_NTS 場合にのみ必要です。  
  
 [b] 数値のバイト数に加えて、符号には1バイトが必要で、小数点には別のバイトが必要です。  
  
 [c] この一覧の数値は、SQL_DATE_STRUCT 構造体のフィールドに格納されている数値です。  
  
 [d] この一覧の数値は、SQL_TIMESTAMP_STRUCT 構造体のフィールドに格納されている数値です。
