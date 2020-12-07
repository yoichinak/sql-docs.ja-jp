---
description: 環境ハンドルの割り当て
title: 環境ハンドルを割り当てています |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 390d7f4248d43e6fc6cb7910be5f42cb286f37e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429454"
---
# <a name="allocating-the-environment-handle"></a>環境ハンドルの割り当て
ODBC アプリケーションの最初のタスクは、ドライバーマネージャーを読み込むことです。これがどのように行われるかは、オペレーティングシステムに依存します。 たとえば、Microsoft® Windows NT® Server/Windows 2000 Server、Windows NT Workstation/Windows 2000 Professional、または Microsoft Windows®95/98 を実行しているコンピューターでは、アプリケーションは Driver Manager ライブラリにリンクするか、または **LoadLibrary** を呼び出して DRIVER manager DLL を読み込みます。  
  
 次のタスクは、アプリケーションが他の ODBC 関数を呼び出すことができるようになる前に実行する必要があります。そのためには、ODBC 環境を初期化し、次のように環境ハンドルを割り当てます。  
  
1.  このアプリケーションでは、SQLHENV 型の変数を宣言しています。 次に、 **SQLAllocHandle** を呼び出し、この変数のアドレスと SQL_HANDLE_ENV オプションを渡します。 次に例を示します。  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  ドライバーマネージャーは、環境に関する情報を格納する構造体を割り当て、変数内の環境ハンドルを返します。  
  
 ドライバーマネージャーは、この時点では **SQLAllocHandle** を呼び出しません。これは、ドライバーが呼び出すドライバーを認識しないためです。 アプリケーションが関数を呼び出してデータソースに接続するまで、ドライバーでの **SQLAllocHandle** の呼び出しが遅延します。 詳細については、このセクションで後述する「 [接続プロセスでのドライバーマネージャーの役割](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)」を参照してください。  
  
 アプリケーションが ODBC の使用を終了すると、 **Sqlfreehandle**で環境ハンドルが解放されます。 環境を解放した後、ODBC 関数の呼び出しで環境のハンドルを使用するアプリケーションプログラミングエラーになります。この操作を行うと、未定義になりますが、致命的な結果になります。  
  
 **Sqlfreehandle**が呼び出されると、ドライバーは環境に関する情報を格納するために使用される構造体を解放します。 環境ハンドルのすべての接続ハンドルが解放されるまで、環境ハンドルに対して **Sqlfreehandle** を呼び出すことはできません。  
  
 環境ハンドルの詳細については、「 [環境ハンドル](../../../odbc/reference/develop-app/environment-handles.md)」を参照してください。
