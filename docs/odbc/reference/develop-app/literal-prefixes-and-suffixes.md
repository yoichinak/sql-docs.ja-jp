---
description: リテラル プレフィックスおよびサフィックス
title: リテラルプレフィックスとサフィックス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f658c401bfc31e69a6e5e2fc5110bc9a809f345
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424614"
---
# <a name="literal-prefixes-and-suffixes"></a>リテラル プレフィックスおよびサフィックス
SQL ステートメントでは、 *リテラル* は実際のデータ値の文字表現です。 たとえば、次のステートメントでは、ABC、FFFF、および10がリテラルです。  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 一部のデータ型のリテラルには、特別なプレフィックスとサフィックスが必要です。 前の例では、文字リテラル (ABC) にはプレフィックスとサフィックスの両方として単一引用符 (') が必要です。バイナリリテラル (FFFF) では、プレフィックスとして文字0x が必要です。また、整数リテラル (10) ではプレフィックスまたはサフィックスは必要ありません。  
  
 日付、時刻、およびタイムスタンプを除くすべてのデータ型について、相互運用可能なアプリケーションでは、 **SQLGetTypeInfo**によって作成された結果セット内の列 LITERAL_PREFIX および LITERAL_SUFFIX 列に返される値を使用する必要があります。 Date、time、timestamp、および datetime の各 interval リテラルでは、相互運用可能なアプリケーションで、前のセクションで説明したエスケープシーケンスを使用する必要があります。
