---
description: SQL Server の参照の例
title: SQL Server の参照の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14016832989c6fcba1dc39bc64434e72b049c18a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424564"
---
# <a name="sql-server-browsing-example"></a>SQL Server の参照の例
次の例では、 **SQLBrowseConnect** を使用して、ドライバーで使用可能な接続を SQL Server で参照する方法を示します。 まず、アプリケーションが接続ハンドルを要求します。  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 次に、アプリケーションは **SQLBrowseConnect** を呼び出し、 **sqldrivers**によって返されるドライバーの説明を使用して SQL Server ドライバーを指定します。  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 **SQLBrowseConnect**の最初の呼び出しであるため、ドライバー SQL Server マネージャーは、アプリケーションから受け取ったものと同じ引数を使用して、ドライバーの**SQLBrowseConnect**関数を呼び出します。  
  
> [!NOTE]  
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、 `Trusted_Connection=yes` 接続文字列にユーザー ID とパスワードの情報ではなくを指定する必要があります。  
  
 ドライバーは、これが **SQLBrowseConnect** の最初の呼び出しであると判断し、接続属性の2番目のレベル (サーバー、ユーザー名、パスワード、アプリケーション名、ワークステーション ID) を返します。 Server 属性では、有効なサーバー名の一覧が返されます。 **SQLBrowseConnect**からのリターンコードは SQL_NEED_DATA です。 参照結果の文字列を次に示します。  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 参照結果文字列の各キーワードの後には、コロンと等号の前に1つ以上の単語が続きます。 これらの単語は、アプリケーションがダイアログボックスを構築するために使用できるわかりやすい名前です。 **アプリ**と**wsid**キーワードの先頭にはアスタリスクが付いています。これは省略可能であることを意味します。 **SERVER**、 **UID**、および**PWD**キーワードの前にアスタリスクが付いていません。これらの値は、次の参照要求文字列で指定する必要があります。 **SERVER**キーワードの値には、 **SQLBrowseConnect**によって返されるサーバーの1つ、またはユーザーが指定した名前を使用できます。  
  
 アプリケーションは、次のように、緑のサーバーを指定し、**アプリ**と**wsid**キーワード、および各キーワードの後にユーザーフレンドリ名を省略して、 **SQLBrowseConnect**を再度呼び出します。  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 ドライバーは、緑色のサーバーへの接続を試みます。 キーワードと値のペアがないなど、致命的でないエラーが発生した場合、 **SQLBrowseConnect** は SQL_NEED_DATA を返し、エラーが発生する前と同じ状態のままになります。 アプリケーションは、 **SQLGetDiagField** または **SQLGetDiagRec** を呼び出して、エラーを特定できます。 接続に成功すると、ドライバーは SQL_NEED_DATA を返し、参照結果の文字列を返します。  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 この文字列の属性は省略可能であるため、アプリケーションは省略できます。 ただし、アプリケーションは **SQLBrowseConnect** を再度呼び出す必要があります。 アプリケーションがデータベース名と言語を省略した場合は、空の参照要求文字列を指定します。 この例では、アプリケーションは pubs データベースを選択し、 **SQLBrowseConnect** を呼び出します。このとき、 **LANGUAGE** キーワードと、 **database** キーワードの前にあるアスタリスクを省略します。  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 **DATABASE**属性はドライバーに必要な最後の接続属性であるため、参照プロセスが完了し、アプリケーションがデータソースに接続され、 **SQLBrowseConnect**が SQL_SUCCESS を返します。 また、 **SQLBrowseConnect**は、参照結果の文字列として完全な接続文字列を返します。  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 ドライバーによって返される最終的な接続文字列には、各キーワードの後にユーザーフレンドリ名が含まれていません。また、アプリケーションで指定されていない省略可能なキーワードも含まれていません。 アプリケーションでは、この文字列を **SQLDriverConnect** と共に使用して、現在の接続ハンドル (切断後) 上のデータソースに再接続したり、別の接続ハンドルのデータソースに接続したりできます。 次に例を示します。  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
