---
description: データの概要の更新
title: データの更新の概要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b1755ea75426030a96ed7b349cc82f0fc7e282a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424424"
---
# <a name="updating-data-overview"></a>データの概要の更新
アプリケーションでは、SQL ステートメントを実行するか、 **SQLSetPos** または **sqlbulkoperations**を呼び出すことによって、データを更新できます。 **UPDATE**、 **DELETE**、および **INSERT** ステートメントは、データソース上で直接動作し、通常はドライバーによってサポートされます。 検索される update ステートメントと delete ステートメントには、変更する行の指定が含まれています。 位置指定の update および delete ステートメントと **SQLSetPos** は、カーソルを介してデータソースに対して動作し、広くサポートされていません。  
  
 このセクションで説明するメソッドを使用して、カーソルが結果セットに加えられた変更を検出できるかどうかは、カーソルの種類と実装方法によって異なります。 順方向専用カーソルは行を再確認しないため、変更は検出されません。 スクロール可能なカーソルが変更を検出できるかどうかについては、「スクロール可能な [カーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)」を参照してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [UPDATE、DELETE、INSERT ステートメント](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [位置指定の UPDATE および DELETE ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [位置指定の UPDATE および DELETE ステートメントのシミュレート](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [影響を受ける行数の決定](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [SQLSetPos によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [SQLBulkOperations によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
