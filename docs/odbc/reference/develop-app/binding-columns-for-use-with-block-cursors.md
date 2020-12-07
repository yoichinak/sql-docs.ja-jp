---
description: ブロック カーソルで使用するためのバインディング列
title: ブロックカーソルで使用する列をバインドする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a58e6359bd7b0ad5d44f75a3d844ef2e9872f2a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429444"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>ブロック カーソルで使用するためのバインディング列
ブロックカーソルは複数の行を返すので、それらを使用するアプリケーションは、変数の配列を1つの変数ではなく各列にバインドする必要があります。 これらの配列は、まとめて *行セットバッファー*と呼ばれます。 バインディングの2つのスタイルを次に示します。  
  
-   各列に配列をバインドします。 各データ構造 (配列) には1つの列のデータが含まれているため、これは *列方向のバインド* と呼ばれます。  
  
-   行全体のデータを保持する構造体を定義し、これらの構造体の配列をバインドします。 各データ構造に1つの行のデータが含まれているため、これは行方向の *バインド* と呼ばれます。  
  
 アプリケーションが単一の変数を列にバインドするときは、 **SQLBindCol** を呼び出して、配列を列にバインドします。 唯一の違いは、渡されるアドレスが配列アドレスであり、単一の変数アドレスではないことです。 アプリケーションでは、列方向のバインドと行方向のバインドのどちらを使用しているのかを指定するために SQL_BIND_BY_COLUMN statement 属性を設定します。 列方向のバインドと行方向のバインドのどちらを使用するかは、主にアプリケーションの設定に関係しています。 行方向のバインドは、アプリケーションのデータレイアウトにより密接に対応する場合があります。その場合、パフォーマンスが向上します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [列方向のバインド](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [行方向のバインド](../../../odbc/reference/develop-app/row-wise-binding.md)
