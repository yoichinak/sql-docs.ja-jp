---
description: ODBC 動的カーソル
title: ODBC 動的カーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19ae15a211329e07fdab13a5b6ff40e210e97cb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429194"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 動的カーソル
動的カーソルは、次のような動的カーソルです。 カーソルを開いた後に、結果セットのメンバーシップ、順序、および値に対して行われたすべての変更を検出できます。 たとえば、動的カーソルで 2 つの行がフェッチされた後、別のアプリケーションによって一方の行は更新され、他の行は削除されたものとします。 その後、動的カーソルによってこれらの行の再フェッチが試行されても、削除された行は見つかりませんが、更新された行の新しい値が返されます。  
  
 動的カーソルは、すべての更新、削除、および挿入を、独自のものと他のユーザーが行ったものの両方を検出します。 (これは、SQL_ATTR_TXN_ISOLATION 接続属性によって設定されるトランザクションの分離レベルに従います)。SQL_ATTR_ROW_STATUS_PTR statement 属性によって指定された行の状態の配列は、これらの変更を反映し、SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED、および SQL_ROW_ADDED を含むことができます。 動的カーソルは行セットの外部で削除された行を返さないため、SQL_ROW_DELETED を返すことはできません。したがって、結果セット内の削除された行または行の状態配列内の対応する要素が存在するかどうかを認識できなくなります。 SQL_ROW_ADDED は、別のカーソルによって更新されたときではなく、 **SQLSetPos**の呼び出しによって行が更新された場合にのみ返されます。  
  
 データベースに動的カーソルを実装する方法の1つとして、結果セットのメンバーシップと順序を定義する選択的インデックスを作成する方法があります。 他のユーザーが変更を行ったときにインデックスが更新されるため、このようなインデックスに基づくカーソルはすべての変更に影響を受けます。 このインデックスによって定義された結果セット内のその他の選択は、インデックスに従って処理することによって可能になります。  
  
 動的カーソルをシミュレートするには、一意のキーで結果セットを並べ替える必要があります。 このような制限があると、カーソルが行をフェッチするたびに **select** ステートメントを実行することでフェッチが行われます。 たとえば、次のステートメントで結果セットが定義されているとします。  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 この結果セットの次の行セットをフェッチするために、シミュレートされたカーソルは、次の **select** ステートメントのパラメーターを現在の行セットの最後の行の値に設定し、それを実行します。  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 このステートメントは2番目の結果セットを作成します。最初の行セットは、元の結果セットの次の行セット (この場合は Customers テーブル内の行のセット) です。 カーソルがこの行セットをアプリケーションに返します。  
  
 この方法で実装された動的カーソルは、実際には多数の結果セットを作成するため、元の結果セットに対する変更を検出することができます。 アプリケーションでは、これらの補助結果セットの存在について学習することはありません。単に、カーソルが元の結果セットに対する変更を検出できるかのように表示されます。
