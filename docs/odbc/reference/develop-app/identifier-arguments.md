---
description: 識別子の引数
title: 識別子の引数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24efb295c9c27dbfc5edc2b1d7a46d6ca166e2c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461454"
---
# <a name="identifier-arguments"></a>識別子の引数
識別子引数内の文字列が引用符で囲まれている場合、ドライバーは先頭および末尾の空白を削除し、文字どおり文字列を引用符で囲みます。 文字列が引用符で囲まれていない場合、ドライバーは末尾の空白を削除し、文字列を大文字にします。 Null ポインターに識別子引数を設定すると SQL_ERROR と SQLSTATE HY009 (null ポインターの使用は無効) が返されます。ただし、引数がカタログ名であり、カタログがサポートされていない場合は除きます。  
  
 これらの引数は、SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、識別子の引数として扱われます。 この場合、アンダースコア (_) とパーセント記号 (%)は、検索パターン文字としてではなく、実際の文字として扱われます。 この属性が SQL_FALSE に設定されている場合、これらの引数は引数に応じて、通常の引数またはパターン引数のいずれかとして扱われます。  
  
 特殊文字を含む識別子は、SQL ステートメントで引用符で囲む必要がありますが、カタログ関数の引数として渡すときは引用符で囲む必要があります。これは、カタログ関数に渡された引用符文字が文字どおりに解釈されるためです。 たとえば、識別子の引用符 (ドライバー固有であり、 **SQLGetInfo**を通じて返される文字) が二重引用符 (") であるとします。 **Sqltables**の最初の呼び出しでは、買掛金テーブルに関する情報を含む結果セットが返されます。2回目の呼び出しでは、"accounts 買掛" テーブルに関する情報が返されますが、これは意図したものではない可能性があります。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引用符で囲まれた識別子は、Oracle の ROWID など、同じ名前の擬似列からの真の列名を区別するために使用されます。 "ROWID" がカタログ関数の引数として渡された場合、その関数は ROWID 擬似列 (存在する場合) を使用します。 擬似列が存在しない場合、関数は "ROWID" 列を使用します。 ROWID がカタログ関数の引数で渡される場合、関数は ROWID 列を操作します。  
  
 引用符で囲まれた識別子の詳細については、「 [引用符で囲ま](../../../odbc/reference/develop-app/quoted-identifiers.md)れた識別子」をご覧ください。
