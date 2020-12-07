---
description: ブロック カーソルの使用
title: ブロックカーソルの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67cad7220641e9c3800e89675825cf2c0b1e334d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482865"
---
# <a name="using-block-cursors"></a>ブロック カーソルの使用
ブロックカーソルのサポートは ODBC 3 に組み込まれています。*x*。 **Sqlfetch** は、ODBC 3 で呼び出された場合に複数行フェッチに対してのみ使用できます。*x*;ODBC 2 の場合。*x* アプリケーションは **sqlfetch**を呼び出します。これは、単一行の順方向専用カーソルだけを開きます。 ODBC 3 の場合。*x* アプリケーションは ODBC 2 で **sqlfetch** を呼び出します。*x* ドライバーは、ドライバーが **SQLExtendedFetch**をサポートしていない限り、1つの行を返します。 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [ブロックカーソル、スクロール可能なカーソル、および旧バージョンとの互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 」を参照してください。  
  
 ブロックカーソルを使用するには、アプリケーションは行セットのサイズを設定し、前のセクションで説明したように行セットバッファーをバインドします。オプションで SQL_ATTR_ROWS_FETCHED_PTR および SQL_ATTR_ROW_STATUS_PTR ステートメントの属性を設定し、 **sqlfetch** または **sqlfetchscroll** を呼び出して行のブロックをフェッチします。 行がフェッチされた後でも、アプリケーションは行セットのサイズを変更し、新しい行セットバッファーをバインドします ( **SQLBindCol** を呼び出すか、バインドオフセットを指定します)。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [行セット サイズ](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [フェッチされた行の数と状態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData カーソルとブロックカーソルブロック curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
