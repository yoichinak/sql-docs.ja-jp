---
description: テキスト ファイルのデータ型
title: テキストファイルのデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d14d98f7aa25c42ec6d121aa0819a1f3dcce5db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449104"
---
# <a name="text-file-data-types"></a>テキスト ファイルのデータ型
次の表は、テキストデータ型を ODBC SQL データ型にマップする方法を示しています。 Odbc テキストドライバーでは、すべての ODBC SQL データ型がサポートされているわけではないことに注意してください。  
  
|Text データ型|ODBC データ型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** は ODBC データ型を返します。 *ODBC プログラマーズリファレンス*の付録 D のすべての変換は、前の表に記載されている SQL データ型に対してサポートされています。  
  
 次の表は、テキストデータ型の制限を示しています。  
  
|データ型|説明|  
|---------------|-----------------|  
|CHAR|長さが0または指定されていない CHAR 型の列を作成すると、実際には255ビットの列が返されます。<br /><br /> 区切られたファイルでは、CHAR 型の列の先頭と末尾に二重引用符の区切り記号が含まれている場合と終了しない場合があります。固定長ファイルでは、二重引用符は区切り記号として使用されません。|  
|DATETIME|MM-DD-YY (例: 01-17-92)<br /><br /> MMM-DD-YY (たとえば、Jan-17-92)<br /><br /> DD-MMM-YY (例:17-Jan-92)<br /><br /> YYYY-MM-DD (たとえば、1992-01-17)<br /><br /> YYYY-MMM-DD (たとえば、1992-Jan-17)<br /><br /> テーブル内では、日付の区切り記号を混在させることはできません。<br /><br /> テキスト ISAM は、Windows のコントロールパネルの [インターナショナル] 設定に応じて、米国または欧州形式の DATETIME フィールドを書式設定します。|  
|FLOAT|最大幅には、符号と小数点が含まれます。 Schema.ini では、幅は次のように表されます。<br /><br /> 14.083 は浮動小幅6<br /><br /> -14.083 は浮動小幅7<br /><br /> + 14.083 は浮動小幅7<br /><br /> 14083. は浮動小幅6です<br /><br /> FLOAT 型の列の場合、ODBC は常に8を返します。<br /><br /> FLOAT 型の列には、次のような科学的表記法を使用することもできます。<br /><br /> -3.04 e + 2 は Float 幅8<br /><br /> 25E4 は浮動小幅4<br /><br /> **メモ** Decimal および科学的表記法を1つの列に混在させることはできません。<br /><br /> NULL 値は固定長ファイル内の空白で埋め込まれた文字列によって表され、区切られたファイルでは省略されます。<br /><br /> Float データは、先頭に空白を埋め込むことができます。|  
|INTEGER|整数型の列の有効な値は、32767 ~-32766 です。<br /><br /> Schema.ini では、幅は次のように表されます。<br /><br /> 14083は整数の幅5<br /><br /> 0は整数の幅1です<br /><br /> ODBC では、整数列に対して常に4が返されます。<br /><br /> 最大幅には符号が含まれています。 整数型の列の最大幅は11ですが、固定形式のテーブルで使用できる空白のために幅が長くなる可能性があります。|  
|LONGCHAR|固定長または区切られたテーブルの LONGCHAR 列の幅の理論的な制限は、65500K です。 テキスト ISAM は、最大32K の信頼性の高いサポートを提供する可能性が高くなります。|  
  
 データ型に関する制限事項の詳細については、 [「データ型の制限](../../odbc/microsoft/data-type-limitations.md)」を参照してください。
