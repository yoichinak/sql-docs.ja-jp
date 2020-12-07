---
description: SQLBulkOperations によるデータの更新
title: SQLBulkOperations を使用したデータの更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c8626a0925d0f30792ed92332c0f96efd23f62e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465536"
---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations によるデータの更新
アプリケーションでは、 **Sqlbulkoperations**を呼び出すことにより、データソースの基になるテーブルに対して一括更新、削除、フェッチ、挿入などの操作を実行できます。 **Sqlbulkoperations**の呼び出しは、SQL ステートメントの構築と実行に代わる便利な方法です。 データソースで位置指定 SQL ステートメントがサポートされていない場合でも、ODBC ドライバーで位置指定更新をサポートできます。 これは、関数呼び出しを使用してデータベースへの完全アクセスを実現するパラダイムの一部です。  
  
 **Sqlbulkoperations** は現在の行セットに対して動作し、 **sqlfetch** または **sqlbulkoperations**の呼び出しの後にのみ使用できます。 アプリケーションでは、ブックマークをキャッシュすることによって、更新、削除、または更新する行を指定します。 ドライバーは、更新する行の新しいデータ、または基になるテーブルに挿入する新しいデータを行セットバッファーから取得します。  
  
 **Sqlbulkoperations**によって使用される行セットのサイズは、SQL_ATTR_ROW_ARRAY_SIZE の*属性*引数を指定して**SQLSetStmtAttr**を呼び出すことによって設定されます。 Sqlfetch または**Sqlfetchscroll**の呼び出しの後に新しい行**SQLFetch**セットサイズを使用する**SQLSetPos**とは異なり、 **sqlbulkoperations**は**SQLSetStmtAttr**の呼び出し後に新しい行セットサイズを使用します。  
  
 リレーショナルデータベースとのほとんどのやり取りは SQL を通じて行われるため、 **Sqlbulkoperations** は広くサポートされていません。 ただし、ドライバーは、 **UPDATE**、 **DELETE**、または **INSERT** ステートメントを構築して実行することで、簡単にエミュレートできます。  
  
 **Sqlbulkoperation**がサポートする操作を特定するために、アプリケーションでは、SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 情報オプションを使用して**SQLGetInfo**を呼び出します (カーソルの種類によって異なります)。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLBulkOperations を使ったブックマークによる行の更新](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations を使ったブックマークによる行の削除](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations による行の挿入](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations による行のフェッチ](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
