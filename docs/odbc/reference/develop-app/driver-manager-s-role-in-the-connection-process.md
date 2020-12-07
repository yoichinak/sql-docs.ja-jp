---
description: 接続プロセスの Driver Manager&#39;s ロール
title: 接続プロセスの Driver Manager&#39;s ロール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fb4eea978604960d87ef6c5b621e5801121c5f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483045"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>接続プロセスの Driver Manager&#39;s ロール
アプリケーションがドライバー関数を直接呼び出すことはないことに注意してください。 代わりに、同じ名前でドライバーマネージャーの関数を呼び出し、ドライバーマネージャーがドライバーの機能を呼び出します。 通常、これはほぼ即座に発生します。 たとえば、アプリケーションがドライバーマネージャーで **Sqlexecute** を呼び出し、いくつかのエラーチェックが行われた後、ドライバーマネージャーがドライバーで **sqlexecute** を呼び出します。  
  
 接続プロセスが異なります。 アプリケーションが SQL_HANDLE_ENV および SQL_HANDLE_DBC オプションを使用して **SQLAllocHandle** を呼び出すと、関数はドライバーマネージャーでのみハンドルを割り当てます。 ドライバーマネージャーは、呼び出すドライバーが認識されないため、ドライバーでこの関数を呼び出しません。 同様に、アプリケーションが接続されていない接続のハンドルを **SQLSetConnectAttr** または **Sqlgetconnectattr**に渡す場合は、ドライバーマネージャーだけが関数を実行します。 このメソッドは、接続ハンドルから属性値を格納または取得し、設定されていない属性の値を取得するときに SQLSTATE 08003 (接続が開かれていません) を返します。 ODBC では既定値が定義されていません。  
  
 アプリケーションが **SQLConnect**、 **SQLDriverConnect**、または **SQLBrowseConnect**を呼び出すと、ドライバーマネージャーはまず、使用するドライバーを決定します。 次に、ドライバーが現在接続に読み込まれているかどうかを確認します。  
  
-   ドライバーが接続に読み込まれていない場合、ドライバーマネージャーは、指定されたドライバーが同じ環境内の別の接続に読み込まれているかどうかを確認します。 それ以外の場合は、ドライバーマネージャーが接続にドライバーを読み込み、SQL_HANDLE_ENV オプションを使用してドライバーで **SQLAllocHandle** を呼び出します。  
  
     ドライバーマネージャーは、ドライバーが読み込まれたかどうかにかかわらず、SQL_HANDLE_DBC オプションを使用してドライバーで **SQLAllocHandle** を呼び出します。 アプリケーションで接続属性が設定されている場合、ドライバーマネージャーはドライバーで **SQLSetConnectAttr** を呼び出します。エラーが発生した場合、ドライバーマネージャーの接続関数は SQLSTATE IM006 (ドライバーの **SQLSetConnectAttr** failed) を返します。 最後に、ドライバーマネージャーは、ドライバーの接続関数を呼び出します。  
  
-   指定されたドライバーが接続に読み込まれた場合、ドライバーマネージャーはドライバー内の接続関数だけを呼び出します。 この場合、ドライバーは、接続のすべての接続属性が現在の設定を維持していることを確認する必要があります。  
  
-   接続に別のドライバーが読み込まれている場合、ドライバーマネージャーはドライバーで **Sqlfreehandle** を呼び出して接続を解放します。 ドライバーを使用する他の接続がない場合は、ドライバーマネージャーがドライバーの **Sqlfreehandle** を呼び出して、環境を解放し、ドライバーをアンロードします。 ドライバーマネージャーは、接続時にドライバーが読み込まれていない場合と同じ操作を実行します。  
  
 *Handletype*が**SQL_HANDLE_DBC**に設定されている場合、ドライバーマネージャーは、ドライバー**の SQLAllocHandle**と**sqlfreehandle**を呼び出す前に、環境ハンドル (*henv*) をロックします。  
  
 アプリケーションが **sqldisconnect**を呼び出すと、ドライバーマネージャーはドライバーで **sqldisconnect** を呼び出します。 ただし、アプリケーションがドライバーに再接続した場合に備えて、ドライバーは読み込まれたままになります。 アプリケーションが SQL_HANDLE_DBC オプションを使用して **Sqlfreehandle** を呼び出すと、ドライバーマネージャーはドライバーで **sqlfreehandle** を呼び出します。 ドライバーが他のどの接続でも使用されていない場合は、ドライバーマネージャーが SQL_HANDLE_ENV オプションを使用してドライバーの **Sqlfreehandle** を呼び出し、ドライバーをアンロードします。
