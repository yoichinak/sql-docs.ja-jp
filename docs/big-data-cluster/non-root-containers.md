---
title: 非ルート ビッグ データ クラスター コンテナー
titleSuffix: SQL Server big data clusters
description: この記事では SQL Server ビッグ データ クラスターで非ルート コンテナーを展開する方法について説明します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e74e08146ea4c92f23ba17816738122147150e7b
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257122"
---
# <a name="non-root-big-data-clusters-containers"></a>非ルート ビッグ データ クラスター コンテナー

SQL Server 2019 CU5 では、非ルート コンテナーのサポートが導入されています。 サポートされているすべてのプラットフォームで、BDC 内で実行されているすべてのコンテナー アプリケーションが既定ではルート以外のユーザーとして開始されるようにすることで、プラットフォームの実装がより安全になっています。 これらの機能は、SQL Server 2019 CU5 対応のイメージ タグを使用するすべての新しい展開で利用できます。 この変更によって CU5 BDC より前の既存の展開は影響を受けません。これらのクラスター内のアプリケーションは、ルート ユーザーとして引き続き実行されます。 

## <a name="technical-background"></a>技術的な背景

[こちらのテクニカル ホワイトペーパー](https://aka.ms/sql-bdc-openshift-security)をご確認ください。これは、非ルート ユーザーを使用して展開に対応するためのセキュリティ設計の詳細を示すものであり、ビッグ データ クラスターでの一時的なアクセス許可の昇格とは何であるかとその理由について説明しています。 そのホワイトペーパーの内容は SQL Server と Red Hat のセキュリティの専門家との共同作業で開発され、OpenShift のセキュリティ コンテキストと機能に重点を置いていますが、BDC のセキュリティの概念と設計は、サポートされているすべてのプラットフォームに適用されます。

> [!NOTE]
> CU5 リリースの時点では、[アプリ展開](concept-application-deployment.md)インターフェイスを使用して展開されたアプリケーションのセットアップ手順は、引き続き "*ルート*" ユーザーとして実行されます。 これは、セットアップ中に、アプリケーションで使用する追加のパッケージがインストールされるために必要です。 アプリケーションの一部として展開された他のユーザー コードは、特権の低いユーザーとして実行されます。 

> [!NOTE]
> クラスターは、既定の非ルート設定を使用して実行することをお勧めします。 CU5 より前の動作に戻して、BDC 内のコンテナーを `root` ユーザーとして実行する場合は、新しい機能スイッチである `allowRunAsRoot` を使用して、既定の動作をオフにすることができます。 これは展開時にのみ設定できます。 これを設定するには、`control.json` 展開構成ファイルの `security` セクションで設定を指定します。

```json
 "security": {
  …
    "allowRunAsRoot": true,
  …
}
```

> [!IMPORTANT]
> OpenShift 環境でのこの設定の変更はサポートされていません。

BDC 内のサービスが非ルート ユーザーとして実行されるようになった結果、ゲートウェイ エンドポイント経由でのサービスへの接続に使用される資格情報で `root` ユーザー名は使用されません。 ゲートウェイ エンドポイントへの接続に使用されるアプリケーションで間違った資格情報が使用されている場合、認証エラーが発生します。 ゲートウェイ エンドポイントの新しいユーザー名は、`AZDATA_USERNAME` 環境変数を通じて渡された値に基づきます。 これは、コントローラーと SQL Server エンドポイントに使用されるのと同じユーザー名です。 これは新しい展開にのみ影響し、以前のリリースのいずれかで展開された既存のビッグ データ クラスターでは引き続き `root` が使用されます。 Active Directory 認証を使用するためにクラスターがデプロイされている場合、資格情報には影響はありません。 

## <a name="use-the-latest-azure-data-studio"></a>最新の Azure Data Studio を使用する

Azure Data Studio を使用すると、ゲートウェイを介して確立した接続の資格情報の変更を透過的に処理し、オブジェクト エクスプローラーで HDFS のブラウズ エクスペリエンスを有効にしたり、ノートブックを使用して Spark ジョブを送信したりできます。 [Azure Data Studio Insiders ビルド](../azure-data-studio/download-azure-data-studio.md#download-insiders-build-of-azure-data-studio)をインストールします。 このビルドには、このユース ケースに必要な変更が含まれています。

ゲートウェイ経由でサービスにアクセスするための資格情報を提供する必要があるその他のシナリオ ([!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] でのログイン、Spark の Web ダッシュボードへのアクセスなど) では、確実に正しい資格情報が使用されるようにしてください。 CU5 より前に展開された既存のクラスターを対象とする場合は、クラスターを CU5 にアップグレードした後も、ゲートウェイへの接続には引き続きユーザー名 `root` を使用することになります。 CU5 ビルドを使用して新しいクラスターを展開する場合は、`AZDATA_USERNAME` 環境変数に対応するユーザー名を指定してログインします。

## <a name="configuration-file-switches"></a>構成ファイルのスイッチ

CU5 以降では、ポッドとノードのメトリックの収集を制御するために、2 つの新しい機能スイッチが追加されました。 Kubernetes インフラストラクチャの監視に別のソリューションを使用する場合は、`control.json` 展開構成ファイルで `allowNodeMetricsCollection` と `allowPodMetricsCollection`* を `false` に設定し、ポッドとホスト ノードに対する組み込みのメトリック収集を無効にすることができます。 

次に例を示します。 

```json
"security": {
  ...
  "allowPodMetricsCollection": true,
  "allowNodeMetricsCollection": true,
  ...
}
```

> [!NOTE]
> OpenShift 環境では、これらの設定は、組み込みの展開プロファイルでは既定では false に設定されています。 ポッドとノードのメトリックを収集するには特権機能が必要であり、OpenShift の推奨されるセキュリティ コンテキストは、"*制限された*" 制約に基づいています。

非特権コンテナーに加えて、CU5 以降では、BDC のすべての新しい展開を対象として、サポートされているすべてのプラットフォームでコンテナーは既定では非ルート ユーザーとして実行されます。 これらの機能は、SQL Server 2019 CU5 対応のイメージ タグを使用するすべての新しい展開で利用できます。 CU5 より前の既存の BDC 展開は影響を受けません。これらのクラスター内のアプリケーションは、引き続きルート ユーザーとして実行されます。

## <a name="next-steps"></a>次のステップ
[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する方法](deployment-guidance.md)

[OpenShift に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する](deploy-openshift.md)

[セキュリティに関するホワイトペーパー](https://aka.ms/sql-bdc-openshift-security)
