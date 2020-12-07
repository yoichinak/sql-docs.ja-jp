---
title: Azure Data Studio のプレビュー機能
description: Azure Data Studio プレビュー機能の詳細と、それらを有効にして使用する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: hannahqin
ms.author: hanqin
ms.reviewer: maghan
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 4054917071578fb0b3ddcf5c22d5950075a2b0fe
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328486"
---
# <a name="preview-features-in-azure-data-studio"></a>Azure Data Studio のプレビュー機能

Azure Data Studio の新機能と機能強化は、一般公開 (GA) される前に、プレビュー機能としてまずリリースされることがよくあります。 機能がプレビュー段階にとどまる時間は、ユーザーのフィードバック、品質チェック、および長期的なロード マップによって異なります。 プレビュー機能を有効にすると、Azure Data Studio 機能にフル アクセスできるようになり、早期にフィードバックを提供できるようになります。

## <a name="how-do-i-enable-preview-features"></a>プレビュー機能を有効にする方法

### <a name="on-first-launch"></a>初回起動時

新しいユーザーの場合は、初めて Azure Data Studio を起動するときにプレビュー機能を選択できます。 起動時に、画面の右下隅にトースト通知が表示され、プレビュー機能を有効または無効にするオプションが提供されます。 プレビュー機能を有効にするには、 **[はい (推奨)]** を選択します。

![初回起動時のプレビューのトースト通知](./media/getting-started/preview-toast-notification.png)

### <a name="in-settings"></a>設定で

プレビュー機能は、設定でいつでも有効または無効にすることができます。

1. 左下隅にある **歯車** アイコンを選択し、コンテキスト メニューから **[設定]** を選択します。 [設定] タブが開きます。

   ![ADS で設定にアクセスするための歯車アイコン](./media/settings/open-settings-menu.png)

2. 検索バーに「プレビュー機能を有効にする」と入力します。

3. プレビュー機能を有効にするには、 **[Workbench: プレビュー機能を有効にする]** の下の **[未リリースのプレビュー機能を有効にする]** チェックボックスをオンにします。 プレビュー機能を無効にするには、チェックボックスをオフにします。

   ![ADS でプレビュー機能設定を有効にする](./media/settings/preview-features-settings.png)

## <a name="list-of-preview-features-in-azure-data-studio"></a>Azure Data Studio のプレビュー機能のリスト

### <a name="general-features-in-preview"></a>プレビューの一般的な機能

* Azure ポータルの統合
* バックアップ/復元
* デプロイメント
    * SQL Edge
    * SQL Server ビッグ データ クラスター
    * SQL Server コンテナー イメージ
    * Windows 上の SQL Server
* 機能ツアー
*  SQLCMD モード
* 新しいウェルカム ページ

### <a name="notebook-features-in-preview"></a>プレビューの Notebook 機能

* Dotnet 対話型サポート
* Markdown ツールバー
*  新しいノートブック ツール バー
* Notebook カーネル
    * Kusto
    * PowerShell
    * PySpark
    * Python
    * Spark | Scala
    * Spark | R
    * SQL
* ブラウザーから Notebook を開く
* ピン留めされた Notebooks
* Python の依存関係ウィザード

### <a name="first-party-extensions-in-preview"></a>プレビュー段階のファーストパーティ拡張機能

* SQL Server 用の管理パック
* Azure Synapse Analytics Insights
* 中央管理サーバー
* Database Administration Tool Extensions for Windows
* Kusto
* 言語パック
* PostgreSQL
* PowerShell
* クエリ履歴
* SandDance for Azure Data Studio
* サーバー レポート
* SQL の評価
* SQL Server エージェント
* SQL Server プロファイラー
* Machine Learning
* Managed Instance ダッシュボード
* Visual Studio IntelliCode
* whoisactive

## <a name="next-steps"></a>次のステップ

* [Azure Data Studio](what-is-azure-data-studio.md)
