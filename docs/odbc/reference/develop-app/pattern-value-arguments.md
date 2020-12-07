---
description: パターン値の引数
title: パターン値の引数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a014c63c7fff6b82bbdd26d9fd5b4391c29d0ce2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465754"
---
# <a name="pattern-value-arguments"></a>パターン値の引数
**Sqltables**の*TableName*引数など、カタログ関数の引数の中には、検索パターンを受け入れるものがあります。 SQL_ATTR_METADATA_ID statement 属性が SQL_FALSE に設定されている場合、これらの引数は検索パターンを受け取ります。この属性が SQL_TRUE に設定されている場合、検索パターンを受け入れない識別子引数です。  
  
 検索パターンの文字は次のとおりです。  
  
-   任意の1文字を表すアンダースコア (_)。  
  
-   0個以上の文字のシーケンスを表すパーセント記号 (%)。  
  
-   エスケープ文字。これはドライバー固有のものであり、アンダースコア、パーセント記号、およびエスケープ文字をリテラルとして含めるために使用されます。 エスケープ文字が特殊文字以外の文字の前にある場合、エスケープ文字は特別な意味を持ちません。 エスケープ文字が特殊文字の前にある場合は、特殊文字をエスケープします。 たとえば、"\a" は2つの文字 (" \\ " および "a") として扱わ \\ れますが、"%" は特殊な1文字 "%" として扱われます。  
  
 このエスケープ文字は、 **SQLGetInfo**の SQL_SEARCH_PATTERN_ESCAPE オプションを使用して取得されます。 検索パターンを受け取る引数内のアンダースコア、パーセント記号、またはエスケープ文字の前に、その文字をリテラルとして含める必要があります。 次の表に例を示します。  
  
|検索パターン|説明|  
|--------------------|-----------------|  
|ある|A という文字を含むすべての識別子|  
|ABC_|ABC で始まる4文字のすべての識別子|  
|ABC \\ _|エスケープ文字が円記号 () であると仮定して ABC_ 識別子 \\ 。|  
|\\\\%|円記号 () で始まるすべて \\ の識別子で、エスケープ文字が円記号であることを前提としています。|  
  
 検索パターンを受け入れる引数で検索パターン文字をエスケープするには、特別な注意が必要です。 これは、識別子でよく使用されるアンダースコア文字に特に当てはまります。 アプリケーションでよくある間違いは、1つのカタログ関数から値を取得し、その値を別のカタログ関数の検索パターン引数に渡すことです。 たとえば、アプリケーションが **Sqltables** の結果セットから MY_TABLE テーブル名を取得し、それを **sqltables** に渡して MY_TABLE 内の列の一覧を取得するとします。 MY_TABLE の列を取得する代わりに、MY_TABLE、MY1TABLE、MY2TABLE などの検索パターン MY_TABLE に一致するすべてのテーブルの列がアプリケーションによって取得されます。  
  
> [!NOTE]
>  ODBC 2.*x*ドライバーは、 **Sqltables**の*CatalogName*引数の検索パターンをサポートしていません。 SQL_ATTR_ ODBC_VERSION environment 属性が SQL_OV_ODBC3 に設定されている場合、ODBC*3.x ドライバーは* この引数の検索パターンを受け入れます。SQL_OV_ODBC2 に設定されている場合、この引数の検索パターンは受け入れられません。  
  
 検索パターン引数に null ポインターを渡すと、その引数の検索が制限されません。つまり、null ポインターと検索パターン% (任意の文字) は等価です。 ただし、長さゼロの検索パターン (長さゼロの文字列への有効なポインター) は、空の文字列 ("") にのみ一致します。
