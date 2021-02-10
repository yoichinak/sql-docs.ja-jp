---
title: Data Migration Assistant を使用したアプリケーションのデータアクセス層の評価
description: Data Migration Assistant を使用して、アプリケーションのデータアクセス層を評価する方法について説明します。
ms.date: 01/23/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: f56976c9140cb4ac18c048d7d57d6949fc4ae74d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100065161"
---
# <a name="assess-an-apps-data-access-layer-with-data-migration-assistant"></a>Data Migration Assistant を使用したアプリのデータアクセス層の評価

通常、アプリケーションはデータベースに接続し、データを保持します。 アプリケーションのデータアクセス層は、このデータへの簡単なアクセスを提供します。 Data Migration Assistant (DMA) では、ユーザーがデータベースと関連オブジェクトを評価できるようになりました。 最新バージョンの DMA (v1.0) では、アプリケーションコードでデータベース接続と埋め込み SQL クエリを分析するためのサポートが導入されています。

次の C# コードセグメントについて考えてみましょう。

![C# コードセグメントのサンプル](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-segment.png)

この場合、アプリケーションが SQL クエリを使用して従業員の名前を取得していることがわかります。

![C# コードセグメントの詳細のサンプル](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-detail.png)

アプリケーションの所有者は、アプリケーションが接続できるさまざまなデータベースと、アプリケーションのデータアクセス層に埋め込まれたクエリを識別できる必要があります。 さらに、Azure Data services にアプリケーションを最新化するために必要な変更を特定する必要があります。

## <a name="assess-an-app-with-data-access-migration-toolkit"></a>データアクセス移行ツールキットを使用したアプリの評価

この評価を有効にするために、データアクセス移行ツールキット (DAMT)、Visual Studio Code の拡張機能が最近導入されました。 この拡張機能の最新バージョン (0.2) では、.Net アプリケーションと T-sql 言語のサポートが追加されています。

1. [ここ](https://code.visualstudio.com/download)から VS Code をダウンロードしてインストールします。
2. 拡張機能マーケットプレースから [Data Access Migration Toolkit 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit) を有効にします。

   ![データアクセス移行ツールキットの拡張機能ページ](../dma/media/dma-assess-app-data-layer/dma-damt-extension-page.png)

3. Visual Studio Code でアプリケーションプロジェクトを開きます。

   ![Visual Studio Code のアプリケーションプロジェクト](../dma/media/dma-assess-app-data-layer/dma-app-project-in-vscode.png)

4. 拡張機能コンソール (Ctrl-Shft-P) を起動し、 **データアクセス: [ワークスペースの分析** ] コマンドを実行します。

   ![Visual Studio Code の拡張コンソール](../dma/media/dma-assess-app-data-layer/dma-vscode-extension-console.png)

5. SQL Server 言語を選択します。

   ![SQL Server 言語選択](../dma/media/dma-assess-app-data-layer/dma-sql-server-dialect.png)

   分析の最後に、コマンドによって SQL 接続コマンドとクエリのレポートが生成されます。

   ![データアクセスレポート](../dma/media/dma-assess-app-data-layer/dma-data-access-report.png)

6. データ接続コンポーネントおよびアプリケーションコードに埋め込まれている SQL クエリのレポートで、強調表示されているものを確認します。

   ![アプリケーションコード内の SQL クエリ](../dma/media/dma-assess-app-data-layer/dma-sql-queries-in-app-code.png)

   これらのクエリは、対象の SQL プラットフォームに基づく互換性と機能のパリティの問題について、DMA によって分析できます。

7. アプリケーションのデータ層を評価するには、レポートを json ファイルとしてエクスポートします。

   ![. json ファイルのエクスポート](../dma/media/dma-assess-app-data-layer/dma-json-file-export.png)

   この場合、生成されたファイルは次のようになります。

   ![Json ファイルの内容を表示する](../dma/media/dma-assess-app-data-layer/dma-json-file-contents.png)

   Data Migration Assistant を使用すると、データベースを Azure Data platform に最新化するコンテキスト内で、アプリケーションで特定されたクエリを評価できます。

8. Data Migration Assistant を開始し、評価プロジェクトを作成します。

   ![新しい評価プロジェクトの Data Migration Assistant](../dma/media/dma-assess-app-data-layer/dma-new-assessment-project.png)

9. ソース SQL Server インスタンスを選択します。

   ![SQL Server ソースを選択 Data Migration Assistant には](../dma/media/dma-assess-app-data-layer/dma-select-sql-source.png)

10. アプリケーションが接続しているデータベースを選択します。

    ![データアクセスの移行アプリケーションデータベースの選択](../dma/media/dma-assess-app-data-layer/dma-select-app-database.png)

    データアクセスの評価を容易にするために、DMA には、アプリケーションクエリに json ファイルを含める機能が導入されています。 次に、アプリケーションクエリで事前に記述した json ファイルを含めます。

11. データベースを選択し、データアクセス移行ツールキットからエクスポートした json ファイルを参照して、評価用のアプリケーションからのクエリを含めます。

    ![Data Migration Assistant open DMAT json ファイル](../dma/media/dma-assess-app-data-layer/dma-open-damt-json-file.png)

12. 評価を開始します。

    ![評価の開始 Data Migration Assistant](../dma/media/dma-assess-app-data-layer/dma-start-assessment.png)

13. 評価レポートを確認します。 生成されたレポートには、次に示すように、アプリケーションクエリで検出された互換性または機能のパリティの問題が含まれます。

    ![Data Migration Assistant 評価レポート](../dma/media/dma-assess-app-data-layer/dma-assessment-report.png)

これで、データベースの観点から見ると、ユーザーはアプリケーションの観点から見ることもできます。

## <a name="see-also"></a>関連項目

* [Data Migration Assistant の概要](../dma/dma-overview.md)
* [Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: ベストプラクティス](../dma/dma-bestpractices.md)
* [データ アクセス移行ツールキット](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)