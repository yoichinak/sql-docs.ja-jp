---
title: Kibana ダッシュボードを使用してクラスター ログを確認する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスター上で Kibana ダッシュボードを使用したクラスターの監視。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 66b405f020728c0ed7040a712d56bcadc3180e38
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378415"
---
# <a name="check-out-cluster-logs--with-kibana-dashboard"></a>Kibana ダッシュボードを使用してクラスター ログを確認する

この記事では、SQL Server ビッグ データ クラスター内でアプリケーションを監視する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)
- [azdata コマンドライン ユーティリティ](deploy-install-azdata.md)

## <a name="capabilities"></a>機能

SQL Server 2019 では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、 **azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |説明 |
|:---|:---|
|`azdata bdc endpoint list` | ビッグ データ クラスターのエンドポイントを一覧表示します。 |


次の例を利用し、 **Kibana ダッシュボード** のエンドポイントをリストアップできます。

```bash
azdata bdc endpoint list --endpoint-name logsui 
```

表示されたエンドポイントには、クラスターのユーザー名とパスワードを使用してログインできます。 

![Kibana ダッシュボード](media/big-data-cluster-monitor-cluster/kibana-dashboard-endpoint.png)


Kibana ダッシュボードへのリンク:

![Kibana ダッシュボード](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> 古い Microsoft Edge ブラウザー ios と Kibana との互換性がありません。ダッシュボードを正しく表示するには、chromium ベースのブラウザーを使用する必要があります。 サポートされていないブラウザーを使用してダッシュボードを読み込むと、空のページが表示されます。 Kibana.rs でサポートされるブラウザーについては、こちらを参照してください。

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
