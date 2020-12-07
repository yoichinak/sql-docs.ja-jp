---
description: レベル 2 インターフェイスの適合性
title: レベル2のインターフェイス準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b7148b05d3870a7f23a51167fffeb1860c26d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476564"
---
# <a name="level-2-interface-conformance"></a>レベル 2 インターフェイスの適合性
レベル2のインターフェイスの準拠レベルには、レベル1のインターフェイスの準拠レベルの機能に加え、次の機能が含まれています。  
  
|機能番号|説明|  
|-|-|  
|201|データベースのテーブルとビューには、3つの部分で構成される名前を使用します。 (詳細については、「 [レベル1のインターフェイス](../../../odbc/reference/develop-app/level-1-interface-conformance.md)への準拠」の2部構成の名前付けサポート機能101を参照してください)。|  
|202|**SQLDescribeParam**を呼び出して、動的パラメーターについて説明します。|  
|203|入力パラメーターだけでなく、出力パラメーター、入出力パラメーター、およびストアドプロシージャの結果値も使用します。|  
|204|ブックマークの取得を含むブックマークを使用します。これには、列番号0で**SQLDescribeCol**と**sqlcolattribute**を呼び出します。*Fetchorientation*引数を SQL_FETCH_BOOKMARK に設定して**sqlfetchscroll**を呼び出すことにより、ブックマークに基づいてフェッチします。また、*操作*の引数を SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK、または SQL_FETCH_BY_BOOKMARK に設定して**sqlbulkoperations**を呼び出して、ブックマーク操作による更新、削除、およびフェッチを行います。|  
|205|**Sqlcolumnprivileges**、 **SQLForeignKeys**、 **sqlcolumnprivileges**を呼び出して、データ辞書に関する詳細情報を取得します。|  
|206|SQL ステートメントの代わりに ODBC 関数を使用して、追加のデータベース操作を実行します。これには、SQL_ADD で **Sqlbulkoperations** を呼び出すか、SQL_DELETE または SQL_UPDATE を使用して **SQLSetPos** を呼び出します。 ( *LockType*引数が SQL_LOCK_EXCLUSIVE または SQL_LOCK_UNLOCK に設定された**SQLSetPos**の呼び出しのサポートは、準拠レベルの一部ではありませんが、オプションの機能です)。|  
|207|指定された個々のステートメントに対して ODBC 関数の非同期実行を有効にします。|  
|208|**Sql特徴的な列**を呼び出して、テーブルの SQL_ROWVER 行を識別する列を取得します。 (詳細については、「azure [Core インターフェイス](../../../odbc/reference/develop-app/core-interface-conformance.md)への準拠」で、 *identifiertype*引数が SQL_BEST_ROWID に設定されている**sql特殊列**のサポートを参照してください)。|  
|209|SQL_ATTR_CONCURRENCY ステートメントの属性を、SQL_CONCUR_READ_ONLY 以外の少なくとも1つの値に設定します。|  
|210|ログイン要求と SQL クエリをタイムアウトする機能 (SQL_ATTR_LOGIN_TIMEOUT と SQL_ATTR_QUERY_TIMEOUT)。|  
|211|既定の分離レベルを変更する権限。分離の "serializable" レベルでトランザクションを実行する機能。|
