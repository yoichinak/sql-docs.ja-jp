---
description: 'SQL から C へ: GUID'
title: 'SQL から C: GUID |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a0285850372d78bbe0a24c8707e14e4f5672fb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456503"
---
# <a name="sql-to-c-guid"></a>SQL から C へ: GUID
GUID ODBC SQL データ型の識別子は次のとおりです。  
  
 SQL_GUID  
  
 次の表は、GUID SQL データが変換される可能性がある ODBC C データ型を示しています。 テーブル内の列と用語の詳細については、「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Bufferlength* > 文字のバイト長|データ|36|該当なし|  
||*Bufferlength* < 37|未定義。|未定義。|22003|  
|SQL_C_WCHAR|*Bufferlength* > 文字長|データ|36|該当なし|  
||*Bufferlength* < 37|未定義。|未定義。|22003|  
|SQL_C_BINARY|データ \< =  *バッファー長*のバイト長|データ|データの長さ (バイト単位)|該当なし|  
||データ > *bufferlength*のバイト長|未定義。|未定義。|22003|  
|SQL_C_GUID|なし [a]|データ|16 [b]|該当なし|  
  
 [a] この変換では、 *Bufferlength* の値は無視されます。 ドライバーは、**Targetvalueptr* のサイズが C データ型のサイズであることを前提としています。  
  
 [b] これは、対応する C データ型のサイズです。
