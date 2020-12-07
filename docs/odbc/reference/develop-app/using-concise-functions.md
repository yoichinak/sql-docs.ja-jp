---
description: 簡潔な関数の使用
title: 簡潔な関数を使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0dcd16c1380c95921d5e4bb58831e2dd939ecf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482798"
---
# <a name="using-concise-functions"></a>簡潔な関数の使用
一部の ODBC 関数は、記述子への暗黙的なアクセスを取得します。 アプリケーションの作成者は、 **SQLSetDescField** または **SQLGetDescField**を呼び出すよりも便利です。 これらの関数は、記述子フィールドの設定や取得など、さまざまな関数を実行するため、 *簡潔* な関数と呼ばれます。 一部の簡潔な関数は、アプリケーションが1つの関数呼び出しで複数の関連する記述子フィールドを設定または取得できるようにします。  
  
 引数として使用するために最初に記述子ハンドルを取得せずに、簡潔な関数を呼び出すことができます。 これらの関数は、呼び出されるステートメントハンドルに関連付けられた記述子フィールドを操作します。  
  
 簡潔な関数 **SQLBindCol** と **SQLBindParameter** は、その引数に対応する記述子フィールドを設定することによって、列またはパラメーターをバインドします。 これらの各関数は、単に記述子を設定するよりも多くのタスクを実行します。 **SQLBindCol** と **SQLBindParameter** は、データ列または動的パラメーターのバインドの完全な仕様を提供します。 ただし、アプリケーションでは、 **SQLSetDescField** または **SQLSetDescRec** を呼び出すことによって、バインディングの個々の詳細を変更できます。また、これらの関数に対して一連の適切な呼び出しを行うことによって、列またはパラメーターを完全にバインドできます。  
  
 簡潔な関数 **Sqlcolattribute**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **Sqlcolattribute**、および **sqlnumresultcols** は、記述子フィールドの値を取得します。  
  
 **SQLSetDescRec** と **Sqlgetdescrec** は、1回の呼び出しで、データ型と列またはパラメーターデータの格納に影響を与える複数の記述子フィールドを設定または取得する、簡潔な関数です。 **SQLSetDescRec** は、1つのステップでの列またはパラメーターデータのバインドを変更する効果的な方法です。  
  
 **SQLSetStmtAttr** と **SQLGetStmtAttr** は、場合によっては簡潔な関数として機能します。 (「 [記述子フィールド](../../../odbc/reference/develop-app/descriptor-fields.md)」を参照してください)。
