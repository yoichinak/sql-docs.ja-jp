---
description: 行セット サイズ
title: 行セットサイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d915d6e11fc7678312eab60c3316815cfabab38e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465610"
---
# <a name="rowset-size"></a>行セット サイズ
使用する行セットのサイズは、アプリケーションによって異なります。 通常、画面ベースのアプリケーションは、次の2つの方法のいずれかに従います。 1つ目は、行セットのサイズを画面に表示される行数に設定することです。ユーザーが画面のサイズを変更した場合、アプリケーションはそれに応じて行セットのサイズを変更します。 2つ目の方法では、行セットのサイズを100などのより大きな数値に設定して、データソースへの呼び出しの回数を減らします。 アプリケーションは、可能な場合は、行セット内でローカルにスクロールし、行セットの外にスクロールしたときにのみ新しい行をフェッチします。  
  
 レポートなどの他のアプリケーションでは、行セットのサイズを、アプリケーションが適度に処理できる最大行数に設定する傾向があります。これにより、行ごとのネットワークオーバーヘッドが減少します。 行セットがどれだけ大きくなるかは、各行のサイズと使用可能なメモリの量によって異なります。  
  
 行セットサイズは、SQL_ATTR_ROW_ARRAY_SIZE の*属性*引数を使用して**SQLSetStmtAttr**を呼び出すことによって設定されます。 このアプリケーションでは、行がフェッチされた後であっても ( **SQLBindCol** を呼び出すか、またはバインディングオフセットを指定して)、行セットのサイズを変更したり、行のフェッチ後に新しい行セットバッファーをバインドしたりできます。 行セットサイズを変更した場合の影響は、関数によって異なります。  
  
-   **Sqlfetch** および **sqlfetchscroll** は、呼び出し時に行セットのサイズを使用して、フェッチする行数を決定します。 ただし、 **Sqlfetchscroll** SQL_FETCH_NEXT の *fetchorientation* を使用すると、前のフェッチの行セットに基づいてカーソルがインクリメントされ、現在の行セットのサイズに基づいて行セットがフェッチされます。  
  
-   **Sqlsetpos**は、既に設定されている行セットに対して**sqlsetpos**が動作するため、 **Sqlfetch**または**sqlfetchscroll**の前の呼び出しのときに有効な行セットのサイズを使用します。 また、行セットのサイズが変更された後に**Sqlbulkoperations**が呼び出された場合、 **SQLSetPos**は新しい行セットサイズを取得します。  
  
-   **Sqlbulkoperations** は、フェッチされた行セットとは無関係にテーブルに対して操作を実行するので、呼び出し時に有効な行セットのサイズを使用します。
