---
description: コンカレンシーの種類
title: 同時実行の種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d55740b71d4e9a7d3b8d22400da0c5b3d94e73d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461544"
---
# <a name="concurrency-types"></a>コンカレンシーの種類
カーソルの同時実行性が低下する問題を解決するために、ODBC では4種類のカーソル同時実行が公開されています。  
  
-   **読み取り** 専用カーソルはデータを読み取ることができますが、データを更新または削除することはできません。 これは、既定の同時実行の種類です。 DBMS は、Repeatable Read および Serializable 分離レベルを適用するために行をロックする場合がありますが、書き込みロックではなく読み取りロックを使用できます。 その結果、他のトランザクションが少なくともデータを読み取ることができるため、同時実行性が向上します。  
  
-   **ロック** カーソルは、必要なロックの最低レベルを使用して、結果セット内の行を更新または削除できるようにします。 これにより、特に Repeatable Read および Serializable トランザクション分離レベルでは、同時実行レベルが非常に低くなります。  
  
-   **値を使用した行バージョンとオプティミスティック同時実行制御を使用したオプティミスティック同時実行制御** カーソルはオプティミスティック同時実行制御を使用します。行が最後に読み取られてから変更されていない場合にのみ、行を更新または削除します。 変更を検出するために、行のバージョンまたは値を比較します。 カーソルが行を更新または削除できる保証はありませんが、同時実行はロックを使用する場合よりもはるかに高くなります。 詳細については、次の「 [オプティミスティック同時実行制御](../../../odbc/reference/develop-app/optimistic-concurrency.md)」セクションを参照してください。  
  
 アプリケーションでは、カーソルが SQL_ATTR_CONCURRENCY statement 属性で使用する同時実行の種類を指定します。 サポートされている型を確認するために、SQL_SCROLL_CONCURRENCY オプションを指定して **SQLGetInfo** を呼び出します。
