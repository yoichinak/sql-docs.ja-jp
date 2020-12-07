---
title: SQL Server エージェントの拡張機能
description: SQL Agent のジョブと構成を管理するための拡張機能である、Azure Data Studio 用の SQL Server エージェント拡張機能をインストールして使用する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 3d00919c0967db12dfe678ad541a5a9ed9ecae61
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123273"
---
# <a name="sql-server-agent-extension-preview"></a>SQL Server エージェントの拡張機能 (プレビュー)

SQL Server エージェントの拡張機能 (プレビュー) は、SQL エージェントのジョブおよび構成の管理とトラブルシューティングを行うための拡張機能です。 この拡張機能は、現在プレビューの段階にあります。

主要なアクションには、次のようなものがあります。

- SQL Server 上で構成された SQL Server エージェント ジョブを一覧表示する
- ジョブの実行結果を含むジョブ履歴を表示する
- ジョブの開始と停止を行う基本的なジョブの制御

## <a name="install-the-sql-server-agent-extension"></a>SQL Server エージェントの拡張機能をインストールする

1. 拡張機能マネージャーを開いて、使用可能な拡張機能にアクセスするには、拡張機能アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。
2. 使用可能な拡張機能を選択すると、その詳細が表示されます。

   ![エージェントのインストール](media/sql-server-agent-extension/install-sql-agent.png)

3. 必要な拡張機能を選択して**インストール**します。
4. **[再読み込み]** を選択して拡張機能を有効にします (拡張機能を初めてインストールするときにのみ必要です)。
5. ご利用のサーバーまたはデータベースを右クリックし、 **[管理]** を選択することで、ご利用の管理ダッシュボードに移動します。
6. インストールされた拡張機能が、ご利用の管理ダッシュボード上にタブとして表示されます。

   ![エージェントの表示](media/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>ジョブの表示

SQL Server エージェントの拡張機能に接続すると、最初に表示されるのは、ご利用のすべてのエージェント ジョブの一覧です。

   ![ジョブの表示](media/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>次のステップ

SQL Server エージェントの詳細については、[こちら](../../ssms/agent/sql-server-agent.md)のドキュメントを参照してください。
