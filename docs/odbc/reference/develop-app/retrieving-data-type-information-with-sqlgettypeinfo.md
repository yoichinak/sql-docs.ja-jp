---
description: SQLGetTypeInfo によるデータ型情報の取得
title: SQLGetTypeInfo | を使用したデータ型情報の取得Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7135a6d149646c43eb93218d2ce8952930748c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476524"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo によるデータ型情報の取得
基になる SQL データ型から ODBC 型識別子へのマッピングは概数であるため、ODBC では、ドライバーがデータソース内の各 SQL データ型を完全に記述できる関数 (**SQLGetTypeInfo**) を提供しています。 この関数は、結果セットを返します。各行は、名前、型識別子、有効桁数、小数点以下桁数、null 値の許容など、1つのデータ型の特性を記述します。  
  
 一般に、この情報は、ユーザーがテーブルを作成したり変更したりできるようにする汎用アプリケーションによって使用されます。 このようなアプリケーションは、 **SQLGetTypeInfo** を呼び出してデータ型情報を取得し、その一部またはすべてをユーザーに提示します。 このようなアプリケーションでは、次の2つの点に注意する必要があります。  
  
-   複数の SQL データ型を1つの型識別子にマップできます。これにより、使用するデータ型を決定するのが困難になる場合があります。 この問題を解決するには、結果セットを型識別子で並べ替え、2番目に型識別子の定義に従って並べ替えます。 また、データソース定義データ型は、ユーザー定義データ型よりも優先されます。 たとえば、データソースが整数データ型とカウンターデータ型を定義している場合は、カウンターが自動インクリメントされる点が異なります。 また、ユーザー定義型 WHOLENUM が整数のシノニムであるとします。 これらの各型は SQL_INTEGER にマップされます。 **SQLGetTypeInfo**の結果セットでは、最初に整数が表示され、その後に WHOLENUM と then カウンターが表示されます。 WHOLENUM は、整数の後に表示されます。これは、SQL_INTEGER 型識別子の定義とより密接に一致するため、このカウンターはユーザー定義であるためです。  
  
-   ODBC では、 **CREATE TABLE** および **ALTER TABLE** ステートメントで使用するデータ型名が定義されていません。 代わりに、アプリケーションでは、 **SQLGetTypeInfo**によって返される結果セットの TYPE_NAME 列に返された名前を使用する必要があります。 その理由は、ほとんどの SQL は Dbms によって大きく異なるわけではありませんが、データ型名は大きく異なります。 ドライバーで SQL ステートメントを解析し、標準のデータ型名を DBMS 固有のデータ型名に置き換えるのではなく、ODBC では最初に DBMS 固有の名前を使用する必要があります。  
  
 **SQLGetTypeInfo**は、アプリケーションで発生する可能性のあるすべてのデータ型を必ずしも記述するわけではないことに注意してください。 特に、結果セットには、データソースによって直接サポートされていないデータ型が含まれる場合があります。 たとえば、カタログ関数によって返される結果セット内の列のデータ型は ODBC によって定義され、これらのデータ型はデータソースでサポートされない場合があります。 結果セットのデータ型の特性を確認するために、アプリケーションは **Sqlcolattribute**を呼び出します。
