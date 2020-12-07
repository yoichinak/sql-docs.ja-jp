---
description: 'SQL から C へ: bit'
title: 'SQL から C へ: Bit |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15f635ea1c325c60e8ae957aed6f8e1f6b7fe58e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456544"
---
# <a name="sql-to-c-bit"></a>SQL から C へ: bit
ビット ODBC SQL データ型の識別子は次のとおりです。  
  
 SQL_BIT  
  
 次の表は、SQL のビットデータを変換できる ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*Bufferlength* > 1<br /><br /> *Bufferlength* <= 1|データ<br /><br /> 未定義。|1<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|なし [a]|データ|C データ型のサイズ|該当なし|  
|SQL_C_BIT|なし [a]|データ|1 [b]|該当なし|  
|SQL_C_BINARY|*Bufferlength* >= 1<br /><br /> *Bufferlength* < 1|データ<br /><br /> 未定義。|1<br /><br /> 未定義。|該当なし<br /><br /> 22003|  
  
 [a] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [b] これは、対応する C データ型のサイズです。  
  
 ビット SQL データを文字 C データに変換する場合、有効な値は "0" と "1" です。
