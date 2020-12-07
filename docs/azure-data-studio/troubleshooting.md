---
title: Azure Data Studio のトラブルシューティング
description: Azure Data Studio のログを取得してトラブルシューティングを行う方法について説明します。これは、バグ レポートを報告するときに役立ちます。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: hanqin, maghan
ms.custom: seodec18
ms.date: 11/24/2020
ms.openlocfilehash: 1d2483532589cd840f1120cfb0ac3273b41e0bb5
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "95920212"
---
# <a name="azure-data-studio-troubleshooting"></a>Azure Data Studio のトラブルシューティング
Azure Data Studio での問題と機能要求の追跡には、`azuredatastudio` リポジトリの [GitHub リポジトリ イシュー トラッカー](https://github.com/Microsoft/azuredatastudio/issues)が使用されます。 

## <a name="if-youve-experienced-any-issue"></a>問題が発生した場合

問題を [GitHub イシュー トラッカー](https://github.com/Microsoft/azuredatastudio/issues)に報告し、担当者がエラーの再現に役立つ詳細情報を把握できるようにしてください。 ログ ファイルのすべての[ログ情報](#how-to-set-the-logging-level)を含めます。

## <a name="writing-good-bug-reports-and-feature-requests"></a>適切なバグ レポートと機能要求の記述

問題および機能要求ごとに 1 つのイシューを登録します。

* 同じイシューに、複数のバグまたは機能要求を列挙しないでください。
* 入力内容が同じ場合を除き、既存のイシューに自分のイシューをコメントとして追加しないでください。 多くのイシューは似ていますが、原因は異なります。

提供できる情報が多いほど、問題を再現して解決策を発見できる可能性が高くなります。 

各イシューには次の情報を含めます。

* Azure Data Studio のバージョン
* 再現可能な手順 (1...2...3...)、および予想されたものと実際に表示されたもの。 
* 画像、アニメーション、またはビデオへのリンク。 画像とアニメーションは再現手順を示していますが、それらを置き換えないでください。
* 問題が示されるコード スニペット、またはこちらでコンピューターに簡単にプルダウンして問題を再現できるコード リポジトリへのリンク。 

> [!NOTE]
>  コード スニペットをコピーして貼り付ける必要があるため、コード スニペットをメディア ファイル (.gif など) として含めるだけでは不十分です。 

* 開発者ツール コンソールでのエラー([ヘルプ] > [開発者ツールの切り替え])

次の点に注意してください。

* イシュー リポジトリを検索して、同じものが存在するかどうかを確認します。 
* 問題をより的確に特定できるように、イシューに関するコードを簡略化します。 

こちらで問題を再現できず、さらに多くの情報を要求することがあっても、気を悪くしないでください。

## <a name="how-to-set-the-logging-level"></a>ログ レベルを設定する方法

### <a name="azure-data-studio"></a>Azure Data Studio
現在のセッションのログ レベルを選択するには、`Developer: Set Log Level...` コマンドを実行します。 この値は複数のセッションにわたって保持されないため、Azure Data Studio を再起動すると、既定の `Info` レベルに戻ります。 

起動時にデバッグ ログを有効にする場合は、ログ レベルを `Debug` に設定して、`Developer: Reload Window` コマンドを実行します

### <a name="mssql-built-in-extension"></a>MSSQL (組み込み拡張機能)

`Mssql: Log Debug Info` ユーザー設定が true に設定されている場合、デバッグ ログ情報が `MSSQL` の出力チャネルに送信されます。

`Mssql: Tracing Level` ユーザー設定は、ログの詳細度を制御するために使用されます。

## <a name="debug-log-location"></a>デバッグ ログの場所
ログへのパスを開くには、Azure Data Studio から `Developer: Open Logs Folder` コマンドを実行します。 さまざまな種類の多数のログ ファイルがそこに書き込まれています。よく使用されるものは次のとおりです。

1. `renderer#.log` (例: renderer1.log) - このファイルは、メイン プロセス用のログ ファイルです。
1. `telemetry.log` - ログ レベルが `Trace` に設定されている場合、Azure Data Studio によって送信されたテレメトリ イベントがこのファイルに格納されます
1. `exthost#/exthost.log` - 拡張機能のホスト プロセス用のログ ファイル (これはプロセス自体だけであり、その内部で実行されている拡張機能ではありません)
1. `exthost#/Microsoft.mssql` - mssql 拡張機能用のログであり、MSSQL 関連の機能のコア ロジックの多くが含まれます
   * sqltools.log は SQL ツール サービス用のログです
1. `exthost#/output_logging_#######` - これらのフォルダーには、Azure Data Studio の [`Output`] パネルに表示されたメッセージが格納されます。 各ファイルの名前は `#-<Channel Name>` であり、たとえば `Notebooks` の出力チャネルは `3-Notebooks.log` という名前のファイルに出力される場合があります。

ログの提供を求められた場合は、正しいログが確実に含まれるように、フォルダー全体を zip 形式で圧縮してください。 

## <a name="next-steps"></a>次の手順
- [問題の報告](https://github.com/Microsoft/azuredatastudio/issues)
- [Azure Data Studio とは](what-is-azure-data-studio.md)