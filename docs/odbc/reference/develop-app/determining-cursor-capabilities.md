---
description: カーソル機能の決定
title: カーソル機能の決定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3390f83a30f6f462148d477ec018d1209ee6e098
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465824"
---
# <a name="determining-cursor-capabilities"></a>カーソル機能の決定
**SQLGetInfo**の次の4つのオプションでは、サポートされているカーソルの種類とその機能について説明しています。  
  
-   SQL_CURSOR_SENSITIVITY。 カーソルが別のカーソルによって行われた変更に影響を受けているかどうかを示します。  
  
-   SQL_SCROLL_OPTIONS。 サポートされているカーソルの種類 (順方向専用、静的、キーセットドリブン、動的、または混在) を一覧表示します。 すべてのデータソースは順方向専用カーソルをサポートする必要があります。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 (カーソルの種類によって異なります)。 スクロール可能なカーソルでサポートされているフェッチの種類を一覧表示します。 戻り値のビットは、 **Sqlfetchscroll**のフェッチの型に対応します。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 または SQL_STATIC_CURSOR_ATTRIBUTES2 (カーソルの種類によって異なります)。 静的カーソルとキーセットドリブンカーソルが独自の更新、削除、および挿入を検出できるかどうかを示します。  
  
 アプリケーションでは、これらのオプションを指定して **SQLGetInfo** を呼び出すことによって、実行時にカーソル機能を決定できます。 これは一般的に汎用アプリケーションによって行われます。 また、カーソル機能は、アプリケーションの開発中に特定したり、アプリケーションにハードコーディングしたりすることもできます。 これは通常、垂直およびカスタムアプリケーションによって行われますが、ODBC カーソルライブラリなどのクライアント側のカーソル実装を使用する汎用アプリケーションでも実行できます。
