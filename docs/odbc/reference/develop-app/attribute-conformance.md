---
description: 属性の適合性
title: 属性の準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c58dfe7f8c4219d134cd1662ce8d57b9c76de6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476904"
---
# <a name="attribute-conformance"></a>属性の適合性
次の表は、各 ODBC 環境属性の準拠レベルを示しています。これは適切に定義されています。  
  
|機能|一致レベル|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|コア|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] これはオプションの機能であるため、準拠レベルの一部ではありません。  
  
 次の表は、各 ODBC 接続属性が適切に定義されている場合の準拠レベルを示しています。  
  
|機能|一致レベル|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|コア|  
|SQL_ATTR_ASYNC_ENABLE|レベル 1/レベル 2 [1]|  
|SQL_ATTR_AUTO_IPD|[レベル 2]|  
|SQL_ATTR_AUTOCOMMIT|[レベル 1]|  
|SQL_ATTR_CONNECTION_DEAD|[レベル 1]|  
|SQL_ATTR_CONNECTION_TIMEOUT|[レベル 2]|  
|SQL_ATTR_CURRENT_CATALOG|[レベル 2]|  
|SQL_ATTR_LOGIN_TIMEOUT|[レベル 2]|  
|SQL_ATTR_ODBC_CURSORS|コア|  
|SQL_ATTR_PACKET_SIZE|[レベル 2]|  
|SQL_ATTR_QUIET_MODE|コア|  
|SQL_ATTR_TRACE|コア|  
|SQL_ATTR_TRACEFILE|コア|  
|SQL_ATTR_TRANSLATE_LIB|コア|  
|SQL_ATTR_TRANSLATE_OPTION|コア|  
|SQL_ATTR_TXN_ISOLATION|レベル 1/レベル 2 [2]|  
  
 [1] 接続レベルの非同期性 (レベル1に必要) をサポートするアプリケーションは、 **SQLSetConnectAttr**を呼び出して、この属性を SQL_TRUE に設定することをサポートしている必要があります。 **SQLSetStmtAttr**を使用して、属性を既定値以外の値に設定することはできません。 ステートメントレベルの非同期性 (レベル2に必要) をサポートするアプリケーションでは、いずれかの関数を使用して、この属性を SQL_TRUE に設定することをサポートする必要があります。  
  
 [2] レベル1のインターフェイスに準拠するには、ドライバーによって定義された既定値 (SQL_DEFAULT_TXN_ISOLATION オプションを指定して **SQLGetInfo** を呼び出すことによって使用可能) に加えて、ドライバーが1つの値をサポートしている必要があります。 レベル2のインターフェイス準拠の場合、ドライバーは SQL_TXN_SERIALIZABLE もサポートする必要があります。  
  
 次の表は、各 ODBC ステートメント属性の準拠レベルを示しています。これは適切に定義されています。  
  
|機能|一致レベル|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|コア|  
|SQL_ATTR_APP_ROW_DESC|コア|  
|SQL_ATTR_ASYNC_ENABLE|レベル 1/レベル 2 [1]|  
|SQL_ATTR_CONCURRENCY|レベル 1/レベル 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|[レベル 1]|  
|SQL_ATTR_CURSOR_SENSITIVITY|[レベル 2]|  
|SQL_ATTR_CURSOR_TYPE|コア/レベル 2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|[レベル 2]|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|[レベル 2]|  
|SQL_ATTR_IMP_PARAM_DESC|コア|  
|SQL_ATTR_IMP_ROW_DESC|コア|  
|SQL_ATTR_KEYSET_SIZE|[レベル 2]|  
|SQL_ATTR_MAX_LENGTH|[レベル 1]|  
|SQL_ATTR_MAX_ROWS|[レベル 1]|  
|SQL_ATTR_METADATA_ID|コア|  
|SQL_ATTR_NOSCAN|コア|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|コア|  
|SQL_ATTR_PARAM_BIND_TYPE|コア|  
|SQL_ATTR_PARAM_OPERATION_PTR|コア|  
|SQL_ATTR_PARAM_STATUS_PTR|コア|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|コア|  
|SQL_ATTR_PARAMSET_SIZE|コア|  
|SQL_ATTR_QUERY_TIMEOUT|[レベル 2]|  
|SQL_ATTR_RETRIEVE_DATA|[レベル 1]|  
|SQL_ATTR_ROW_ARRAY_SIZE|コア|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|コア|  
|SQL_ATTR_ROW_BIND_TYPE|コア|  
|SQL_ATTR_ROW_NUMBER|[レベル 1]|  
|SQL_ATTR_ROW_OPERATION_PTR|[レベル 1]|  
|SQL_ATTR_ROW_STATUS_PTR|コア|  
|SQL_ATTR_ROWS_FETCHED_PTR|コア|  
|SQL_ATTR_SIMULATE_CURSOR|[レベル 2]|  
|SQL_ATTR_USE_BOOKMARKS|[レベル 2]|  
  
 [1] 接続レベルの非同期性 (レベル1に必要) をサポートするアプリケーションは、 **SQLSetConnectAttr**を呼び出して、この属性を SQL_TRUE に設定することをサポートしている必要があります。 **SQLSetStmtAttr**を使用して、属性を既定値以外の値に設定することはできません。 ステートメントレベルの非同期性 (レベル2に必要) をサポートするアプリケーションでは、いずれかの関数を使用して、この属性を SQL_TRUE に設定することをサポートする必要があります。  
  
 [2] レベル2のインターフェイスに準拠するには、ドライバーが SQL_CONCUR_READ_ONLY とその他の少なくとも1つの値をサポートしている必要があります。  
  
 [3] レベル1のインターフェイスに準拠するには、ドライバーが SQL_CURSOR_FORWARD_ONLY とその他の少なくとも1つの値をサポートしている必要があります。 レベル2のインターフェイス準拠の場合、ドライバーはこのドキュメントで定義されているすべての値をサポートする必要があります。
