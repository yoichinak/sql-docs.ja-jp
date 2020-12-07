---
description: アプリケーション
title: アプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc811b075eb698e5127fc321406bf906012c6d12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386138"
---
# <a name="applications"></a>アプリケーション
*アプリケーション*は、データにアクセスするために ODBC API を呼び出すプログラムです。 多くの種類のアプリケーションが可能ですが、ほとんどは、このガイド全体の例として使用される3つのカテゴリに分類されています。  
  
-   **汎用アプリケーション** これらは、"圧縮ラップされたアプリケーション" または "既製のアプリケーション" とも呼ばれます。 汎用アプリケーションは、さまざまな Dbms で動作するように設計されています。 たとえば、詳細な分析のために ODBC を使用してデータをインポートするスプレッドシートや統計パッケージや、ODBC を使用してデータベースからメーリングリストを取得するワードプロセッサなどがあります。  
  
     汎用アプリケーションの重要なサブカテゴリは、PowerBuilder や Microsoft® Visual Basic®などのアプリケーション開発環境です。 これらの環境で構築されたアプリケーションは、1つの DBMS でしか動作しませんが、環境自体は複数の Dbms で動作する必要があります。  
  
     すべての汎用アプリケーションに共通しているのは、Dbms 間で高度な相互運用が可能で、比較的一般的な方法で ODBC を使用する必要があることです。 相互運用性の詳細については、「 [レベルの相互運用性の選択](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)」を参照してください。  
  
-   **垂直方向のアプリケーション** 垂直アプリケーションでは、注文の入力や製造データの追跡など、1種類のタスクを実行し、アプリケーションの開発者によって制御されるデータベーススキーマを操作します。 特定の顧客の場合、アプリケーションは1つの DBMS で動作します。 たとえば、小規模なビジネスでは、dBase でアプリケーションを使用し、大企業では Oracle で使用する場合があります。  
  
     アプリケーションは、アプリケーションが1つの DBMS に関連付けられていないという方法で ODBC を使用しますが、同様の機能を提供する dbms の数に制限される場合もあります。 このため、アプリケーション開発者は DBMS とは別にアプリケーションを販売できます。 垂直方向のアプリケーションは、開発時に相互運用できますが、ユーザーが DBMS を選択した後に相互運用不可能なコードを含めるように変更されることもあります。  
  
-   **カスタムアプリケーション** カスタムアプリケーションは、1つの会社で特定のタスクを実行するために使用されます。 たとえば、大企業のアプリケーションでは、複数の部門 (それぞれが異なる DBMS を使用) から売上データを収集し、1つのレポートを作成する場合があります。 ODBC は、共通のインターフェイスであり、プログラマが複数のインターフェイスを学習する必要がないために使用されます。 通常、このようなアプリケーションは相互運用できず、特定の Dbms とドライバーに書き込まれます。  
  
 多くのタスクは、ODBC の使用方法に関係なく、すべてのアプリケーションに共通です。 これらは、すべての ODBC アプリケーションのフローを定義しています。 タスクは次のとおりです。  
  
-   データソースを選択して接続します。  
  
-   実行する SQL ステートメントを送信しています。  
  
-   結果の取得 (存在する場合)。  
  
-   処理エラー。  
  
-   SQL ステートメントを囲むトランザクションをコミットまたはロールバックしています。  
  
-   データソースから切断しています。  
  
 ほとんどのデータアクセス作業は SQL で行われるため、アプリケーションが ODBC を使用する主なタスクは、SQL ステートメントを送信し、これらのステートメントによって生成された結果 (存在する場合) を取得することです。 ODBC を使用するその他のタスクには、ドライバー機能の決定と調整、データベースカタログの参照などがあります。
