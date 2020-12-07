---
description: トレース DLL
title: トレース DLL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1791b72b5f7e836fba05275f87bd57948a273775
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487505"
---
# <a name="trace-dll"></a>トレース DLL
トレースを実行する DLL は、ODBC のコアコンポーネントの1つです。 現在、トレース DLL は、Windows SDK の ODBC コンポーネントにサンプル DLL として提供されており、以前は Microsoft Data Access Components (MDAC) SDK に含まれていました。 そのため、トレース DLL のレジストリエントリ、インターフェイス、およびサンプルコードを使用できます。 この DLL は、ODBC ユーザーまたはサードパーティベンダーによって作成されたトレース DLL に置き換えることができます。 カスタムトレース DLL には、元のサンプルトレース DLL とは異なる名前を付ける必要があります。 トレース Dll がシステムディレクトリにインストールされている必要があります。インストールしないと、読み込みに失敗します。 接続文字列はドライバーマネージャーによってトレース DLL に渡されません。  
  
 トレース DLL は、入力引数、出力引数、遅延引数、リターンコード、および SQLSTATEs をトレースします。 トレースが有効になっている場合、ドライバーマネージャーは、(引数の検証の前に) 関数の開始時と関数が返される直前の2つのポイントでトレース DLL を呼び出します。  
  
 アプリケーションが関数を呼び出すと、ドライバーマネージャーは、ドライバーで関数を呼び出す前、または呼び出し自体を処理する前に、トレース DLL 内のトレース関数を呼び出します。 各 ODBC 関数には、ODBC 関数と同じ名前を持つ、対応するトレース関数 (先頭に *trace*が付いています) があります。 トレース関数が呼び出されると、トレース DLL は入力引数をキャプチャし、リターンコードを返します。 ドライバーマネージャーが引数を検証する前にトレース DLL が呼び出されるため、無効な関数呼び出しがトレースされるため、状態遷移エラーと無効な引数がログに記録されます。  
  
 トレース DLL でトレース関数を呼び出した後、ドライバーマネージャーはドライバーで ODBC 関数を呼び出します。 次に、トレース DLL で **Tracereturn** を呼び出します。 この関数は2つの引数を受け取ります。トレース関数のトレース DLL によって返される値と、ドライバーによって ODBC 関数のドライバーマネージャーに返されるリターンコード (または、関数を処理した場合は、ドライバーマネージャー自体によって返される値)。 関数は、トレース関数に返された値を使用して、キャプチャされた入力引数値を操作します。 ODBC 関数に対して返されたコードをログファイルに書き込みます (有効になっている場合は、動的に表示されます)。 出力引数のポインターを逆参照し、出力引数の値をログに記録します。
