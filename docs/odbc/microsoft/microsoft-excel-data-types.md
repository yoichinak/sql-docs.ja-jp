---
description: Microsoft Excel のデータ型
title: Microsoft Excel のデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3e54ece7962fc5b56e4b9fcc17123ac7ad3c9e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466434"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel のデータ型
次の表は、Microsoft Excel ドライバーのデータ型を ODBC SQL データ型にマップする方法を示しています。 Microsoft Excel ドライバーは、列のデータに基づいて、これらのデータ型を Microsoft Excel テーブルの列に割り当てます。  
  
|Microsoft Excel のデータ型|ODBC データ型|  
|-------------------------------|--------------------|  
|通貨|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LUN|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|[TEXT]|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** は、ODBC SQL データ型を返します。 *Odbc プログラマーズリファレンス*の付録 D のすべての変換は、このトピックで前述した odbc SQL データ型に対してサポートされています。  
  
 次の表は、Microsoft Excel のデータ型に関する制限を示しています。  
  
|データ型|説明|  
|---------------|-----------------|  
|暗号化データ|Microsoft Excel ドライバーは暗号化されたデータを読み取ることができません。|  
|エラー文字列|Microsoft Excel driver は、Microsoft Excel のエラー値 (#N/A!、#VALUE!、#REF!、#DIV/0!、#NUM!、#NAME?、および #NULL!) の文字列を返すことができませんが、代わりに NULL が返されます。|  
|LUN|論理列の値は、0または1として SQL_C_CHAR バッファーに返されます。|  
|NUMBER|整数型の列が作成された場合、整数データ型に対して大きすぎる数値を入力できます。また、整数以外の値を含むデータを挿入することもできます。その結果、列が SQL_DOUBLE に変換される可能性があります。|  
|[TEXT]|列の行に複数の Microsoft Excel データ型が含まれている場合は、ODBC Microsoft Excel driver によって SQL_VARCHAR データ型が列に割り当てられます。 この例外が発生するのは、1つの列に datetime データ型 (DATE、TIME、および DATETIME) が2つまたは3つ含まれている場合、ODBC Microsoft Excel ドライバーによって列に SQL_TIMESTAMP データ型が割り当てられます。<br /><br /> 長さが0または指定されていないテキスト列を作成すると、実際には255バイトの列が返されます。<br /><br /> 文字列リテラルには、任意の ANSI 文字 (1-255 10 進数) を含めることができます。 2つの連続する単一引用符 (") を使用して、1つの単一引用符 (') を表します。<br /><br /> SQL_VARCHAR 以外のデータ型の列に NULL を挿入すると、列のデータ型が SQL_VARCHAR に変更されます。|  
  
 データ型に関する制限事項の詳細については、 [「データ型の制限](../../odbc/microsoft/data-type-limitations.md)」を参照してください。
