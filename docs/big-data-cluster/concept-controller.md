---
title: コントローラーとは
titleSuffix: SQL Server big data clusters
description: この記事では、SQL Server ビッグ データ クラスターのコントローラーについて説明します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 70ca43a017edaa760a5ffa999f40d99516f232bb
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914349"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターのコントローラーとは

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このコントローラーでは、SQL Server ビッグ データ クラスターを展開および管理するコア ロジックがホストされます。 Kubernetes、クラスターの一部である SQL Server インスタンス、および HDFS や Spark などのその他のコンポーネントとのすべてのやり取りがここで処理されます。

コントローラー サービスには、次のコア機能があります。

- クラスターのライフサイクルの管理: クラスターのブートストラップと削除、構成の更新
- マスター SQL Server インスタンスを管理する
- コンピューティング、データ、および記憶域プールを管理する
- クラスターの状態を観察する監視ツールを公開する
- 予期しない問題を検出して修復するトラブルシューティング ツールを公開する
- クラスターのセキュリティを管理する:
  - クラスター エンドポイントを確実にセキュリティで保護する
  - ユーザーとロールを管理する
  - クラスター内通信用の資格情報を構成する

## <a name="deploying-the-controller-service"></a>コントローラー サービスを展開する

このコントローラーは、お客様がビッグ データ クラスターを構築する場合と同じ Kubernetes 名前空間で展開およびホストされます。 このサービスは、クラスターのブートストラップ中に、Kubernetes 管理者によって **azdata** コマンドライン ユーティリティを使用してインストールされます。 詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の使用を開始する](deploy-get-started.md)」を参照してください。

ビルドアウト ワークフローは、「[概要](big-data-cluster-overview.md)」の記事で説明されているすべてのコンポーネントを含む Kubernetes の完全に機能する SQL Server ビッグ データ クラスター上にレイアウトします。 ブートストラップ ワークフローでは、まずコントローラー サービスが作成されます。これが展開されると、コントローラー サービスによって、マスター、コンピューティング、データ、および記憶域プールの残りのサービス部分のインストールと構成が調整されます。

## <a name="managing-the-cluster-through-the-controller-service"></a>コントローラー サービスを使用してクラスターを管理する

いずれかの **azdata** コマンドを使用して、コントローラー サービスを介してクラスターを管理できます。 ポッドのような追加の Kubernetes オブジェクトを同じ名前空間に展開しても、コントローラー サービスによって管理または監視されません。 **kubectl** コマンドを使用して、Kubernetes レベルでクラスターを管理することもできます。 詳細については「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の監視とトラブルシューティング](cluster-troubleshooting-commands.md)」を参照してください。

ビッグ データ クラスター用に作成されたコントローラーと Kubernetes オブジェクト (ステートフル セット、ポッド、シークレットなど) は、専用の Kubernetes 名前空間に存在します。 コントローラー サービスには、その名前空間内のすべてのリソースを管理するために、Kubernetes クラスター管理者によってアクセス許可が付与されます。  このシナリオの RBAC ポリシーは、 **azdata** を使用して初期クラスター展開の一部として自動的に構成されます。

### <a name="azdata"></a>azdata

**azdata** は Python で記述されたコマンドライン ユーティリティです。これを使用すると、クラスター管理者は、コントローラー サービスによって公開されている REST API を使用して、ビッグ データ クラスターをブートストラップして管理することができます。

## <a name="controller-service-security"></a>コントローラー サービスのセキュリティ

コントローラー サービスへのすべての通信は、HTTPS 経由の REST API を介して行われます。 自己署名証明書は、ブートストラップ時に自動的に生成されます。 

コントローラー サービス エンドポイントに対する認証は、Active Directory ID を使用するか、ユーザー名とパスワードに基づいています。 これらの資格情報は、環境変数 `AZDATA_USERNAME` および `AZDATA_PASSWORD` の入力を使用して、クラスターのブートストラップ時にプロビジョニングされます。

> [!NOTE]
> [SQL Server パスワードの複雑さの要件](../relational-databases/security/password-policy.md)に準拠したパスワードを指定する必要があります。

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] の詳細については、次のリソースを参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
- [ワークショップ: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] アーキテクチャ](https://github.com/microsoft/sqlworkshops-bdc)