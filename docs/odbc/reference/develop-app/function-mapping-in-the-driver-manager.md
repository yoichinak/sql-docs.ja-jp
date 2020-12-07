---
description: ドライバー マネージャーの関数マッピング
title: ドライバーマネージャーでの関数マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69434638dee25cdbad8428a1e09cb05a270f99de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499846"
---
# <a name="function-mapping-in-the-driver-manager"></a>ドライバー マネージャーの関数マッピング
ドライバーマネージャーは、文字列引数を受け取る関数の2つのエントリポイントをサポートしています。 非装飾関数 (**SQLDriverConnect**) は、関数の ANSI 形式です。 Unicode 形式は *W* (**SQLDriverConnectW**) で修飾されます。  
  
 ODBC ヘッダーファイル *は、混合* ANSI/Unicode アプリケーションの利便性を高めるために、(**SQLDriverConnectA**) で修飾された関数もサポートしています。 関数に対して行われた呼び出し **は、実際** には、装飾されていないエントリポイント (**SQLDriverConnect**) を呼び出します。  
  
 _UNICODE **#define**を使用してアプリケーションをコンパイルすると、ODBC ヘッダーファイルによって、非装飾関数呼び出し (**SQLDriverConnect**) が UNICODE バージョン (**SQLDriverConnectW**) にマップされます。  
  
 ドライバーマネージャーは、 **Sqlconnectw** がドライバーによってサポートされている場合に、ドライバーを Unicode ドライバーとして認識します。  
  
 ドライバーが Unicode ドライバーの場合、ドライバーマネージャーは次のように関数呼び出しを行います。  
  
-   文字列引数を含まない関数またはパラメーターをドライバーに直接渡します。  
  
-   ( *W* サフィックスの付いた) Unicode 関数を直接ドライバーに渡します。  
  
-   文字列引数を Unicode 文字に変換することに*より、(サフィックスが*付いた*W* ) ANSI 関数を unicode 関数に変換し、その unicode 関数をドライバーに渡します。  
  
 ドライバーが ANSI ドライバーの場合、ドライバーマネージャーは次のように関数呼び出しを行います。  
  
-   文字列の引数またはパラメーターのない関数を直接ドライバーに渡します。  
  
-   Unicode 関数を *W* サフィックス付きで ANSI 関数呼び出しに変換し、ドライバーに渡します。  
  
-   ANSI 関数をドライバーに直接渡します。  
  
 ドライバーマネージャーは、内部的には Unicode に対応しています。 このため、unicode ドライバーを使用している unicode アプリケーションでは、最適なパフォーマンスが得られます。これは、ドライバーマネージャーが Unicode 関数をドライバーに渡すだけであるためです。 Ansi アプリケーションが ANSI ドライバーを使用している場合、ドライバーマネージャーは、 **SQLDriverConnect**などの一部の関数を処理するときに、Ansi から Unicode に文字列を変換する必要があります。 関数を処理した後、ドライバーマネージャーは、ANSI ドライバーに関数を送信する前に、Unicode 文字列を ANSI に変換する必要があります。  
  
 アプリケーションは、ドライバーが SQL_STILL_EXECUTING または SQL_NEED_DATA を返したときに、バインドされたパラメーターバッファーを変更または読み取ることはできません。 ドライバーマネージャーは、ドライバーが SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、または SQL_ERROR を返すまで、ANSI にバインドされたバッファーをそのままにします。 マルチスレッドアプリケーションでは、別のスレッドが SQL ステートメントを実行しているバインドされたパラメーター値にアクセスすることはできません。 ドライバーマネージャーは、データを Unicode から ANSI の "インプレース" に変換します。他のスレッドは、ドライバーが SQL ステートメントを処理している間に、これらのバッファーに ANSI データを表示する可能性があります。 Unicode データを ANSI ドライバーにバインドするアプリケーションでは、2つの異なる列を同じアドレスにバインドすることはできません。
