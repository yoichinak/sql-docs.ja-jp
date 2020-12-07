---
description: 'SQL から C へ: Time'
title: 'SQL から C へ: Time |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0516cc970238e9535c340c14282be1640ba78513
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429554"
---
# <a name="sql-to-c-time"></a>SQL から C へ: Time
Time ODBC SQL データ型の識別子は次のとおりです。  
  
 SQL_TYPE_TIME  
  
 次の表は、SQL データが変換される可能性がある ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 文字のバイト長<br /><br /> *9*  <= *Bufferlength* <= 文字バイト長<br /><br /> *Bufferlength* < 9|データ<br /><br /> 切り捨てられたデータ [a]<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Bufferlength* > 文字長<br /><br /> *9*  <= *Bufferlength* <= 文字の長さ<br /><br /> *Bufferlength* < 9|データ<br /><br /> 切り捨てられたデータ [a]<br /><br /> 未定義。|データの長さ (文字数)<br /><br /> データの長さ (文字数)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_TYPE_TIME|なし [b]|データ|6 [d]|該当なし|  
|SQL_C_TYPE_TIMESTAMP|なし [b]|データ [c]|16 [d]|該当なし|  
  
 [a] 時間の秒の小数部は切り捨てられます。  
  
 [b] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [c] タイムスタンプ構造の日付フィールドは現在の日付に設定され、timestamp 構造体の秒の小数部のフィールドは0に設定されます。  
  
 [d] これは、対応する C データ型のサイズです。  
  
 SQL データを文字 C データに変換すると、結果の文字列は "*hh*:*mm*:*ss*" の形式になります。 この形式は、Windows®の国設定の影響を受けません。
