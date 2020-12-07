---
description: ODBC 静的カーソル
title: ODBC の静的カーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9689badd39e21f82c268be904b29ffb1fa90a8ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429164"
---
# <a name="odbc-static-cursors"></a>ODBC 静的カーソル
静的カーソルとは、結果セットが静的であることを示します。 通常、カーソルを開いた後に、結果セットのメンバーシップ、順序、または値に対して行われた変更は検出されません。 たとえば、静的カーソルによって行がフェッチされ、別のアプリケーションによってその行が更新されるとします。 静的カーソルによって行が refetches された場合、他のアプリケーションによって行われた変更にかかわらず、表示される値は変更されません。  
  
 静的カーソルは、独自の更新、削除、および挿入を検出できますが、この操作は必要ありません。 特定の静的カーソルによってこれらの変更が検出されるかどうかは、 **SQLGetInfo**の SQL_STATIC_SENSITIVITY オプションを使用して報告されます。 静的カーソルは、他の更新、削除、および挿入を検出しません。  
  
 SQL_ATTR_ROW_STATUS_PTR statement 属性によって指定された行の状態の配列には、任意の行の SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、または SQL_ROW_ERROR を含めることができます。 カーソルによって更新、削除、または挿入された行の SQL_ROW_UPDATED、SQL_ROW_DELETED、または SQL_ROW_ADDED が返されます。このような変更は、カーソルによって検出されることが前提となります。  
  
 静的カーソルは、通常、結果セットの行をロックするか、結果セットのコピー (スナップショット) を作成することによって実装されます。 行のロックは比較的簡単ですが、同時実行性が大幅に低下するという欠点があります。 コピーを作成すると、同時実行性が向上し、カーソルはそのコピーを変更することで、独自の更新、削除、および挿入を追跡できます。 ただし、コピーの方がコストがかかり、データが他のユーザーによって変更されるため、基になるデータから逸脱することがあります。
