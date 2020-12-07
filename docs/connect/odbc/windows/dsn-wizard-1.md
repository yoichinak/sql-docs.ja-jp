---
description: データ ソース ウィザード画面 1 (ODBC Driver for SQL Server)
title: データ ソース ウィザード画面 1 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78009925b5d62e8a314d0a3fdc27c29acaee5c5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462226"
---
# <a name="data-source-wizard-screen-1"></a>データ ソース ウィザード画面 1

データ ソースの名前と説明、およびデータ ソースが接続される、SQL Server を実行しているサーバーの名前を指定します。 
    
## <a name="options"></a>オプション

### <a name="name"></a>名前

データ ソースへの接続を要求する場合に ODBC アプリケーションで使用されるデータ ソースの名前です。 たとえば、"人事" のようにします。 データ ソース名は、[ODBC データ ソース アドミニストレーター] ダイアログ ボックスに表示されます。

### <a name="description"></a>説明

(省略可) データ ソースの説明です。 たとえば、"全従業員の入社日、給与履歴、および現在の評価" のようにします。

### <a name="select-or-enter-a-server-name"></a>[サーバー名の選択または入力]

ネットワーク上の SQL Server のインスタンスの名前です。 次の編集ボックスにサーバーを指定する必要があります。

ほとんどの場合、ODBC ドライバーは、既定のプロトコルの順序とこのボックスに指定されたサーバー名を使用して接続することが可能です。 サーバーの別名を作成する場合やクライアント ネットワーク ライブラリを構成する場合は、SQL Server 構成マネージャーを使用してください。

SQL Server と同じコンピューターを使用している場合は、[サーバー] ボックスに「(local)」と入力することができます。 その後、ネットワークに接続されていないバージョンの SQL Server を実行している場合でも、ユーザーは SQL Server のローカル インスタンスに接続することができます。 SQL Server の複数インスタンスを同一コンピューターで実行できます。 SQL Server の名前付きインスタンスをサポートするには、<_サーバー名_>\\<_インスタンス名_> という形式でサーバー名を指定します。

さまざまな種類のネットワークに対応するサーバー名の詳細については、SQL Server オンライン ブックにある SQL Server のインストールに関するドキュメントを参照してください。

### <a name="finish"></a>[完了]

SQL Server への接続に必要なすべての情報がこの画面で指定されると、**[完了]** をクリックすることができます。 ウィザードの他の画面で指定するすべての属性には既定値が使用されます。

### <a name="next"></a>次へ

ウィザードの次の画面に進むには、**[Next]** をクリックします。

## <a name="next-steps"></a>次のステップ

[データ ソース ウィザード画面 2](../../../connect/odbc/windows/dsn-wizard-2.md)
