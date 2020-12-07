---
description: SQLSetPos によるデータの更新
title: SQLSetPos | を使用したデータの更新Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eccc08e7af81b2b2b13dd50b2cfb0f5701174e70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476284"
---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos によるデータの更新
アプリケーションは、 **SQLSetPos**を使用して行セット内の任意の行を更新または削除できます。 **SQLSetPos**の呼び出しは、SQL ステートメントの構築と実行に代わる便利な方法です。 データソースで位置指定 SQL ステートメントがサポートされていない場合でも、ODBC ドライバーで位置指定更新をサポートできます。 これは、関数呼び出しを使用してデータベースへの完全アクセスを実現するパラダイムの一部です。  
  
 **SQLSetPos** は現在の行セットに対して動作し、 **sqlfetchscroll**の呼び出しの後にのみ使用できます。 アプリケーションでは、更新、削除、または挿入する行の番号を指定し、ドライバーは行セットのバッファーからその行の新しいデータを取得します。 **SQLSetPos** を使用して、指定した行を現在の行として指定したり、データソースから行セット内の特定の行を更新したりすることもできます。  
  
 行セットサイズは、SQL_ATTR_ROW_ARRAY_SIZE の*属性*引数を使用して**SQLSetStmtAttr**を呼び出すことによって設定されます。 **SQLSetPos** では、 **Sqlfetch** または **sqlfetchscroll**を呼び出した後にのみ、新しい行セットサイズが使用されます。 たとえば、行セットのサイズが変更された場合は、 **sqlsetpos** が呼び出され、 **Sqlfetch** または **sqlfetchscroll** が呼び出されます。 **Sqlsetpos** を呼び出すと、 **sqlfetch** または **sqlfetchscroll** は新しい行セットサイズを使用しますが、古い行セットサイズが使用されます。  
  
 行セット内の先頭行の行番号は 1 です。 **SQLSetPos**の*RowNumber*引数は、行セット内の行を識別する必要があります。つまり、その値は、1から最後にフェッチされた行の数 (行セットのサイズよりも小さくなる場合があります) の範囲内である必要があります。 *RowNumber*が0の場合、操作は行セットのすべての行に適用されます。  
  
 リレーショナルデータベースとのほとんどのやり取りは SQL を通じて行われるため、 **SQLSetPos** は広くサポートされていません。 ただし、ドライバーは、 **UPDATE** ステートメントまたは **DELETE** ステートメントを構築して実行することで、簡単にエミュレートできます。  
  
 **SQLSetPos**がサポートする操作を確認するために、アプリケーションでは、SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 情報オプションを使用して**SQLGetInfo**を呼び出します (カーソルの種類によって異なります)。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLSetPos による行セットの行の更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos による行セットの行の削除](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
