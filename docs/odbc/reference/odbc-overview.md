---
description: ODBC の概要
title: ODBC の概要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13f34a1ef329957854a8b33916b6b29506fc0ad9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421316"
---
# <a name="odbc-overview"></a>ODBC の概要
Open Database Connectivity (ODBC) は、データベース アクセスのために広く受け入れられているアプリケーション プログラミング インターフェイス (API) です。 Open Group と ISO/IEC for database Api の呼び出しレベルインターフェイス (CLI) 仕様に基づいており、データベースアクセス言語として構造化照会言語 (SQL) を使用しています。  
  
 ODBC は、 *相互運用性* が最大になるように設計されています。つまり、1つのアプリケーションが同じソースコードを使用して異なるデータベース管理システム (dbms) にアクセスする機能です。 データベースアプリケーションは ODBC インターフェイスの関数を呼び出します。このインターフェイスは、 *ドライバー*と呼ばれるデータベース固有のモジュールに実装されています。 ドライバーを使用すると、プリンタードライバーがプリンター固有のコマンドからワードプロセッシングプログラムを分離するのと同じ方法で、データベース固有の呼び出しからアプリケーションが分離されます。 ドライバーは実行時に読み込まれるため、ユーザーは新しいドライバーを追加して新しい DBMS にアクセスするだけで済みます。アプリケーションを再コンパイルまたは再リンクする必要はありません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC の作成の目的](../../odbc/reference/why-was-odbc-created.md)  
  
-   [ODBC とは](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC と標準の CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
