---
description: 動作の変更
title: 動作の変更 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fb5501d362cb46f3616e58c5a4994bab86e00ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461624"
---
# <a name="behavioral-changes"></a>動作の変更
動作の変更とは、インターフェイスの *構文* が変わりませんが、 *セマンティクス* が変更された変更です。 これらの変更については、ODBC 2 で使用される機能です。*x* の動作は、ODBC 3 の同じ機能とは異なります。*x*。  
  
 アプリケーションが ODBC 2 を示すかどうか。*x* 動作または ODBC 3。*x* の動作は、SQL_ATTR_ODBC_VERSION 環境属性によって決まります。 この32ビット値は SQL_OV_ODBC2 に設定され、ODBC 2 が見られます。*x* の動作と、ODBC 3 を示す SQL_OV_ODBC3 ます。*x* の動作。  
  
 SQL_ATTR_ODBC_VERSION 環境属性は、 **SQLSetEnvAttr**の呼び出しによって設定されます。 アプリケーションは、 **SQLAllocHandle** を呼び出して環境ハンドルを割り当てると、その動作を設定するために**SQLSetEnvAttr** をすぐに呼び出す必要があります。 (結果として、割り当てられたの環境ハンドルを記述する新しい環境の状態がありますが、versionless の状態になります)。詳細については、「 [付録 B: ODBC 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」を参照してください。  
  
 アプリケーションでは、SQL_ATTR_ODBC_VERSION 環境属性でどのような動作が発生しているかが示されますが、この属性は ODBC 2 とのアプリケーションの接続には影響しません。*x* または ODBC 3。*x* ドライバー。 ODBC 3.*x* アプリケーションは、ODBC 2 に接続できます。*x* または3。*x* ドライバー。環境属性の設定には関係ありません。  
  
 ODBC 3.*x* アプリケーションは **sqlallocenv**を呼び出すことはできません。 その結果、ドライバーマネージャーが **Sqlallocenv**の呼び出しを受け取ると、そのアプリケーションは ODBC 2 として認識されます。*x* アプリケーション。  
  
 SQL_ATTR_ODBC_VERSION 属性は、ODBC 3 の3つの異なる側面に影響します。*x* ドライバーの動作:  
  
-   SQLSTATE  
  
-   日付、時刻、およびタイムスタンプのデータ型  
  
-   **Sqltables**の*CatalogName*引数は、ODBC 3 の検索パターンを受け入れます。*x*(ODBC 2 ではありません)。*x*  
  
 SQL_ATTR_ODBC_VERSION 環境属性の設定は、 **SQLSetParam** または **SQLBindParam**には影響しません。 **Sqlcolattribute** はこのビットの影響も受けません。 **Sqlcolattribute**は ODBC のバージョン (日付型、有効桁数、小数点以下桁数、および長さ) の影響を受ける属性を返しますが、目的の動作は*FieldIdentifier*引数の値によって決まります。 *FieldIdentifier*が SQL_DESC_TYPE と等しい場合、 **sqlcolattribute**は ODBC 3 を返します。日付、時刻、およびタイムスタンプの*x*コード*FieldIdentifier*が SQL_COLUMN_TYPE と等しい場合、 **sqlcolattribute**は ODBC 2 を返します。日付、時刻、およびタイムスタンプの*x*コード。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLSTATE マッピング](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [datetime データ型の変更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
