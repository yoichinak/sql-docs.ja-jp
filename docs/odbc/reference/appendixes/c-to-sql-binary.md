---
description: 'C から SQL へ: Binary'
title: 'C から SQL へ: Binary |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e3e1d197a1999c6502848d92222f1c3d6ad5d6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99212423"
---
# <a name="c-to-sql-binary"></a>C から SQL へ: Binary
バイナリ ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_BINARY  
  
 次の表は、バイナリ C データの変換先となる ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|データのバイト長 <= 列バイト長<br /><br /> データ > 列バイト長のバイト長|該当なし<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|データの文字長 <= 列文字の長さ<br /><br /> データ > 列文字長の文字長|該当なし<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|データのバイト長 = SQL データ長<br /><br /> データ <> SQL データ長のバイト長|該当なし<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|データ <の長さ = 列の長さ<br /><br /> 列の長さ > データの長さ|該当なし<br /><br /> 22001|
