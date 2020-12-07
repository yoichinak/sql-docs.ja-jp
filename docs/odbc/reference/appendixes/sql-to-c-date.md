---
description: 'SQL から C へ: Date'
title: 'SQL から C へ: Date |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5bab301c7a4bc55289006df1c9df5498629f317
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456518"
---
# <a name="sql-to-c-date"></a>SQL から C へ: Date
Date ODBC SQL データ型の識別子は次のとおりです。  
  
 SQL_TYPE_DATE  
  
 次の表は、SQL データの変換先となる ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 文字のバイト長<br /><br /> 11 <= *bufferlength* <= 文字バイト長<br /><br /> *Bufferlength* < 11|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|10<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Bufferlength* > 文字長<br /><br /> 11 <= *bufferlength* <= 文字の長さ<br /><br /> *Bufferlength* < 11|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|10<br /><br /> データの長さ (文字数)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_TYPE_DATE|なし [a]|データ|6 [c]|該当なし|  
|SQL_C_TYPE_TIMESTAMP|なし [a]|データ [b]|16 [c]|該当なし|  
  
 [a] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [b] タイムスタンプ構造の時刻フィールドが0に設定されています。  
  
 [c] これは、対応する C データ型のサイズです。  
  
 SQL データを文字 C データに変換すると、結果の文字列は "*yyyy* - *mm* - *dd*" の形式になります。 この形式は、Windows®の国設定の影響を受けません。
