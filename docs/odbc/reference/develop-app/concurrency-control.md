---
description: 同時実行制御
title: 同時実行制御 | Microsoft Docs
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
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e47308cc0224ef73689a3b82d1ab4186fd0c823a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461554"
---
# <a name="concurrency-control"></a>同時実行制御
*同時実行* は、2つのトランザクションが同時に同じデータを使用できるようにする機能であり、トランザクションの分離を増やすことで、通常は同時実行性が低下します。 これは、トランザクション分離は通常、行をロックすることによって実装されるためです。また、ロックされている行が増えるにつれて、ロックされた行によって一時的にブロックされることなく、トランザクションを完了できるようになります。 データベースの整合性を維持するために必要な高いトランザクション分離レベルのトレードオフとして、同時実行数の削減が一般に認められていますが、カーソルを使用する読み取り/書き込みアクティビティが高い対話型アプリケーションで問題になる可能性があります。  
  
 たとえば、アプリケーションが SQL ステートメントの **select \* FROM Orders**を実行するとします。 このメソッドは、 **Sqlfetchscroll** を呼び出して結果セットをスクロールし、ユーザーが注文を更新、削除、または挿入できるようにします。 ユーザーが注文を更新、削除、または挿入すると、アプリケーションによってトランザクションがコミットされます。  
  
 分離レベルが Repeatable Read の場合、トランザクションの実装方法によっては、 **Sqlfetchscroll**によって返される各行がロックされる可能性があります。 分離レベルが Serializable の場合、トランザクションによって Orders テーブル全体がロックされる可能性があります。 どちらの場合も、トランザクションはコミットまたはロールバックされたときにのみロックを解放します。 そのため、ユーザーが注文の読み取りに多くの時間を費やし、更新、削除、または挿入の時間が非常に少ない場合、トランザクションは多数の行を簡単にロックして、他のユーザーが使用できないようにすることができます。  
  
 カーソルが読み取り専用で、アプリケーションによってユーザーが既存の注文のみを読み取ることができる場合でも、この問題が発生します。 この場合、アプリケーションはトランザクションをコミットし、ロックが解放されるときに (自動コミットモードで)、または**SQLEndTran** (手動コミットモード)**で呼び出され**ます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [コンカレンシーの種類](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [オプティミスティック コンカレンシー](../../../odbc/reference/develop-app/optimistic-concurrency.md)
