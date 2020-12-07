---
description: 行のスクロールとフェッチ (ODBC)
title: 行のスクロールとフェッチ (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6fcdd2cd635a7da66a5d81c4beb24088f96382b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476494"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>行のスクロールとフェッチ (ODBC)
スクロール可能なカーソルを使用すると、アプリケーションは **Sqlfetchscroll** を呼び出してカーソルを移動し、行をフェッチします。 **Sqlfetchscroll** は、相対スクロール (次、前、相対 *n* 行)、絶対スクロール (最初、最後、および行 *n*)、およびブックマークによる配置をサポートしています。 次の図に示すように、 **Sqlfetchscroll**の*Fetchorientation*引数と*fetchorientation*引数は、フェッチする行セットを指定します。  
  
 ![次、前、最初、および最後の行セットのフェッチ](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **次、前、最初、および最後の行セットのフェッチ**  
  
 ![絶対的行セット、相対的行セット、およびブックマーク付き行セットのフェッチ](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **絶対行セット、相対行セット、およびブックマーク付き行セットのフェッチ**  
  
 **Sqlfetchscroll** は、指定された行にカーソルを置いて、その行から始まる行セット内の行を返します。 指定された行セットが結果セットの末尾に重なっている場合は、部分行セットが返されます。 指定された行セットが結果セットの先頭に重なっている場合は、通常、結果セットの最初の行セットが返されます。詳細については、 [Sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 関数の説明を参照してください。  
  
 場合によっては、データを取得せずに、アプリケーションでカーソルを配置することが必要になることがあります。 たとえば、行が存在するかどうかをテストしたり、ネットワーク上で他のデータを使用せずに行のブックマークを取得したりすることができます。 これを行うには、SQL_ATTR_RETRIEVE_DATA statement 属性を SQL_RD_OFF に設定します。 Bookmark 列にバインドされている変数 (存在する場合) は、このステートメント属性の設定に関係なく、常に更新されます。  
  
 行セットが取得されると、アプリケーションは **SQLSetPos** を呼び出して、行セット内の特定の行に移動したり、行セット内の行を更新したりできます。 **Sqlsetpos**の使用方法の詳細については、「sqlsetpos を使用し[たデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)」を参照してください。  
  
> [!NOTE]  
>  スクロールは ODBC 2 でサポートされています。*x* ドライバー ( **SQLExtendedFetch**)。 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [ブロックカーソル、スクロール可能なカーソル、および旧バージョンとの互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)」を参照してください。
