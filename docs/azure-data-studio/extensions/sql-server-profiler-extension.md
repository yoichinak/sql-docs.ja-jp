---
title: SQL Server Profiler の拡張機能
description: SQL Server Profiler の拡張機能をインストールし、使用する方法について説明します。 SSMS Profiler に似た使いやすい SQL Server トレース ソリューション。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c76e4cf15edcfeb6cb25b9d205f79ba34386e8d0
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123225"
---
# <a name="sql-server-profiler-extension-preview"></a>SQL Server Profiler の拡張機能 (プレビュー)

SQL Server Profiler の拡張機能 (プレビュー) は、拡張イベントを使用して構築されていることを除けば、SQL Server Management Studio (SSMS) プロファイラーに類似したシンプルな SQL Server トレース ソリューションです。 SQL Server Profiler は、非常に使いやすく、最も一般的なトレース構成に合わせて適切な既定値を備えています。 UX は、イベントを参照するため、および関連付けられた Transact-SQL (T-SQL) テキストを表示するために最適化されています。 Azure Data Studio 用の SQL Server Profiler では、使いやすい UX で T-SQL 実行アクティビティを収集するための適切な既定値も想定されています。 この拡張機能は、現在プレビューの段階にあります。

**一般的な SQL Profiler のユースケース:**

- 問題の原因を特定するため、問題の発生したクエリを順次実行する。
- 実行速度の遅いクエリを検出し、その原因を診断する。
- 問題の原因となる一連の Transact-SQL ステートメントをキャプチャする。
- ワークロードを調整するため、SQL Server のパフォーマンスを監視する。
- 問題を診断するために、さまざまなパフォーマンス カウンターの関連を調べる。

## <a name="install-the-sql-server-profiler-extension"></a>SQL Server Profiler の拡張機能をインストールする

1. 拡張機能マネージャーを開いて、使用可能な拡張機能にアクセスするには、拡張機能アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。
2. 使用可能な拡張機能を選択すると、その詳細が表示されます。

    ![プロファイラー拡張機能マネージャー](media/sql-server-profiler-extension/profiler-extension.png)

3. 必要な拡張機能を選択して**インストール**します。
4. **[再読み込み]** を選択して拡張機能を有効にします (拡張機能を初めてインストールするときにのみ必要です)。

## <a name="start-profiler"></a>Profiler の開始

1. Profiler を起動するには、まず [サーバー] タブでサーバーへの接続を確立します。
2. 接続を確立したら、**Alt + P** キーを押して Profiler を起動します。
3. Profiler を起動するには、**Alt + S** キーを押します。これで、拡張イベントの表示を開始できます。

    ![プロファイラーの表示](media/sql-server-profiler-extension/view-profiler.png)

4. Profiler を停止するには、**Alt + S** キーを押します。このホットキーはトグルです。

## <a name="next-steps"></a>次のステップ

Profiler と拡張イベントの詳細については、[拡張イベント](../../relational-databases/extended-events/extended-events.md)に関するページを参照してください。