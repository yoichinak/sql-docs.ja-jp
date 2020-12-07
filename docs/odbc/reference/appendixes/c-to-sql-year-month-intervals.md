---
description: 'C から SQL へ: 年月の間隔'
title: 'C から SQL: 年月間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffd9a3f7f14ff6af93f15521738bebdbc63a8f58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449024"
---
# <a name="c-to-sql-year-month-intervals"></a>C から SQL へ: 年月の間隔
Month interval ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 次の表は、データ型が年の月を表す ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|列のバイト長 >= 文字バイト長<br /><br /> 列のバイト長 < 文字のバイト長 [a]<br /><br /> データ値は有効な間隔リテラルではありません|該当なし<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|列の文字長 >= データの文字長<br /><br /> 列文字の長さ < データの文字の長さ [a]<br /><br /> データ値は有効な間隔リテラルではありません|該当なし<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|単一フィールドの間隔の変換によって、整数の切り捨てが行われませんでした<br /><br /> 変換の結果、整数の切り捨てが行われる|該当なし<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|データ値は、フィールドを切り捨てずに変換されました<br /><br /> 変換中に1つ以上のデータ値のフィールドが切り捨てられました|該当なし<br /><br /> 22015|  
  
 [a] すべての C interval データ型を文字データ型に変換できます。  
  
 [b] interval 構造体の type フィールドが、間隔が1つのフィールド (SQL_YEAR または SQL_MONTH) である場合は、C の種類の範囲を任意の正確な数値 (SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL、または SQL_NUMERIC) に変換できます。  
  
 間隔 C 型の既定の変換は、対応する年の月の SQL 型になります。  
  
 データを interval C データ型から変換する場合、ドライバーは長さとインジケーターの値を無視し、データバッファーのサイズが interval C データ型のサイズであることを前提としています。 長さ/インジケーターの値は、 **Sqlputdata**の*StrLen_or_Ind*引数と、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定されたバッファーに渡されます。 データバッファーは、 **Sqlputdata**の*DataPtr*引数と**SQLBindParameter**の*parametervalueptr*引数を使用して指定します。
