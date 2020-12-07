---
description: ODBC Driver for Oracle の構成
title: ODBC Driver for Oracle の構成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53bf5efc66ad260c0184baf95a254313319da5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483675"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>ODBC Driver for Oracle の構成
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 Odbc Driver for Oracle のパフォーマンスを制御するには、データ環境を把握し、[ [Odbc データソースアドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md) ] ダイアログボックスまたは [接続文字列] パラメーターを使用してデータソース接続のパラメーターを正しく設定します。 ダイアログボックスには、ダイアログボックスまたは接続文字列を使用してデータソースに接続するための次のコントロールが用意されています。  
  
-   **[ユーザー DSN] タブ** コンピューターに対してローカルなデータソース名を一覧表示します。  
  
-   **[システム DSN] タブ** システムデータソースを追加または削除できます。 システムデータソースは、ローカルコンピューター上のすべてのユーザーがアクセスできます。  
  
-   **[ファイル DSN] タブ** ローカルコンピューターのファイルデータソースを追加または削除できます。 ファイルデータソースは、同じドライバーがインストールされているすべてのユーザーが共有できます。  
  
-   **[ドライバー] タブ** インストールされている ODBC ドライバーの一覧を表示します。  
  
-   **[トレース] タブ** Odbc ドライバーマネージャーが ODBC 関数の呼び出しをトレースする方法を指定できます。 インストールされている ODBC アプリケーションごとに、トレースを個別に構成できます。  
  
-   **[接続プール] タブ** インストールされているドライバーごとに接続オプションを選択できます。  
  
-   **[バージョン情報] タブ** インストールされている ODBC コンポーネントファイルを一覧表示します。  
  
 データソースを追加した後は、[ **ODBC データソースアドミニストレーター** ] ダイアログボックスを使用して、データソースへのアクセスを構成できます。 データソースを選択し、タブのいずれかをクリックして、情報を編集または確認します。
