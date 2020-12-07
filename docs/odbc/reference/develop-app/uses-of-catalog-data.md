---
description: カタログ データの使用
title: カタログデータの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e03dff0a8c5715a86f1bcdff65b74f55409889a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471199"
---
# <a name="uses-of-catalog-data"></a>カタログ データの使用
アプリケーションでは、さまざまな方法でカタログデータを使用します。 一般的な用途を次に示します。  
  
-   **実行時の SQL ステートメントの構築。** 注文入力アプリケーションなどの垂直方向のアプリケーションには、ハードコーディングされた SQL ステートメントが含まれています。 アプリケーションによって使用されるテーブルと列は、これらのテーブルにアクセスするステートメントと同様に、あらかじめ修正されています。 たとえば、注文入力アプリケーションには、通常、システムに新しい注文を追加するためのパラメーター化された **INSERT** ステートメントが1つ含まれています。  
  
     ODBC を使用してデータを取得するスプレッドシートプログラムなどの汎用アプリケーションでは、多くの場合、ユーザーからの入力に基づいて、実行時に SQL ステートメントを構築します。 このようなアプリケーションでは、使用するテーブルと列の名前をユーザーが入力する必要があります。 ただし、ユーザーが選択できるテーブルと列の一覧がアプリケーションに表示されている場合は、ユーザーにとってより簡単になります。 これらのリストを構築するために、アプリケーションは **Sqltables** および **sqltables** カタログ関数を呼び出します。  
  
-   **開発時の SQL ステートメントの構築。** 通常、アプリケーション開発環境では、プログラマがプログラムの開発中にデータベースクエリを作成できます。 作成されたアプリケーションでは、クエリがハードコーディングされます。  
  
     このような環境では、 **Sqltables** と **sqltables** を使用して、プログラマが選択できるリストを作成することもできます。 これらの環境では、 **Sqlprimarykeys** と **SQLForeignKeys** を使用して、選択したテーブル間のリレーションシップを自動的に決定して表示することもできます。また、 **sqlstatistics** を使用してインデックス付きフィールドを決定および強調表示することにより、効率的なクエリを作成できます。  
  
-   **カーソルを構築しています。** スクロール可能なカーソルエンジンを提供するアプリケーション、ドライバー、またはミドルウェアは、 **Sql特殊な列** を使用して、行を一意に識別する列を特定できます。 プログラムは、フェッチされた行ごとに、これらの列の値を含む *キーセット* を作成できます。 アプリケーションが行までスクロールすると、次の値を使用して行の最新のデータがフェッチされます。 スクロール可能なカーソルとキーセットの詳細については、「スクロール可能な [カーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)」を参照してください。
