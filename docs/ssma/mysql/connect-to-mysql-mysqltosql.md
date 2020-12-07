---
description: MySQL への接続 (MySQLToSQL)
title: MySQL への接続 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 399946496bbb649f84c9d539a9fe80f3f7919b31
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372698"
---
# <a name="connect-to-mysql-mysqltosql"></a>MySQL への接続 (MySQLToSQL)
[ **Mysql への接続** ] ダイアログボックスを使用して、移行する mysql データベースに接続します。  
  
このダイアログボックスにアクセスするには、[ **ファイル** ] メニューの [ **MySQL に接続**] を選択します。 以前に接続している場合は、コマンドが **MySQL に再接続**されます。  
  
## <a name="options"></a>オプション  
**プロバイダー**  
  
使用可能な MySQL プロバイダーは MySQL ODBC 5.1 Driver (trusted) です。  
  
**モード**  
  
既定のモードは [標準モードです。 標準モードでは、MySQL、サーバー名、サーバーポート、ユーザー名、およびパスワードの値を入力または選択します。  
  
**サーバー名**  
  
MySQL サーバー名を入力します。 これは標準モードオプションです。  
  
**サーバーポート**  
  
サーバーポートを入力します。 既定のサーバーポートは3306です。 これは標準モードオプションです。  
  
**ユーザー名**  
  
MySQL データベースへの接続に SSMA が使用するユーザー名を入力します。  
  
**パスワード**  
  
ユーザー名に対応するパスワードを入力します。  
  
**SSL**  
  
MySQL に安全に接続する場合は、 **ssl** チェックボックスをオンにして Ssl (Secure Socket Layer) を使用します。  
  
**構成**  
  
Secure Socket Layer (SSL) を介した MySQL への接続を構成するためのオプションが用意されています。  
  
> [!NOTE]  
> **構成**を有効にするには、SSL を**True**に設定する必要があります。  
  
[構成] ボタンをクリックすると、ダイアログボックスが表示されます。 MySQL データベースへの接続中に暗号化を使用するには、ダイアログボックスに存在する次の3つの証明書ファイルへのパスを定義する必要があります [Privacy Enhanced Mail 証明書 (PEM)]:  
  
-   **SSL 証明機関:** 信頼された SSL CAs の一覧を含むファイルへのパスを指定します。  
  
-   **SSL 証明書:** セキュリティで保護された接続を確立するために使用する SSL 証明書ファイルの名前を指定します。  
  
-   **SSL キー:** セキュリティで保護された接続を確立するために使用する SSL キーファイルの名前を指定します。  
  
> [!NOTE]  
> -   必要な情報が提供されている場合は、 **[OK** ] ボタンが有効になります。 いずれかのファイルパスが無効な場合は、[OK] ボタンが無効のままになります。  
> -   **[キャンセル**] ボタンをクリックすると、ダイアログボックスが閉じ、メインの接続フォームから SSL オプションが**オフになり**ます。  
  
