---
description: 影響を受ける行数の決定
title: 影響を受ける行の数を確認する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14114700c4d79f83f0388509056dd0b49bb21a8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483075"
---
# <a name="determining-the-number-of-affected-rows"></a>影響を受ける行数の決定
アプリケーションによって行の更新、削除、または挿入が行われた後、 **SQLRowCount** を呼び出して、影響を受けた行数を調べることができます。 **SQLRowCount** は、 **update**、 **delete**、または **INSERT** ステートメントの実行、位置指定の update または delete ステートメントの実行、または **SQLSetPos**を呼び出すことによって、行が更新、削除、または挿入されたかどうかにかかわらず、この値を返します。  
  
 SQL ステートメントのバッチが実行されると、影響を受ける行の数は、バッチ内のすべてのステートメントまたはバッチ内の各ステートメントの個別のカウントの合計数になります。 詳細については、「SQL ステートメントと[複数の結果](../../../odbc/reference/develop-app/multiple-results.md)[のバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)」を参照してください。  
  
 影響を受ける行の数は、ステートメントハンドルに関連付けられている診断領域の SQL_DIAG_ROW_COUNT 診断ヘッダーフィールドにも返されます。 ただし、このフィールドのデータは、同じステートメントハンドルのすべての関数呼び出しの後にリセットされます。一方、 **SQLRowCount** によって返される値は、 **sqlbulkoperations**、 **sqlexecute**、 **SQLExecDirect**、 **SQLPrepare**、または **SQLSetPos**の呼び出しまで同じままです。
