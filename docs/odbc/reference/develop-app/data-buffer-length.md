---
description: データ バッファーの長さ
title: データバッファーの長さ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ad4f083d9f08c744dd6f832638a49b57c04e6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429374"
---
# <a name="data-buffer-length"></a>データ バッファーの長さ
アプリケーションは、データバッファーのバイト長を、 *Bufferlength* または類似した名前という名前の引数でドライバーに渡します。 たとえば、次の **SQLBindCol**への呼び出しでは、アプリケーションは *valueptr* バッファー (**sizeof (***valueptr***)**) の長さを指定します。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 ドライバーは、出力文字列引数を持つ関数のバッファー長引数の文字数ではなく、常にバイト数を返します。  
  
 データバッファーの長さは、出力バッファーに対してのみ必要です。ドライバーは、バッファーの末尾を越えた書き込みを回避するためにこれらを使用します。 ただし、ドライバーは、バッファーに文字やバイナリデータなどの可変長データが含まれている場合にのみ、データバッファーの長さを確認します。 バッファーに整数や日付の構造などの固定長のデータが含まれている場合、ドライバーはデータバッファーの長さを無視し、バッファーがデータを保持するのに十分な大きさであると想定します。つまり、固定長のデータは切り捨てられません。 このため、アプリケーションで固定長データ用に十分な大きさのバッファーを割り当てることが重要です。  
  
 データ以外の出力文字列の切り捨てが発生した場合 ( **Sqlgetcursor name**に返されるカーソル名など)、バッファー長引数で返される長さは、可能な最大文字数になります。  
  
 データバッファーの長さは、ドライバーがこれらのバッファーに書き込むことができないため、入力バッファーには必要ありません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [長さ/インジケーター値の使用](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [データの長さ、バッファー長、および切り捨て](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [文字データと C 文字列](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
