---
description: ステートメント ハンドルの割り当て (ODBC)
title: ステートメントハンドルを割り当てる ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 624490beee55c7fa37346087fc85b560904f6b93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487545"
---
# <a name="allocating-a-statement-handle-odbc"></a>ステートメント ハンドルの割り当て (ODBC)
アプリケーションでステートメントを実行するには、ステートメントハンドルを次のように割り当てておく必要があります。  
  
1.  アプリケーションは、HSTMT 型の変数を宣言します。 次に、 **SQLAllocHandle** を呼び出し、この変数のアドレス、ステートメントを割り当てる接続のハンドル、および SQL_HANDLE_STMT オプションを渡します。 次に例を示します。  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  ドライバーマネージャーは、ステートメントに関する情報を格納する構造体を割り当て、SQL_HANDLE_STMT オプションを使用してドライバーで **SQLAllocHandle** を呼び出します。  
  
3.  ドライバーは、ステートメントに関する情報を格納する独自の構造体を割り当て、ドライバーマネージャーにドライバーのステートメントハンドルを返します。  
  
4.  ドライバーマネージャーは、アプリケーション変数内のアプリケーションに対する Driver Manager ステートメントハンドルを返します。  
  
 ステートメントハンドルは、ODBC 関数を呼び出すときに使用するステートメントを識別します。 ステートメントハンドルの詳細については、「 [ステートメントハンドル](../../../odbc/reference/develop-app/statement-handles.md)」を参照してください。
