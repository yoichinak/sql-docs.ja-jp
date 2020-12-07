---
description: 接続情報をユーザーに確認する
title: ユーザーに接続情報の入力を求める |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f52e0d120fb150fe58b850107847d7ef5df20e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465714"
---
# <a name="prompting-the-user-for-connection-information"></a>接続情報をユーザーに確認する
アプリケーションが **SQLConnect** を使用していて、ユーザー名やパスワードなどの接続情報の入力をユーザーに求める必要がある場合は、それ自体を行う必要があります。 これにより、アプリケーションは "ルックアンドフィール" を制御できるようになりますが、アプリケーションにドライバー固有のコードが含まれている可能性があります。 これは、アプリケーションがユーザーにドライバー固有の接続情報を要求する必要がある場合に発生します。 これにより、アプリケーションの作成時に存在しないドライバーを含め、すべてのドライバーを使用するように設計された汎用アプリケーションの場合、不可能な状況が発生します。  
  
 **SQLDriverConnect** は、ユーザーに接続情報の入力を求めることができます。 たとえば、前述のカスタムプログラムでは、次の接続文字列を **SQLDriverConnect**に渡すことができます。  
  
```  
DSN=XYZ Corp;  
```  
  
 次の図のように、ドライバーによってユーザー Id とパスワードの入力を求めるダイアログボックスが表示される場合があります。  
  
 ![ユーザー ID とパスワードの入力を求めるダイアログ ボックス](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 ドライバーが接続情報の入力を求めることができるかどうかは、汎用的なアプリケーションと垂直方向のアプリケーションに特に役立ちます。 これらのアプリケーションにはドライバー固有の情報が含まれていない必要があります。また、必要な情報をドライバーから要求された場合は、その情報をアプリケーションから除外します。 これは、前の2つの例で示されています。 アプリケーションがデータソース名のみをドライバーに渡した場合、アプリケーションにドライバー固有の情報が含まれていなかったため、特定のドライバーに関連付けられていません。 アプリケーションが完全な接続文字列をドライバーに渡すと、その文字列を解釈できるドライバーに関連付けられていました。  
  
 汎用アプリケーションでは、データソースを指定するのではなく、さらに1つの手順を実行することがあります。 **SQLDriverConnect**が空の接続文字列を受け取ると、次のダイアログボックスが表示されます。  
  
 ![[データ ソースの選択] ダイアログ ボックス](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 ユーザーがデータソースを選択すると、ドライバーマネージャーによって、そのデータソースを指定する接続文字列が構築され、ドライバーに渡されます。 ドライバーは、必要な追加情報をユーザーに確認できます。  
  
 ドライバーがユーザーにプロンプトを表示する条件は、 *Drivercompletion* フラグによって制御されます。常にプロンプトを表示したり、必要に応じてプロンプトを表示したり、メッセージを表示しないようにするオプションがあります。 このフラグの詳細については、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 関数の説明を参照してください。
