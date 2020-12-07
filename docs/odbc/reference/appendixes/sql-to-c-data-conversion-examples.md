---
description: SQL から C へのデータ変換の例
title: SQL から C へのデータ変換の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7a3d70a6f74a814262ddad580b5e5a2b0d79927
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429584"
---
# <a name="sql-to-c-data-conversion-examples"></a>SQL から C へのデータ変換の例

次の表に示す例では、ドライバーが SQL データを C データに変換する方法を示しています。  
  
|SQL 型<br /><br /> identifier|SQL data<br /><br /> value|C 型<br /><br /> identifier|バッファー<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|該当なし|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56 \ 0 [a]|該当なし|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234 \ 0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|無視|1234.56|該当なし|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|無視|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|無視|----|22003|  
|SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|無視|1.2345678|該当なし|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|無視|1.234567|該当なし|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|無視|1|該当なし|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31 \ 0 [a]|該当なし|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|無視|1992、12、31、0、0、0、0 [b]|該当なし|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45: 55.12|SQL_C_CHAR|23|1992-12-31 23:45: 55.12 \ 0 [a]|該当なし|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45: 55.12|SQL_C_CHAR|22|1992-12-31 23:45: 55.1 \ 0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45: 55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\ 0" は、null 終了バイトを表します。 ドライバーは、常に SQL_C_CHAR データを null で終了します。  
  
 [b] この一覧の数値は、TIMESTAMP_STRUCT 構造体のフィールドに格納されている数値です。
