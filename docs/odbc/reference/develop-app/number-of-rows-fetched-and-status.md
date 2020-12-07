---
description: フェッチされた行の数と状態
title: フェッチされた行の数と状態 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc328aab77d6e59db258c463a7dae1554f7d4c11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429214"
---
# <a name="number-of-rows-fetched-and-status"></a>フェッチされた行の数と状態
SQL_ATTR_ROWS_FETCHED_PTR statement 属性が設定されている場合は、 **Sqlfetch** または **sqlfetchscroll**への呼び出しによってフェッチされた行の数を返すバッファーと、エラー行を指定します。 (この数値は、ステータス SQL_ROW_NO_ROWS を持たないすべての行の数です)。 **Sqlbulkoperations** または **SQLSetPos**を呼び出した後、バッファーには、関数によって実行された一括操作によって影響を受けた行数が含まれます。 SQL_ATTR_ROW_STATUS_PTR statement 属性が設定されている場合、 **Sqlfetch** または **sqlfetchscroll** は、返された各行の状態を示す *行の状態の配列* を返します。 これらのフィールドが指すバッファーは、どちらもアプリケーションによって割り当てられ、ドライバーによって設定されます。 アプリケーションでは、カーソルが閉じられるまで、これらのポインターが有効なままであることを確認する必要があります。  
  
 行の状態配列のエントリは、各行が正常にフェッチされたかどうか、最後にフェッチされてから更新、追加、または削除されたかどうか、および行のフェッチ中にエラーが発生したかどうかを指定します。 複数行の行セットの1行を取得しているときに**Sqlfetch**または**sqlfetchscroll**でエラーが発生した場合、または SQL_FETCH_BY_BOOKMARK の操作引数を持つ**sqlbulkoperation**で一括フェッチの実行中にエラーが発生した場合は、行状態配列の対応する値が SQL_ROW_ERROR に設定され、行のフェッチが続行され、SQL_SUCCESS_WITH_INFO が*Operation* エラー処理と行の状態の配列の詳細については、「 [Sqlfetch](../../../odbc/reference/syntax/sqlfetch-function.md) および [sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 関数の説明」を参照してください。
