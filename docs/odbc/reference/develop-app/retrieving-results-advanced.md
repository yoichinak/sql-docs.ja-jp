---
description: 結果の取得 (詳細)
title: 結果の取得 (詳細) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12f5c2ddd1e04b1aef96b7ef1544db9b58a9a58e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461374"
---
# <a name="retrieving-results-advanced"></a>結果の取得 (詳細)
アプリケーションでは、バインドされたデータバッファーアドレスにオフセットを追加するように指定できます。また、 **Sqlbulkoperations**、 **sqlfetch**、 **Sqlbulkoperations**、または **SQLSetPos** が呼び出されたときに、対応する長さ/インジケーターバッファーアドレスを指定することもできます。 これらの追加の結果によって、これらの操作で使用されるアドレスが決まります。  
  
 バインドオフセットを使用すると、アプリケーションは以前にバインドされた列に対して **SQLBindCol** を呼び出さずにバインドを変更できます。 データを再バインドする **SQLBindCol** を呼び出すと、バッファーアドレスと長さ/インジケーターポインターが変更されます。 一方、オフセットを使用して再バインドすると、既存のバインドされたデータバッファーアドレスと長さ/インジケーターバッファーアドレスにオフセットが追加されます。 オフセットが使用されている場合、バインドはアプリケーションバッファーのレイアウト方法の "テンプレート" であり、アプリケーションはオフセットを変更することによって、この "テンプレート" をメモリの別の領域に移動できます。 新しいオフセットはいつでも指定でき、常に元のバインドされた値に追加されます。  
  
 バインドオフセットを指定するために、アプリケーションは、SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性を SQLINTEGER バッファーのアドレスに設定します。 アプリケーションは、バインドを使用する関数 ( **Sqlbulkoperations**、 **sqlfetch**、 **sqlbulkoperations**、 **SQLSetPos**など) を呼び出す前に、このバッファーにバイト単位のオフセットを配置します。ただし、データバッファーアドレスと長さ/インジケーターバッファーアドレスが0でない限り、バインドされた列が結果セット内にある限りです。 アドレスとオフセットの合計は、有効なアドレスである必要があります。 (つまり、オフセットとオフセットが追加されるアドレスの両方または両方が、有効なアドレスである限り無効になることがあります)。SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性はポインターであるため、オフセット値を複数のバインドデータセットに適用できます。これらはすべて、1つのオフセット値を変更することによって変更できます。 アプリケーションでは、カーソルが閉じられるまで、ポインターが有効なままであることを確認する必要があります。  
  
> [!NOTE]  
>  バインドオフセットは ODBC 2 ではサポートされていません。*x* ドライバー。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ブロック カーソル](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC カーソル ライブラリ](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)
