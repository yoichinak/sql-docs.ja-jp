---
description: SQLBulkOperations を使ったブックマークによる行の更新
title: SQLBulkOperations を使用したブックマークによる行の更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9981136d546d53b131cff0d71edcdeab5b2e650c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482875"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations を使ったブックマークによる行の更新
ブックマークによって行を更新すると、 **Sqlbulkoperations** によってデータソースがテーブルの1つ以上の行を更新します。 行は、バインドされたブックマーク列のブックマークによって識別されます。 行は、バインドされた各列のアプリケーションバッファーのデータを使用して更新されます (ただし、列の長さ/インジケーターバッファーの値が SQL_COLUMN_IGNORE の場合を除きます)。 非バインド列は更新されません。  
  
 **Sqlbulkoperations**でブックマークを使用して行を更新するには、次のアプリケーションを実行します。  
  
1.  更新するすべての行のブックマークを取得してキャッシュします。 複数のブックマークがあり、列方向のバインドが使用されている場合、ブックマークは配列に格納されます。複数のブックマークがあり、行方向のバインドが使用されている場合、ブックマークは行構造の配列に格納されます。  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 属性をブックマークの数に設定し、ブックマーク値を含むバッファー、またはブックマークの配列を列0にバインドします。  
  
3.  新しいデータ値を行セットバッファーに配置します。 **Sqlbulkoperations**で長いデータを送信する方法の詳細については、「 [Long data And SQLSetPos And sqlbulkoperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)」を参照してください。  
  
4.  各列の長さ/インジケーターバッファーの値を必要に応じて設定します。 これは、文字列バッファーにバインドされている列のデータまたは SQL_NTS のバイト長、バイナリバッファーにバインドされた列のデータのバイト長、および NULL に設定する列の SQL_NULL_DATA です。  
  
5.  SQL_COLUMN_IGNORE に更新されない列の長さ/インジケーターバッファーの値を設定します。 アプリケーションでこの手順をスキップして既存のデータを再送信することはできますが、これは非効率的であり、読み取り時に切り捨てられたデータソースに値を送信するリスクです。  
  
6.  *操作*引数が SQL_UPDATE_BY_BOOKMARK に設定された**sqlbulkoperations**を呼び出します。  
  
 更新プログラムとしてデータソースに送信されるすべての行について、アプリケーションバッファーに有効な行データが含まれている必要があります。 フェッチによってアプリケーションバッファーがいっぱいになった場合、行の状態配列が保持されていて、行の状態値が SQL_ROW_DELETED、SQL_ROW_ERROR、または SQL_ROW_NOROW の場合、データソースに無効なデータが誤って送信される可能性があります。
