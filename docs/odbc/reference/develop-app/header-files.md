---
description: ヘッダー ファイル
title: ヘッダーファイル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec8eede80f88f10e0b1ca43696e75dddec121ffe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476654"
---
# <a name="header-files"></a>ヘッダー ファイル
Sql .h ヘッダーファイルには、コア ODBC インターフェイス準拠レベルの関数と機能のプロトタイプが含まれています。 Sqlext .h ヘッダーファイルには、レベル1およびレベル2の API 準拠レベルの関数と機能のプロトタイプが含まれています。 Sqltypes ヘッダーファイルには、SQL データ型の型定義とインジケーターが含まれています。  
  
 ヘッダーファイルにはすべて、アプリケーションまたはドライバーがさまざまなバージョンの ODBC 用にコンパイルされるように設定できる **#define**odbcver が含まれています。  
  
 ISO CLI を使用してグループ CLI を開くと、ヘッダーファイルには **SQLGetInfo**の呼び出しで使用される情報の種類のエイリアスが含まれます。 次の表では、"ODBC name" 列は [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)の情報の種類の odbc 名を示しています。 列 "ヘッダーファイル内の別名" は、ISO CLI および Open Group CLI で使用される名前を示します。 これらのマニフェスト名の実際の数値は、ODBC と標準 Cli の両方で同じです。 これらのエイリアスを使用すると、標準に準拠しているアプリケーションまたはドライバーが ODBC *3. x* ヘッダーファイルでコンパイルできるようになります。  
  
 これらのエイリアスには、名前がわかりやすくなるように、ODBC 名の省略形が含まれています。 "MAX" は "MAXIMUM"、"LEN" から "LENGTH"、"MULT" から "MULTIPLE"、"OJ"、"OUTER_JOIN" に、"TXN" を "TRANSACTION" に展開します。  
  
|ODBC 名|ヘッダーファイル内の別名|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
