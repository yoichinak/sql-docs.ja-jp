---
description: SQLStatistics (Access ドライバー)
title: SQLStatistics (Access Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67ea4e7f2553d85837c1ece30327f24298d94c97
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421586"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Access ドライバー)
> [!NOTE]  
>  このトピックでは、ドライバー固有の情報にアクセスします。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
|列|コメント|  
|------------|--------------|  
|TABLE_QUALIFIER|Microsoft Access では、データベースファイルへのパスが返されます。<br /><br /> パターンマッチングは、 *Sztablequalifier* 引数ではサポートされていません。|  
|TABLE_OWNER|所有者名がサポートされていないため、この列には NULL が返されます。|  
|TABLE_NAME|区切られていないテーブル名です。<br /><br /> パターンマッチングは、 *Sztablename* 引数ではサポートされていません。|  
|INDEX_QUALIFIER|常に NULL が返されます。|  
|INDEX_NAME|インデックスに依存します。|  
|TYPE|型に対しては、SQL_TABLE_STAT または SQL_INDEX_OTHER のみが返されます。|  
|SEQ_IN_INDEX|インデックスに依存します。|  
|COLUMN_NAME|インデックスに依存します。|  
|COLLATION|インデックスに依存します。|  
|CARDINALITY|Microsoft アクセスのみに対して返されます。|  
|PAGES|常に NULL が返されます。|  
  
 フィルター処理は、一意性 ( *Funique* 引数) に基づいています。 *FAccuracy*パラメーターは無視されます。
