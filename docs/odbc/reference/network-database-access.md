---
description: ネットワーク データベース アクセス
title: ネットワークデータベースアクセス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 025959072b7ebadc96fd1d1a628bdfaf5d449940
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461324"
---
# <a name="network-database-access"></a>ネットワーク データベース アクセス
ネットワーク経由でデータベースにアクセスするには、さまざまなコンポーネントが必要です。これらはそれぞれ独立しており、プログラミングインターフェイスの下に存在します。 次の図は、これらのコンポーネントについて示しています。  
  
 ![ネットワーク経由でデータベースにアクセスするコンポーネント](../../odbc/reference/media/pr04.gif "pr04")  
  
 各コンポーネントの詳細については、次のとおりです。  
  
-   **プログラミングインターフェイス** このセクションで既に説明したように、プログラミングインターフェイスには、アプリケーションによる呼び出しが含まれています。 これらのインターフェイス (embedded SQL、SQL モジュール、および呼び出しレベルのインターフェイス) は、通常、各 DBMS に固有のものですが、通常は ANSI または ISO 標準に基づいています。  
  
-   **データストリームプロトコル** データストリームプロトコルでは、DBMS とそのクライアントの間で転送されるデータのストリームが記述されます。 たとえば、プロトコルでは、最初のバイトに、実行される SQL ステートメント、返されたエラー値、または返されるデータというストリームの残りの部分について記述する必要があります。 ストリーム内の残りのデータの形式は、このフラグに依存します。 たとえば、エラーストリームには、フラグ、2バイト整数エラーコード、2バイト整数エラーメッセージの長さ、およびエラーメッセージが含まれている場合があります。  
  
     データストリームプロトコルは論理プロトコルであり、基になるネットワークで使用されるプロトコルとは無関係です。 そのため、通常、1つのデータストリームプロトコルを複数の異なるネットワークで使用できます。 データストリームプロトコルは、通常は専用であり、特定の DBMS で動作するように最適化されています。  
  
-   **プロセス間の通信メカニズム** プロセス間通信 (IPC) メカニズムは、あるプロセスが別のプロセスと通信するプロセスです。 例としては、名前付きパイプ、TCP/IP ソケット、DECnet ソケットなどがあります。 IPC メカニズムの選択は、使用されるオペレーティングシステムとネットワークによって制限されます。  
  
-   **ネットワークプロトコル** ネットワークプロトコルは、ネットワーク経由でデータストリームを転送するために使用されます。 これは、データストリームプロトコルを実装するために使用される IPC メカニズムをサポートする構成、およびファイル転送や印刷共有などの基本的なネットワーク操作をサポートする組み込みと考えることができます。 ネットワークプロトコルには、NetBEUI、TCP/IP、DECnet、および SPX/IPX があり、各ネットワークに固有です。
