---
description: 標準に準拠したアプリケーションとドライバー
title: 標準に準拠したアプリケーションとドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6733afa5281f86d8dd425e6157832ee0680d34b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476384"
---
# <a name="standards-compliant-applications-and-drivers"></a>標準に準拠したアプリケーションとドライバー
標準に準拠しているアプリケーションまたはドライバーは、Open Group CAE Specification "データ管理: SQL 呼び出しレベルインターフェイス (CLI)、および ISO/IEC 9075-3:1995 (E) の呼び出しレベルインターフェイス (SQL/CLI) に準拠しています。  
  
 ODBC *3. x* では、次の機能が保証されます。  
  
-   Open Group および ISO CLI 仕様に書き込まれるアプリケーションは、odbc *3.x ドライバーまた* は標準に準拠しているドライバーを使用してコンパイルされ、odbc *3. x ヘッダーファイル* を使用してコンパイルされ、odbc *3* . x ライブラリにリンクされている場合は *、odbc 3.x ドライバーマネージャー* を使用してドライバーへのアクセスを取得します。  
  
-   Open Group および ISO CLI 仕様に書き込まれるドライバーは *、odbc 3.x アプリケーションまた* は標準に準拠しているアプリケーションで動作します。 odbc *3. x ヘッダーファイル* を使用してコンパイルし、odbc *3* . x ライブラリにリンクし、アプリケーションが odbc *3. x* ドライバーマネージャーを使用してドライバーへのアクセスを取得したときに使用します。  
  
 標準に準拠しているアプリケーションとドライバーは、ODBC_STD compile フラグを使用してコンパイルされます。  
  
 標準に準拠しているアプリケーションでは、次の動作が発生します。  
  
-   標準に準拠しているアプリケーションが **Sqlallocenv** を呼び出す場合 ( **Sqlallocenv** が OPEN Group と ISO CLI の有効な関数であるために発生する可能性があります)、呼び出しはコンパイル時に **SQLAllocHandleStd** にマップされます。 その結果、実行時に、アプリケーションは **SQLAllocHandleStd**を呼び出します。 この呼び出しを処理する過程で、Driver Manager は SQL_ATTR_ODBC_VERSION environment 属性を SQL_OV_ODBC3 に設定します。 **SQLAllocHandleStd**の呼び出しは、 *handletype*が SQL_HANDLE_ENV で**SQLAllocHandle**を呼び出す場合と同じです。また、 **SQLSetEnvAttr**を SQL_OV_ODBC3 に設定する場合は、SQL_ATTR_ODBC_VERSION を呼び出します。  
  
-   標準に準拠しているアプリケーションが **SQLBindParam** を呼び出す場合 ( **SQLBindParam** が OPEN Group と ISO CLI の有効な関数であるために発生する可能性があります)、ODBC *3. x* ドライバーマネージャーは、呼び出しを **SQLBindParameter**の同等の呼び出しにマップします。 (「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [SQLBindParam Mapping](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) 」を参照してください)。  
  
-   ISO CLI に合わせるために、ODBC *3 .x* ヘッダーファイルには、 **SQLGetInfo**の呼び出しで使用される情報の種類のエイリアスが含まれています。 標準に準拠しているアプリケーションでは、ODBC *3. x* 情報の種類ではなく、これらのエイリアスを使用できます。 詳細については、次のトピック「 [ヘッダーファイル](../../../odbc/reference/develop-app/header-files.md)」を参照してください。  
  
-   標準に準拠しているアプリケーションでは、サポートしているすべての機能が、使用するドライバーでサポートされていることを確認する必要があります。 SQL_ATTR_CURSOR_SCROLLABLE statement 属性を SQL_SCROLLABLE に設定し、SQL_ATTR_CURSOR_SENSITIVITY statement 属性を SQL_INSENSITIVE または SQL_SENSITIVE に設定する機能は、標準のオプション機能としては使用できますが、ODBC 3.x *のコアレベル* には含まれないため、すべての odbc *3.x ドライバーで* サポートされていない可能性があります。 標準に準拠しているアプリケーションでこれらの機能を使用する場合は、それが動作するドライバーがサポートしているかどうかを確認する必要があります。
