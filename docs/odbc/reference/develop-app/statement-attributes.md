---
description: ステートメント属性
title: ステートメントの属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e2106a952bfdd7945d5d11ddde39138d0c82a14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476354"
---
# <a name="statement-attributes"></a>ステートメント属性
ステートメント属性は、ステートメントの特性です。 たとえば、ブックマークを使用するかどうか、およびステートメントの結果セットと共に使用するカーソルの種類は、ステートメント属性です。  
  
 ステートメント属性は **SQLSetStmtAttr** で設定され、その現在の設定は **SQLGetStmtAttr**で取得されます。 アプリケーションでステートメント属性を設定する必要はありません。すべてのステートメント属性には既定値があり、その一部はドライバー固有です。  
  
 ステートメント属性を設定できるかどうかは、属性自体によって異なります。 ステートメントを実行する前に、SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、および SQL_ATTR_USE_BOOKMARKS ステートメントの属性を設定する必要があります。 SQL_ATTR_ASYNC_ENABLE および SQL_ATTR_NOSCAN statement 属性はいつでも設定できますが、ステートメントが再度使用されるまでは適用されません。 SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、および SQL_ATTR_QUERY_TIMEOUT ステートメント属性はいつでも設定できますが、ステートメントを再使用する前に適用するかどうかはドライバーによって異なります。 残りのステートメント属性は、いつでも設定できます。  
  
> [!NOTE]  
>  ODBC 3 では、 **SQLSetConnectAttr** を呼び出して、接続レベルでステートメント属性を設定する機能は非推奨とされました。*x*。 ODBC 3.*x* アプリケーションでは、接続レベルでステートメント属性を設定しないでください。 ODBC 3.*x* ドライバーは ODBC 2 で動作する必要がある場合にのみ、この機能をサポートする必要があります。*x* アプリケーション。 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [SQLSetConnectOption Mapping](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 」を参照してください。  
>   
>  この例外は、SQL_ATTR_METADATA_ID 属性と SQL_ATTR_ASYNC_ENABLE 属性であり、接続属性とステートメント属性の両方であり、接続レベルまたはステートメントレベルで設定できます。  
>   
>  ODBC 3 では、どのステートメント属性も導入されていません。*x* (SQL_ATTR_METADATA_ID を除く) は、接続レベルで設定できます。  
  
 詳細については、 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 関数の説明を参照してください。
