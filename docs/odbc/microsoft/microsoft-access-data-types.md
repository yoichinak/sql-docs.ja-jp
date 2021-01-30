---
description: Microsoft Access データ型
title: Microsoft Access のデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e7a55c6929d63bf036c9f1585d2eb039f6fec77
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99205704"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access データ型
次の表に、Microsoft Access のデータ型、テーブルの作成に使用されるデータ型、および ODBC SQL データ型を示します。  
  
|Microsoft Access データ型|データ型 (CREATETABLE)|ODBC SQL データ型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|対抗|対抗|SQL_INTEGER|  
|CURRENCY|通貨|SQL_NUMERIC|  
|日付/時刻|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|LONG バイナリ|LONGBINARY|SQL_LONGVARBINARY|  
|長いテキスト|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|記|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|数値 (FieldSize = SINGLE)|1|SQL_REAL|  
|数値 (FieldSize = DOUBLE)|DOUBLE|SQL_DOUBLE|  
|数値 (FieldSize = バイト)|符号なしバイト|SQL_TINYINT|  
|数値 (FieldSize = 整数)|SHORT|SQL_SMALLINT|  
|数値 (FieldSize)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE●ole○|LONGBINARY|SQL_LONGVARBINARY|  
|[TEXT]|VARCHAR|SQL_VARCHAR [1] SQL_WVARCHAR [2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 4.0 アプリケーションのみにアクセスします。 最大長は4000バイトです。 LONGBINARY と同様の動作です。  
  
 [2] ANSI アプリケーションのみ。  
  
 [3] Unicode では、4.0 アプリケーションのみにアクセスします。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** は ODBC データ型を返します。 複数の Microsoft access の種類が同じ ODBC SQL データ型にマップされている場合、Microsoft Access のすべてのデータ型は返されません。 *ODBC プログラマーズリファレンス* の付録 D のすべての変換は、前の表に記載されている SQL データ型に対してサポートされています。  
  
 次の表は、Microsoft Access のデータ型に関する制限を示しています。  
  
|データ型|説明|  
|---------------|-----------------|  
|BINARY、VARBINARY、および VARCHAR|長さ0または未指定の BINARY、VARBINARY、または VARCHAR 型の列を作成すると、実際には510バイトの列が返されます。|  
|BYTE|FieldSize が "バイト" である Microsoft アクセス番号フィールドが符号なしの場合でも、Microsoft Access ドライバーを使用するときに負の値をフィールドに挿入できます。|  
|CHAR、LONGVARCHAR、および VARCHAR|文字列リテラルには、任意の ANSI 文字 (1-255 10 進数) を含めることができます。 2つの連続する単一引用符 (' ') を使用して、1つの単一引用符 (') を表します。<br /><br /> 文字データ型の列で特殊文字を使用する場合は、プロシージャを使用して文字データを渡す必要があります。|  
|DATE|日付値は、ODBC 標準の日付形式に従って区切るか、datetime 区切り記号 ("#") で区切る必要があります。 それ以外の場合、Microsoft Access は値を算術式として扱い、警告やエラーを発生させません。<br /><br /> たとえば、日付 "1996 年3月5日" は、{d ' 1996-03-05 '} または #03/05/1996 #; として表す必要があります。それ以外の場合、03/05/1993 のみが送信されると、Microsoft Access はこれを3で割って1996で割った値を評価します。 この値は、整数の0に切り上げられます。ゼロの日は1899-12-31 にマップされるため、これは使用された日付になります。<br /><br /> 逆引用符で囲まれていても、パイプ文字 (&#124;) を日付値に使用することはできません。|  
|GUID|データ型は、Microsoft Access 4.0 に制限されています。|  
|NUMERIC|データ型は、Microsoft Access 4.0 に制限されています。|  
  
 データ型に関する制限事項の詳細については、 [「データ型の制限](../../odbc/microsoft/data-type-limitations.md)」を参照してください。
