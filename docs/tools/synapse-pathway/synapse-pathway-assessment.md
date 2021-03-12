---
title: Azure Synapse Pathway プレビューの評価。
description: Azure Synapse Pathway でデータ ウェアハウスのコード翻訳を実行する
author: anshul82-ms
ms.author: anrampal
ms.prod: sql
ms.technology: tools-other
ms.topic: tutorial
ms.date: 03/02/2021
monikerRange: =azure-sqldw-latest
ms.custom: template-tutorial
ms.openlocfilehash: 3e5e8536c135244288d022879764d021c53e67ca
ms.sourcegitcommit: f10f0d604be1dce6c600a92aec4c095e7b52e19c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2021
ms.locfileid: "102770505"
---
# <a name="tutorial-to-perform-your-first-code-translation-with-azure-synapse-pathway-preview"></a>Azure Synapse Pathway プレビューで初めてのコード翻訳を実行するためのチュートリアル
[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

Azure Synapse Pathway プレビューには、Azure Synapse Analytics への移行を自動化する T-SQL 準拠コードに、**Netezza**、**Snowflake**、**Microsoft SQL Server** からスキーマ、テーブル、ビュー、関数などを翻訳するためのサポートが導入されています。

詳細については、「[Azure Synapse Pathway プレビューの概要](azure-synapse-pathway-overview.md)」を参照してください。

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> * 既存のデータ ウェアハウスからの SQL スクリプトの Azure Synpase SQL 用の T-SQL スクリプトへの最初の翻訳を実行する 
> * 使用可能なソースのいずれかを選ぶ
> * 翻訳されなかったオブジェクトに関するエラーと警告を表示する

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、[Azure Synapse Pathway](synapse-pathway-download.md) がインストールされていることを確認します。 概要が必要な場合は、[Azure Synapse Pathway の概要](azure-synapse-pathway-overview.md)に関するページを参照してください。

## <a name="run-the-translation"></a>翻訳を実行する

1. Azure Synapse Pathway MSI を起動します。 

1. 使用可能なソースのいずれかを選択すると、すぐに追加されるソースが灰色表示されます。
1. 入力ディレクトリ フォルダーで、[参照] を選択し、翻訳する必要がある **DDL** および **DML** スクリプトのフォルダーの場所をツールに示します。

    > [!Note]
    > 入力ソースとして指定できるのは、拡張子が .sql のファイルのみです。 ユーザーが .txt ファイルで DDL や DML スクリプトを指定すると、ツールで翻訳は実行されません。

1. Netezza コードを Azure Synapse Analytics に翻訳する場合は、[翻訳の種類] ドロップ ダウンで [IBM Netezza] を選びます。
  ![Azure Synapse 評価の入力。](./media/synapse-pathway-assessment/assessment-input.png)

1. 出力ディレクトリを選択するには、[参照] を選択し、出力が生成される場所を指定します。
 ![Azure Synapse の出力ディレクトリ。](./media/synapse-pathway-assessment/output-directory.png)

1. **[翻訳]** を選択して翻訳を開始します

## <a name="view-results"></a>結果を表示する

1. 評価の期間は、追加されたデータベースの数と各データベースのスキーマ サイズによって異なります。 各データベースの結果は利用可能になるとすぐに表示されます。
 ![Azure Synapse の評価レポート。](./media/synapse-pathway-assessment/assessment-report-rendering.png)

1. [結果の表示] を選択すると、前の手順で指定された出力ディレクトリに移動し、入力ディレクトリ構造に基づく翻訳済みスクリプト ファイルが表示されます。

1. これには、GitHub リポジトリに簡単にコミットできるプロジェクトの構造が含まれています。
  
1. エラーと警告の一覧が含まれる、結果ファイルは、同じ出力ディレクトリにアップロードされます。

## <a name="run-the-translation-using-command-line"></a>コマンド ラインを使用して翻訳を実行する
1. インストール時に、AspCmd.exe が C:\Program Files (x86)\Azure Synapse Pathway (プレビュー) から使用できるようになります
1. コマンド プロンプトを起動して、ファイルの保存先に移動する 
1. コマンドの一覧を見るには、「aspcmd.exe--help」と入力します

  ![Azure Synapse の評価コマンド ライン ヘルプ コマンド。](./media/synapse-pathway-assessment/command-line-help.png)


4. コマンド ラインを使用して翻訳の実行を開始することができます

 ![コマンド ラインを使用した Azure Synapse の評価。](./media/synapse-pathway-assessment/command-line-assessment.png)

## <a name="next-steps"></a>次のステップ

[評価を保存して読み込む方法について学習する](tutorial-save-load-assessment.md)
