---
description: SQLBulkOperations を使ったブックマークによる行の削除
title: SQLBulkOperations を使用したブックマークによる行の削除 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dcb96180cdcee5987d8a1cbafeae117ec82bba0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424684"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations を使ったブックマークによる行の削除
ブックマークを使用して行を削除すると、 **Sqlbulkoperations** によって、テーブルの選択した1つ以上の行がデータソースによって削除されます。 行は、バインドされたブックマーク列のブックマークによって識別されます。  
  
 **Sqlbulkoperations**でブックマークを使用して行を削除する場合、アプリケーションは次の処理を実行します。  
  
1.  削除するすべての行のブックマークを取得してキャッシュします。 複数のブックマークがあり、列方向のバインドが使用されている場合、ブックマークは配列に格納されます。複数のブックマークがあり、行方向のバインドが使用されている場合、ブックマークは行構造の配列に格納されます。  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性をブックマークの数に設定し、ブックマーク値を含むバッファー、またはブックマークの配列を列0にバインドします。  
  
3.  *操作*が SQL_DELETE_BY_BOOKMARK に設定された**sqlbulkoperations**を呼び出します。
