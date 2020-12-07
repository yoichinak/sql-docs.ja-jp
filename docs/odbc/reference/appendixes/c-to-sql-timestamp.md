---
description: 'C から SQL へ: Timestamp'
title: 'C から SQL へ: Timestamp |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e51d82e8acd59c8b4e6f5a8385720b0bd38eba4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449034"
---
# <a name="c-to-sql-timestamp"></a>C から SQL へ: Timestamp
タイムスタンプの ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_TYPE_TIMESTAMP  
  
 次の表は、タイムスタンプ C データの変換先となる ODBC SQL データ型を示しています。 テーブル内の列と用語の詳細については、「 [データを C から SQL データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」を参照してください。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列のバイト長 >= 文字バイト長<br /><br /> 19 <= 列のバイト長 < 文字のバイト長<br /><br /> 列のバイト長 < 19<br /><br /> データ値が有効なタイムスタンプではありません|該当なし<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列の文字長 >= データの文字長<br /><br /> 19 <= 列文字の長さ < 文字長のデータ<br /><br /> 列の文字長 < 19<br /><br /> データ値が有効なタイムスタンプではありません|該当なし<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|時刻フィールドが0です。<br /><br /> Time フィールドが0以外である<br /><br /> データ値に有効な日付が含まれていません|該当なし<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|秒の小数部のフィールドがゼロ [a]<br /><br /> 秒の小数部のフィールドが0以外の場合 [a]<br /><br /> データ値に有効な時刻が含まれていません|該当なし<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|秒の小数部のフィールドは切り捨てられません<br /><br /> 秒の小数部のフィールドは切り捨てられます<br /><br /> データ値が有効なタイムスタンプではありません|該当なし<br /><br /> 22008<br /><br /> 22007|  
  
 [a] タイムスタンプ構造の日付フィールドは無視されます。  
  
 SQL_C_TIMESTAMP 構造体で有効な値の詳細については、この付録の「 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)」を参照してください。  
  
 Timestamp C データを文字 SQL データに変換すると、結果として得られる文字データは "*yyyy* - *mm* - *dd* *hh*:*mm*:*ss*" になります。*f...*] "形式.  
  
 タイムスタンプ C データ型からデータを変換する場合、ドライバーは長さ/インジケーター値を無視し、データバッファーのサイズが timestamp C データ型のサイズであると想定します。 長さ/インジケーターの値は、 **Sqlputdata**の*StrLen_or_Ind*引数と、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定されたバッファーに渡されます。 データバッファーは、 **Sqlputdata**の*DataPtr*引数と**SQLBindParameter**の*parametervalueptr*引数を使用して指定します。
