---
description: 'SQL から C へ: Binary'
title: 'SQL から C へ: Binary |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 229611308c2dba83a8d793810eb5a5443cbd7062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456555"
---
# <a name="sql-to-c-binary"></a>SQL から C へ: Binary
バイナリ ODBC SQL データ型の識別子は次のとおりです。  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 次の表は、バイナリ SQL データの変換先となる ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(データのバイト長) \* 2 < *Bufferlength*<br /><br /> (データのバイト長) \* 2 >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)|該当なし<br /><br /> 01004|  
|SQL_C_WCHAR|(データの文字長) \* 2 < *Bufferlength*<br /><br /> (データの文字長) \* 2 >= *Bufferlength*|データ<br /><br /> 切り捨てられたデータ|データの長さ (文字数)<br /><br /> データの長さ (文字数)|該当なし<br /><br /> 01004|  
|SQL_C_BINARY|データ <のバイト長 = *Bufferlength*<br /><br /> データ > *bufferlength*のバイト長|データ<br /><br /> 切り捨てられたデータ|データの長さ (バイト単位)<br /><br /> データの長さ (バイト単位)|該当なし<br /><br /> 01004|  
  
 バイナリ SQL データを文字 C データに変換する場合、ソースデータの各バイト (8 ビット) は2つの ASCII 文字として表現されます。 これらの文字は、16進数形式の数値を ASCII 文字で表現したものです。 たとえば、バイナリ00000001は "01" に変換され、バイナリ11111111は "FF" に変換されます。  
  
 ドライバーは、常に個々のバイトを16進数のペアに変換し、文字列を null バイトで終了します。 このため、 *Bufferlength* が偶数で、変換されたデータの長さよりも小さい場合、**targetvalueptr* バッファーの最後のバイトは使用されません。 (変換されたデータには偶数のバイト数、次の最後から2番目のバイトは null バイト、最後のバイトは使用できません)。  
  
> [!NOTE]  
>  アプリケーション開発者は、バイナリ SQL データを文字 C データ型にバインドすることは推奨されていません。 通常、この変換は効率が悪く、遅くなります。
