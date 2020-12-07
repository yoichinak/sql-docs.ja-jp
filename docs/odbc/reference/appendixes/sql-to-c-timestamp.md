---
description: 'SQL から C へ: Timestamp'
title: 'SQL から C へ: Timestamp |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a2904f01b5ecadbfc224d052366197e41163cd9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429544"
---
# <a name="sql-to-c-timestamp"></a>SQL から C へ: Timestamp

Timestamp ODBC SQL データ型の識別子は次のとおりです。

- SQL_TYPE_TIMESTAMP  

次の表は、SQL データを変換できる ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  

|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 文字のバイト長<br /><br /> 20 <= *bufferlength* <= 文字バイト長<br /><br /> *Bufferlength* < 20|データ<br /><br /> 切り捨てられたデータ [b]<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Bufferlength* > 文字長<br /><br /> 20 <= *bufferlength* <= 文字の長さ<br /><br /> *Bufferlength* < 20|データ<br /><br /> 切り捨てられたデータ [b]<br /><br /> 未定義。|データの長さ (文字数)<br /><br /> データの長さ (文字数)<br /><br /> 未定義。|該当なし<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 未定義。|データの長さ (バイト単位)<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_TYPE_DATE|タイムスタンプの時刻部分がゼロ [a]<br /><br /> タイムスタンプの時刻部分が0以外の場合 [a]|データ<br /><br /> 切り捨てられたデータ [c]|6 [f]<br /><br /> 6 [f]|該当なし<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|タイムスタンプの秒部分の小数部がゼロ [a]<br /><br /> タイムスタンプの秒の小数部が0以外の場合 [a]|データ [d]<br /><br /> 切り捨てられたデータ [d], [e]|6 [f]<br /><br /> 6 [f]|該当なし<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|タイムスタンプの秒の小数部が切り捨てられない [a]<br /><br /> タイムスタンプの秒部分の小数部が切り捨てられる [a]|データ [e]<br /><br /> 切り捨てられたデータ [e]|16 [f]<br /><br /> 16 [f]|該当なし<br /><br /> 01S07|  

 [a] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [b] タイムスタンプの秒の小数部は切り捨てられます。  
  
 [c] タイムスタンプの時刻部分が切り捨てられています。  
  
 [d] タイムスタンプの日付部分は無視されます。  
  
 [e] タイムスタンプの秒部分の小数部は切り捨てられます。  
  
 [f] これは、対応する C データ型のサイズです。  

Timestamp SQL データが文字 C データに変換されると、結果の文字列は "*yyyy* - *mm* - *dd* *hh*:*mm*:*ss*[.*f...*] "形式。秒の小数部には最大9桁まで使用できます。 この形式は、Windows®の国設定の影響を受けません。 (小数点と秒の小数部を除き、タイムスタンプの SQL データ型の有効桁数に関係なく、形式全体を使用する必要があります)。
