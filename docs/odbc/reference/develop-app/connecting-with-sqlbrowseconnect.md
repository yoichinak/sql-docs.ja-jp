---
description: SQLBrowseConnect による接続
title: SQLBrowseConnect | を使用した接続Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7ad54276f54155c68fbdbe984642dda4300a7c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424824"
---
# <a name="connecting-with-sqlbrowseconnect"></a>SQLBrowseConnect による接続
**SQLBrowseConnect**は、 **SQLDriverConnect**のように、接続文字列を使用します。 ただし、 **SQLBrowseConnect**を使用すると、アプリケーションは実行時に完全な接続文字列を作成できます。 この方法を使用すると、アプリケーションで次の 2 つのことを行えます。  
  
-   この情報を確認するための独自のダイアログボックスを構築し、その結果、"ルックアンドフィール" の制御を維持します。  
  
-   特定のドライバーが使用できるデータ ソースをシステムから参照できます。これは複数の手順になる場合があります。 たとえば、ユーザーは最初にネットワークを介してサーバーを参照して、サーバーを選択します。次に、そのサーバーを介して、ドライバーがアクセスできるデータベースを参照するといった手順です。  
  
 アプリケーションは **SQLBrowseConnect** を呼び出し、ドライバーまたはデータソースを指定する接続文字列 ( *参照要求の接続文字列* ) を渡します。 このドライバーは、 *参照結果の接続文字列* と呼ばれる接続文字列を返します。この文字列には、キーワード、有効な値 (キーワードが個別の値のセットを受け入れる場合)、およびユーザーフレンドリ名が含まれています。 アプリケーションは、ユーザーフレンドリ名を使用してダイアログボックスを構築し、ユーザーに値の入力を求めます。 次に、これらの値から新しい参照要求接続文字列を作成し、 **SQLBrowseConnect**への別の呼び出しを使用してこれをドライバーに返します。  
  
 接続文字列がやり取りされるため、ドライバーは、アプリケーションが古い接続文字列を返したときに新しい接続文字列を返すことによって、さまざまなレベルの参照を提供できます。 たとえば、アプリケーションが最初に **SQLBrowseConnect**を呼び出すときに、ドライバーは、ユーザーにサーバー名の入力を求めるキーワードを返すことがあります。 アプリケーションからサーバー名が返された場合、ドライバーは、ユーザーにデータベースの入力を求めるキーワードを返すことがあります。 アプリケーションがデータベース名を返した後、参照プロセスが完了します。  
  
 **SQLBrowseConnect**が新しい参照結果の接続文字列を返すたびに、リターンコードとして SQL_NEED_DATA が返されます。 これにより、接続プロセスが完了していないことがアプリケーションに通知されます。 **SQLBrowseConnect**が SQL_SUCCESS を返すまでは、接続はデータ状態が必要であり、接続属性を設定するなど、他の目的には使用できません。 アプリケーションは、 **Sqldisconnect**を呼び出すことによって、接続の参照プロセスを終了できます。  
  
 ここでは、次のトピックについて説明します。  
  
-   [SQL Server の参照の例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
