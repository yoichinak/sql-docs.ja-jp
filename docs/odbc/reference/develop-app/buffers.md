---
description: バッファー
title: Buffer |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1c82927c122197249b02a2d327364e68bd851a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494782"
---
# <a name="buffers"></a>バッファー
バッファーは、アプリケーションとドライバーの間でデータを渡すために使用されるアプリケーションメモリの一部です。 たとえば、アプリケーションバッファーは、 **SQLBindCol**を使用して結果セット列に関連付けたり、*バインド*したりすることができます。 各行がフェッチされると、これらのバッファー内の各列に対してデータが返されます。 *入力バッファー* は、アプリケーションからドライバーにデータを渡すために使用されます。 *出力バッファー* は、ドライバーからアプリケーションにデータを返すために使用されます。  
  
> [!NOTE]  
>  ODBC 関数によって SQL_ERROR が返された場合、その関数に対する出力引数の内容は未定義になります。  
  
 このディスカッションでは、主に不確定な型のバッファーが使用されます。 これらのバッファーのアドレスは、 **SQLBindCol**の*targetvalueptr*引数など、sqlpointer 型の引数として表示されます。 ただし、ここで説明するいくつかの項目 (バッファーで使用される引数など) は、ドライバーに文字列を渡すために使用される引数にも適用されます (たとえば、 **Sqltables**の*TableName*引数)。  
  
 これらのバッファーは通常、ペアになっています。 データ*バッファーは*、データ自体を渡すために使用されます。*長さ/インジケーターバッファー*は、データバッファー内のデータの長さを渡すために使用されます。また、データが NULL であることを示す SQL_NULL_DATA などの特殊な値を渡すために使用されます。 データバッファー内のデータの長さは、データバッファー自体の長さとは異なります。 次の図は、データバッファーと長さ/インジケーターバッファーの関係を示しています。  
  
 ![データバッファーと長さ&#47;インジケーターバッファー](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 長さ/インジケーターバッファーは、データバッファーに文字やバイナリデータなどの可変長データが含まれている場合に必要です。 データバッファーに整数や日付構造体などの固定長のデータが含まれている場合は、データの長さが既にわかっているため、インジケーターの値を渡すためだけに長さ/インジケーターバッファーが必要です。 アプリケーションで固定長データを含む長さ/インジケーターバッファーが使用されている場合、ドライバーは、渡された長さを無視します。  
  
 データバッファーとそれに含まれるデータの両方の長さは、文字ではなくバイト単位で計測されます。 ANSI 文字列を使用するプログラムでは、バイト数と文字数の長さが同じであるため、この区別は重要ではありません。  
  
 データバッファーがドライバー定義の記述子フィールド、診断フィールド、または属性を表す場合、アプリケーションは、フィールドまたは属性の値を示す関数の引数の性質をドライバーマネージャーに示す必要があります。 これを行うには、フィールドまたは属性を次のいずれかの値に設定する関数呼び出しの length 引数を設定します。 (この関数は、フィールドまたは属性の値を取得する関数にも当てはまりますが、引数が設定関数の値を指していることを除いて、引数自体に含まれています)。  
  
-   フィールドまたは属性の値を示す関数の引数が文字列へのポインターである場合、 *長さ* の引数は文字列または SQL_NTS の長さになります。  
  
-   フィールドまたは属性の値を示す関数の引数がバイナリバッファーへのポインターである場合、アプリケーションは*長さ*の引数に SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を格納します。 これにより、 *length* 引数に負の値が挿入されます。  
  
-   フィールドまたは属性の値を示す関数の引数が文字列またはバイナリ文字列以外の値へのポインターである場合、 *長さ* の引数には SQL_IS_POINTER 値を指定する必要があります。  
  
-   フィールドまたは属性の値を示す関数の引数に固定長の値が含まれている場合は、必要に応じて、 *長さ* の引数が SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、または SQL_ISI_USMALLINT になります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [遅延バッファー](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [バッファーの割り当てと解放](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [データ バッファーの使用](../../../odbc/reference/develop-app/using-data-buffers.md)
