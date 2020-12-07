---
description: '付録 E: スカラー関数'
title: '付録 E: スカラー関数 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a814de22df4a97e3c3b3abd0ddc30266fe02a30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411438"
---
# <a name="appendix-e-scalar-functions"></a>付録 E: スカラー関数
ODBC では、次の種類のスカラー関数を指定します。これらの関数の各型については、この付録の対応するセクションで説明しています。 関数の説明には、関連する構文が含まれます。  
  
 この付録には、次のトピックが含まれています。  
  
-   [文字列関数](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [数値関数](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時刻、日付、および間隔を扱う関数](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [システム関数](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [データ型の明示的な変換用関数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 関数](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC では、スカラー関数からの戻り値のデータ型は必須ではありません。これは、関数がデータソース固有のものであることが多いためです。 アプリケーションでは、可能な限り、データ型の変換を強制するために、スカラーの変換関数を使用する必要があります。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC および SQL-92 スカラー関数  
 この付録の表には、SQL-92 に合わせて ODBC 3.0 に追加された関数が含まれています。 ODBC で定義されているように、特定の種類のスカラー関数に追加された関数は、各セクションに示されています。  
  
 ODBC と SQL-92 では、スカラー関数が異なる方法で分類されます。 ODBC は、スカラー関数を引数の型で分類します。SQL-92 では、戻り値によって分類されます。 たとえば、extract 関数は、ODBC によって timedate 関数として分類されます。これは、抽出フィールドの引数が datetime キーワードで、extract source 引数が datetime または interval 式であるためです。 一方、SQL-92 では、戻り値が数値であるため、抽出は数値スカラー関数として分類されます。  
  
 アプリケーションでは、 **SQLGetInfo**を呼び出すことによって、ドライバーがサポートするスカラー関数を特定できます。 情報の種類は、ODBC と、スカラー関数の SQL-92 の分類の両方に含まれています。 これらの分類は異なるため、一部のスカラー関数のサポートは、ODBC および SQL-92 に対応しない情報の種類で示される場合があります。 たとえば、ODBC での抽出のサポートは、SQL_TIMEDATE_FUNCTIONS 情報の種類によって示されます。一方、SQL-92 での抽出のサポートは、SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 情報型によって示されます。
