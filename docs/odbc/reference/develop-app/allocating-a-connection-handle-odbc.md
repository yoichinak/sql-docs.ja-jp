---
description: 接続ハンドルの割り当て (ODBC)
title: 接続ハンドルの割り当て ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6c17003ed3746f2953eb167f2dc3d944659e352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456438"
---
# <a name="allocating-a-connection-handle-odbc"></a>接続ハンドルの割り当て (ODBC)
アプリケーションでデータソースまたはドライバーに接続するには、次のように接続ハンドルを割り当てる必要があります。  
  
1.  アプリケーションは、SQLHDBC 型の変数を宣言します。 次に、 **SQLAllocHandle** を呼び出し、この変数のアドレス、接続を割り当てる環境のハンドル、および SQL_HANDLE_DBC オプションを渡します。 次に例を示します。  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  ドライバーマネージャーは、ステートメントに関する情報を格納する構造体を割り当て、変数内の接続ハンドルを返します。  
  
 ドライバーマネージャーは、この時点では **SQLAllocHandle** を呼び出しません。これは、ドライバーが呼び出すドライバーを認識しないためです。 アプリケーションが関数を呼び出してデータソースに接続するまで、ドライバーでの **SQLAllocHandle** の呼び出しが遅延します。 詳細については、このセクションで後述する「 [接続プロセスでのドライバーマネージャーの役割](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)」を参照してください。  
  
 接続ハンドルの割り当ては、ドライバーの読み込みと同じではないことに注意してください。 ドライバーは、接続関数が呼び出されるまで読み込まれません。 このため、接続ハンドルを割り当て、ドライバーまたはデータソースに接続する前に、アプリケーションが接続ハンドルを使用して呼び出すことができる関数は、 **SQLSetConnectAttr**、 **sqlgetconnectattr**、または **SQLGetInfo** (SQL_ODBC_VER オプションを指定した場合) のみです。 **SQLEndTran**などの接続ハンドルを使用して他の関数を呼び出すと、SQLSTATE 08003 (接続が開かれていません) が返されます。 詳細については、「 [付録 B: ODBC 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」を参照してください。  
  
 接続ハンドルの詳細については、「 [接続ハンドル](../../../odbc/reference/develop-app/connection-handles.md)」を参照してください。
