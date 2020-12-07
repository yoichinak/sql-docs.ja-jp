---
description: '付録 D: データ型'
title: '付録 D: データ型 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77ca1ac4b4628880e6f0a87237b347aadb66584d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411488"
---
# <a name="appendix-d-data-types"></a>付録 D: データ型
ODBC では、SQL データ型と C データ型の2つのデータ型セットが定義されています。 SQL データ型は、データソースに格納されているデータのデータ型を示します。 C データ型は、アプリケーションバッファーに格納されているデータのデータ型を示します。  
  
 SQL データ型は、SQL-92 標準に従って、各 DBMS によって定義されます。 ODBC では、SQL-92 標準で指定された各 SQL データ型に対して、型識別子が定義されます。これは、ODBC 関数で引数として渡されるか、結果セットのメタデータで返される **#define** 値です。 ODBC でサポートされていない SQL 92 データ型は BIT (ODBC SQL_BIT 型の特性は異なります)、BIT_VARYING、TIME_WITH_TIMEZONE、TIMESTAMP_WITH_TIMEZONE、および NATIONAL_CHARACTER。 ドライバーは、データソース固有の SQL データ型を ODBC SQL データ型識別子およびドライバー固有の SQL データ型識別子にマップする役割を担います。 SQL データ型は、実装記述子の SQL_DESC_CONCISE_TYPE フィールドで指定します。  
  
 ODBC では、C データ型とそれに対応する ODBC 型識別子を定義します。 アプリケーションでは、 **SQLBindCol**または**SQLGetData**の呼び出しで*TargetType*引数に適切な c 型識別子を渡すことによって、結果セットデータを受け取るバッファーの c データ型を指定します。 これは、 **SQLBindParameter**の呼び出しで*ValueType*引数に適切な c 型識別子を渡すことによって、ステートメントパラメーターを含むバッファーの c 型を指定します。 C データ型は、アプリケーション記述子の [SQL_DESC_CONCISE_TYPE] フィールドで指定します。  
  
> [!NOTE]  
>  ドライバー固有の C データ型はありません。  
  
 各 SQL データ型は、ODBC C データ型に対応しています。 データソースからデータを返す前に、ドライバーはそれを指定された C データ型に変換します。 データソースにデータを送信する前に、ドライバーは指定された C データ型からデータを変換します。  
  
 この付録には、次のトピックが含まれています。  
  
-   [データ型識別子の使用](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C データ型](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [データ型識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [疑似型識別子](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [バイナリ形式でのデータ転送](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [間隔と数値データ型のガイドライン](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [グレゴリオ暦カレンダーの制限](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [列サイズ、小数点以下の桁数、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [SQL から C データ型へのデータ変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [C から SQL データ型へのデータ変換](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 ODBC データ型の詳細については、「 [odbc のデータ型](../../../odbc/reference/develop-app/data-types-in-odbc.md)」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。
