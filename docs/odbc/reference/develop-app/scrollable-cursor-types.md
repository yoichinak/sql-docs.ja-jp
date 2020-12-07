---
description: スクロール可能なカーソルの種類
title: スクロール可能なカーソルの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c27ccd54bfe0ba099d78c002fce4c901e4bf8c1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476514"
---
# <a name="scrollable-cursor-types"></a>スクロール可能なカーソルの種類
スクロール可能なカーソルの4種類は、静的、動的、キーセットドリブン、および混合です。 静的カーソルは、変更の数が少ないかどうかを検出しますが、実装するには比較的安価です。 動的カーソルはすべての変更を検出しますが、実装にはコストがかかります。 キーセットドリブンカーソルと混合カーソルは、ほとんどの変更を検出しますが、動的カーソルよりも低コストです。  
  
 スクロール可能な各カーソルの種類の特性を定義するには、次の用語を使用します。  
  
-   **更新、削除、および挿入を独自に行う。** カーソルによって行われた更新、削除、挿入は、 **Sqlbulkoperations** または **SQLSetPos** を呼び出すか、位置指定の update または delete ステートメントを使用して行われます。  
  
-   **その他の更新、削除、および挿入。** カーソルによって行われていない更新、削除、および挿入は、同じトランザクション内の他の操作によって行われたものや、他のトランザクションによって作成されたものなど、他のアプリケーションによって作成されたものも含みます。  
  
-   **要素.** 結果セット内の行のセット。  
  
-   **順序.** カーソルによって行が返される順序。  
  
-   **値.** 結果セットの各行の値。  
  
 データを更新、削除、および挿入する方法の詳細については、「 [データの更新の概要](../../../odbc/reference/develop-app/updating-data-overview.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC 静的カーソル](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動的カーソル](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [キーセット ドリブン カーソル](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合カーソル](../../../odbc/reference/develop-app/mixed-cursors.md)
