---
description: 混合カーソル
title: 混合カーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b15aaee9d74319daa1a211610ce283d247fda2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424604"
---
# <a name="mixed-cursors"></a>混合カーソル

混合カーソルは、キーセットドリブンカーソルと動的カーソルを組み合わせたものです。 結果セットが大きすぎて結果セット全体のキーを適切に保存できない場合に使用されます。 混合カーソルは、結果セット全体よりも小さく、行セットよりも大きいキーセットを作成することによって実装されます。  
  
 アプリケーションがキーセット内をスクロールしている限り、動作はキーセットドリブンです。 アプリケーションがキーセットの外にスクロールすると、動作は動的になります。カーソルは、要求された行をフェッチし、新しいキーセットを作成します。 新しいキーセットが作成されると、そのキーセット内のキーセットドリブンに動作が戻ります。  
  
 たとえば、結果セットに1000行あり、キーセットのサイズが100で、行セットのサイズが10である混合カーソルを使用しているとします。 最初の行セットがフェッチされると、カーソルは最初の100行のキーで構成されるキーセットを作成します。 次に、要求に応じて最初の10行を返します。  
  
 ここで、別のアプリケーションが11と101の行を削除するとします。 カーソルが行11を取得しようとすると、この行にはキーがありますが、行は存在しないため、ギャップが発生します。これはキーセットドリブン動作です。 カーソルが行101を取得しようとすると、行のキーがないため、カーソルによってその行が欠落していることは検出されません。 代わりに、以前の行102を取得します。 これは動的カーソルの動作です。  
  
 キーセットのサイズが結果セットのサイズと等しい場合、混合カーソルはキーセットドリブンカーソルに相当します。 キーセットのサイズが1に等しい場合、混合カーソルは動的カーソルに相当します。
