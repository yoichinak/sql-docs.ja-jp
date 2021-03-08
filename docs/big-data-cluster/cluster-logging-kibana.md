---
title: Kibana ダッシュボードを使用してクラスター ログを確認する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスター上で Kibana ダッシュボードを使用したクラスターの監視。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 02/25/2021
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7c26dc7e193d3dd5ad688af4d4dc79e2dd3eeea7
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101835969"
---
# <a name="check-out-cluster-logs--with-kibana-dashboard"></a>Kibana ダッシュボードを使用してクラスター ログを確認する

この記事では、[!INCLUDE[ssbigdataclusters-ss-nover](../includes/ssbigdataclusters-ss-nover.md)]内でアプリケーションを監視する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [[!INCLUDE[ssbigdataclusters-ss-nover](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)
- [azdata コマンドライン ユーティリティ](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>機能

[!INCLUDE[sssql19-md](../includes/sssql19-md.md)] では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、**azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |説明 |
|:---|:---|
|`azdata bdc endpoint list` | [!INCLUDE[ssbigdataclusters-ss-nover](../includes/ssbigdataclusters-ss-nover.md)]のエンドポイントを一覧表示します。 |


次の例を利用し、**Kibana ダッシュボード** のエンドポイントをリストアップできます。

```bash
azdata bdc endpoint list --endpoint-name logsui 
```

表示されたエンドポイントには、クラスターのユーザー名とパスワードを使用してログインできます。 

![Kibana ダッシュボード](media/big-data-cluster-monitor-cluster/kibana-dashboard-endpoint.png)


Kibana ダッシュボードへのリンク:

![Kibana ダッシュボード](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> 古い Microsoft Edge ブラウザーには、Kibana との互換性がありません。ダッシュボードを正しく表示するには、Edge chromium ベースのブラウザーを使用する必要があります。 サポートされていないブラウザーを使用してダッシュボードを読み込むと、空のページが表示されます。[Kibana でサポートされているブラウザー](https://www.elastic.co/support/matrix#matrix_browsers)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。


