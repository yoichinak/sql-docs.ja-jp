---
description: カーソルの特定とカーソルの種類
title: カーソルの特性とカーソルの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10ec9c7fc42ad20ce0a5a6d70ef4a2a692afbec3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429424"
---
# <a name="cursor-characteristics-and-cursor-type"></a>カーソルの特定とカーソルの種類
アプリケーションでは、カーソルの種類 (順方向専用、静的、キーセットドリブン、または動的) を指定する代わりに、カーソルの特性を指定できます。 これを行うには、アプリケーションは、ステートメントハンドルでカーソルを開く前に、カーソルのスクロール機能 (SQL_ATTR_CURSOR_SCROLLABLE ステートメント属性を設定して) と感度 (SQL_ATTR_CURSOR_SENSITIVITY statement 属性を設定することによって) を選択します。 次に、ドライバーは、アプリケーションが要求した特性を最も効率的に提供するカーソルの種類を選択します。  
  
 アプリケーションでステートメント属性 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_SCROLLABLE、SQL_ATTR_CURSOR_SENSITIVITY、または SQL_ATTR_CURSOR_TYPE が設定されるたびに、ドライバーは、この4つの属性のセットにある他のステートメント属性に対して必要な変更を加えて、値の一貫性を維持します。 その結果、アプリケーションがカーソルの特性を指定すると、ドライバーは、この暗黙的な選択に基づいてカーソルの種類を示す属性を変更できます。アプリケーションが型を指定すると、ドライバーは、他の属性を変更して、選択した型の特性との一貫性を保つことができます。 これらのステートメント属性の詳細については、 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 関数の説明を参照してください。  
  
 ステートメント属性を設定してカーソルの種類とカーソルの特性の両方を指定するアプリケーションでは、アプリケーションの要件を満たすドライバーで使用できる最も効率的な方法ではないカーソルを取得するリスクがあります。  
  
 ステートメント属性の暗黙的な設定は、次の規則に従う必要があることを除いて、ドライバーで定義されています。  
  
-   順方向専用カーソルはスクロールできません。 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)の SQL_ATTR_CURSOR_SCROLLABLE の定義を参照してください。  
  
-   非依存カーソルは更新できません (したがって、同時実行が読み取り専用になります)。これは、ISO SQL 標準における非依存カーソルの定義に基づいています。  
  
 その結果、次の表で説明するように、ステートメント属性の暗黙的な設定が行われます。  
  
|属性をに設定するアプリケーション|暗黙的に設定する他の属性|  
|-----------------------------------|-------------------------------------|  
|SQL_CONCUR_READ_ONLY への SQL_ATTR_CONCURRENCY|SQL_INSENSITIVE に SQL_ATTR_CURSOR_SENSITIVITY します。|  
|SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER、または SQL_CONCUR_VALUES への SQL_ATTR_CONCURRENCY|ドライバーで定義されているように、SQL_UNSPECIFIED または SQL_SENSITIVE に SQL_ATTR_CURSOR_SENSITIVITY します。 非依存カーソルは常に読み取り専用であるため、SQL_INSENSITIVE に設定することはできません。|  
|SQL_NONSCROLLABLE への SQL_ATTR_CURSOR_SCROLLABLE|SQL_CURSOR_FORWARD_ONLY への SQL_ATTR_CURSOR_TYPE|  
|SQL_SCROLLABLE への SQL_ATTR_CURSOR_SCROLLABLE|ドライバーで指定されているように、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN、または SQL_CURSOR_DYNAMIC に SQL_ATTR_CURSOR_TYPE します。 SQL_CURSOR_FORWARD_ONLY には設定されません。|  
|SQL_INSENSITIVE への SQL_ATTR_CURSOR_SENSITIVITY|SQL_CONCUR_READ_ONLY に SQL_ATTR_CONCURRENCY します。<br /><br /> SQL_CURSOR_STATIC に SQL_ATTR_CURSOR_TYPE します。|  
|SQL_SENSITIVE への SQL_ATTR_CURSOR_SENSITIVITY|ドライバーで指定されているように、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER、または SQL_CONCUR_VALUES に SQL_ATTR_CONCURRENCY します。 SQL_CONCUR_READ_ONLY には設定されません。<br /><br /> ドライバーで指定されているように、SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN、または SQL_CURSOR_DYNAMIC に SQL_ATTR_CURSOR_TYPE します。|  
|SQL_UNSPECIFIED への SQL_ATTR_CURSOR_SENSITIVITY|ドライバーで指定されているように、SQL_CONCUR_READ_ONLY、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER、または SQL_CONCUR_VALUES に SQL_ATTR_CONCURRENCY します。<br /><br /> ドライバーで指定されているように、SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN、または SQL_CURSOR_DYNAMIC に SQL_ATTR_CURSOR_TYPE します。|  
|SQL_CURSOR_DYNAMIC への SQL_ATTR_CURSOR_TYPE|SQL_SCROLLABLE に SQL_ATTR_SCROLLABLE します。<br /><br /> SQL_SENSITIVE に SQL_ATTR_CURSOR_SENSITIVITY します。 (ただし、SQL_ATTR_CONCURRENCY が SQL_CONCUR_READ_ONLY と等しくない場合に限ります。 更新可能な動的カーソルは、独自のトランザクションで行われた変更に対して常に機微です)。|  
|SQL_CURSOR_FORWARD_ONLY への SQL_ATTR_CURSOR_TYPE|SQL_NONSCROLLABLE に SQL_ATTR_CURSOR_SCROLLABLE します。|  
|SQL_CURSOR_KEYSET_DRIVEN への SQL_ATTR_CURSOR_TYPE|SQL_SCROLLABLE に SQL_ATTR_SCROLLABLE します。<br /><br /> ドライバーで定義された条件に従って SQL_UNSPECIFIED または SQL_SENSITIVE に SQL_ATTR_SENSITIVITY (SQL_ATTR_CONCURRENCY が SQL_CONCUR_READ_ONLY ない場合)。|  
|SQL_CURSOR_STATIC への SQL_ATTR_CURSOR_TYPE|SQL_SCROLLABLE に SQL_ATTR_SCROLLABLE します。<br /><br /> SQL_INSENSITIVE に SQL_ATTR_SENSITIVITY ます (SQL_ATTR_CONCURRENCY が SQL_CONCUR_READ_ONLY の場合)。<br /><br /> SQL_UNSPECIFIED または SQL_SENSITIVE に SQL_ATTR_SENSITIVITY ます (SQL_ATTR_CONCURRENCY が SQL_CONCUR_READ_ONLY ない場合)。|
