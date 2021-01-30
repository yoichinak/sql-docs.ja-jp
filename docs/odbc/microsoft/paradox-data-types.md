---
description: Paradox データ型
title: Paradox データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee49ff2df24a57daa481ea650f57c09a7712400e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203508"
---
# <a name="paradox-data-types"></a>Paradox データ型
ODBC Paradox ドライバーは、Paradox データ型を ODBC SQL データ型にマップします。 次の表に、すべての Paradox データ型の一覧と、マップ先の ODBC SQL データ型を示します。  
  
|Paradox データ型|ODBC データ型|  
|-----------------------|--------------------|  
|英数字|SQL_VARCHAR|  
|自動インクリメント [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|バイト [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|イメージ [2]|SQL_LONGVARBINARY|  
|論理 [1]|SQL_BIT|  
|長い [1]|SQL_INTEGER|  
|メモ [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|時刻 [1]|SQL_TIMESTAMP|  
|タイムスタンプ [1]|SQL_TIMESTAMP|  
  
 [1] は、Paradox バージョン5でのみ有効です。*x*。  
  
 [2] は、Paradox バージョン4に対してのみ有効です。*x* および5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** は、ODBC SQL データ型を返します。 *Odbc プログラマーズリファレンス* の付録 D のすべての変換は、このトピックで前述した odbc SQL データ型に対してサポートされています。  
  
 次の表は、Paradox データ型に関する制限を示しています。  
  
|データ型|説明|  
|---------------|-----------------|  
|英数字|0または指定されていない長さの英数字列を作成すると、実際には255バイトの列が返されます。|  
|BYTES|Paradox5 ドライバーを使用してバイナリ列に NULL を挿入すると、0に変更されます。|  
|LONG|Paradox 5 の Long データ型に対して、Paradox ドライバーでサポートされる最大の負の値。*x* は-2 ^ 31 (-2147483648) ではありません。これは、LONG が ODBC データ型 SQL_INTEGER にマップされているためです。 Long に対してサポートされる最大の負の値は、実際には-2 ^ 31 + 1 (-2147483647) です。|  
|timestamp|Paradox ドライバーによってタイムスタンプ列に値が挿入され、その後列から取得された場合、取得した値と挿入された値が、丸め処理によって1秒ほどに異なる場合があります。|  
  
 データ型に関する制限事項の詳細については、 [「データ型の制限](../../odbc/microsoft/data-type-limitations.md)」を参照してください。
