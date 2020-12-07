---
description: ブックマークの種類
title: ブックマークの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e85d50a5fe3c21707a78ac2572d8a96166745319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476814"
---
# <a name="bookmark-types"></a>ブックマークの種類
ODBC *3. x* のすべてのブックマークは、可変長のブックマークです。 これにより、テーブルに関連付けられている主キーまたは一意のインデックスをブックマークとして使用できます。 ブックマークは *、ODBC 2.x*で使用されていた32ビット値にすることもできます。 ブックマークをカーソルと共に使用するように指定するには、ODBC *3. x* アプリケーションで、SQL_ATTR_USE_BOOKMARK statement 属性を SQL_UB_VARIABLE に設定します。 可変長のブックマークが自動的に使用されます。  
  
 アプリケーションで **Sqlcolattribute** を呼び出して、 *FieldIdentifier* 引数を SQL_DESC_OCTET_LENGTH に設定すると、ブックマークの長さを取得できます。 可変長のブックマークは long 型の値になる可能性があるため、行セット内の多くの行にブックマークを使用する場合を除き、アプリケーションは列0にバインドしないでください。  
  
 固定長のブックマークは、旧バージョンとの互換性のためにのみサポートされています。 *Odbc 2.x アプリケーションが*odbc *3. x*を使用して SQL_USE_BOOKMARKS を SQL_UB_ON に**設定して**いる場合は、ドライバーマネージャーで SQL_UB_VARIABLE にマップされます。 長さが32ビットだけが設定されている場合でも、可変長のブックマークが使用されます。 ドライバーで固定長のブックマークがサポートされている場合は、可変長のブックマークがサポートされます。 *Odbc 2.x アプリケーションが*odbc *2.x ドライバーを*使用して作業している場合に SQL_ATTR_USE_BOOKMARKS を SQL_UB_VARIABLE に設定するために**SQLSetStmtAttr**を呼び出すと、ドライバーマネージャーで SQL_UB_ON にマップされ、32ビットの固定長ブックマークが使用されます。 SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性は、32ビットのブックマークをポイントする必要があります。 使用するブックマークが32ビットを超えている場合 (主キーをブックマークとして使用する場合など)、カーソルは実際の値を32ビット値にマップする必要があります。 たとえば、ハッシュテーブルを作成することもできます。 *Odbc 2.x アプリケーションで*odbc 2.x ドライバーを使用してブックマークをバインドする場合、バッファーの長さは4である必要が*あります。*
