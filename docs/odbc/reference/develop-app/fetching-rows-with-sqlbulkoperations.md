---
description: SQLBulkOperations による行のフェッチ
title: SQLBulkOperations を使用した行のフェッチ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4c3cb6a38e3ef9c42f4e853b8c406579b5c0236
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499872"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>SQLBulkOperations による行のフェッチ
**Sqlbulkoperations**を呼び出すことにより、ブックマークを使用してデータを行セットに変換できます。 フェッチされる行は、バインドされたブックマーク列のブックマークによって識別されます。 値が SQL_COLUMN_IGNORE の列はフェッチされません。  
  
 **Sqlbulkoperations**を使用して一括フェッチを実行する場合、アプリケーションは次の処理を実行します。  
  
1.  更新するすべての行のブックマークを取得してキャッシュします。 複数のブックマークがあり、列方向のバインドが使用されている場合、ブックマークは配列に格納されます。複数のブックマークがあり、行方向のバインドが使用されている場合、ブックマークは行構造の配列に格納されます。  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性をフェッチする行数に設定し、ブックマーク値またはブックマークの配列を含むバッファーを列0にバインドします。  
  
3.  各列の長さ/インジケーターバッファーの値を必要に応じて設定します。 これは、文字列バッファーにバインドされている列のデータまたは SQL_NTS のバイト長、バイナリバッファーにバインドされた列のデータのバイト長、および NULL に設定する列の SQL_NULL_DATA です。 アプリケーションは、既定値に設定される列 (存在する場合) または NULL (存在しない場合) に設定される列の長さ/インジケーターバッファーの値を SQL_COLUMN_IGNORE に設定します。  
  
4.  *操作*引数が SQL_FETCH_BY_BOOKMARK に設定された**sqlbulkoperations**を呼び出します。  
  
 特定の列に対して操作が実行されないようにするために、アプリケーションで row 操作配列を使用する必要はありません。 アプリケーションは、バインドされたブックマーク配列にその行のブックマークのみをコピーすることによって、フェッチする行を選択します。
