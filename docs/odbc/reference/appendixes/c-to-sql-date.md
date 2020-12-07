---
description: 'C から SQL へ: Date'
title: 'C から SQL へ: Date |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f9d8bed4b16ee1c63134cdb9e1ae0b8303b0deb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500005"
---
# <a name="c-to-sql-date"></a>C から SQL へ: Date
Date ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_TYPE_DATE  
  
 次の表は、日付 C データの変換先となる ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列のバイト長 >= 10<br /><br /> 列のバイト長 < 10<br /><br /> データ値が有効な日付ではありません|該当なし<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列の文字長 >= 10<br /><br /> 列の文字長 < 10<br /><br /> データ値が有効な日付ではありません|該当なし<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|データ値は有効な日付です<br /><br /> データ値が有効な日付ではありません|該当なし<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|データ値は有効な日付 [a] です<br /><br /> データ値が有効な日付ではありません|該当なし<br /><br /> 22007|  
  
 [a] タイムスタンプの時刻部分が0に設定されています。  
  
 SQL_C_TYPE_DATE 構造体で有効な値の詳細については、この付録の「 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)」を参照してください。  
  
 日付 C データを文字 SQL データに変換すると、結果として得られる文字データは "*yyyy* - *mm* - *dd*" 形式になります。  
  
 データを date C データ型から変換する場合、ドライバーは長さとインジケーターの値を無視し、データバッファーのサイズが date C データ型のサイズであると想定します。 長さ/インジケーターの値は、 **Sqlputdata**の*StrLen_or_Ind*引数と、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定されたバッファーに渡されます。 データバッファーは、 **Sqlputdata**の*DataPtr*引数と**SQLBindParameter**の*parametervalueptr*引数を使用して指定します。
