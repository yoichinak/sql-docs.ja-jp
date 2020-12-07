---
title: 開発パイプラインでの SqlPackage
description: インストールされているビルド番号を確認することで SqlPackage.exe によるデータベース開発パイプラインのトラブルシューティングを行う方法について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: 14e54b44a5cfc40e98d1de9de1796630bb903b4f
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94385225"
---
# <a name="sqlpackage-in-development-pipelines"></a>開発パイプラインでの SqlPackage

**SqlPackage.exe** は、さまざまなデータベース開発タスクを自動化するコマンドライン ユーティリティであり、CI/CD パイプラインに組み込むことができます。

## <a name="managed-virtual-environments"></a>マネージド仮想環境

GitHub Actions でホストされているランナーと Azure Pipelines VM イメージに使用される仮想環境は、[virtual-environments](https://github.com/actions/virtual-environments) GitHub リポジトリで管理されます。  SqlPackage は `windows-latest` 環境に含まれており、そのイメージへの更新は、それぞれの SqlPackage リリースの数週間以内に行われます。

## <a name="checking-the-sqlpackage-version"></a>SqlPackage のバージョンを確認する

トラブルシューティング作業中は、使用されている SqlPackage のバージョンを把握しておくことが重要です。  この情報の把握は、`/version` パラメーターを指定して SqlPackage を実行するステップをパイプラインに追加することで実行できます。  以下に示す例は、Microsoft と GitHub によって管理される環境に基づいており、自己ホスト型の環境では作業ディレクトリのインストール パスが異なっている場合があります。

### <a name="azure-pipelines"></a>Azure Pipelines

Azure パイプラインで [script](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema#script) キーワードを利用することで、SqlPackage のバージョン番号を出力する手順を Azure パイプラインに追加できます。

```yaml
- script: sqlpackage.exe /version
  workingDirectory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  displayName: 'get sqlpackage version'
```

### <a name="github-actions"></a>GitHub Actions

GitHub アクション ワークフローで [run](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions) キーワードを利用することで、SqlPackage のバージョン番号を出力する手順を GitHub アクションに追加できます。

```yaml
- name: get sqlpackage version
  working-directory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  run: ./sqlpackage.exe /version
```

:::image type="content" source="media/sqlpackage-pipelines-github-action.png" alt-text="ビルド番号 15.0.4897.1 を表示している GitHub アクションの出力表示":::

## <a name="next-steps"></a>次のステップ

- [sqlpackage](sqlpackage.md) について詳しく学習する
