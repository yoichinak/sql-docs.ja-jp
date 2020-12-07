---
title: アプリケーション展開とは
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスターでアプリケーションを作成、管理、実行するためのインターフェイスがアプリケーションの展開時に提供されます。そのしくみについて説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ac26973c4d1ff8b2a9e689f3aa372d3888f939d6
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914301"
---
# <a name="what-is-application-deployment-on-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターのアプリケーション展開とは

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

アプリケーション展開は、アプリケーションを作成、管理、および実行するためのインターフェイスを提供することにより、SQL Server ビッグ データ クラスターでアプリケーションの展開を可能にします。 SQL Server ビッグ データ クラスターに展開されたアプリケーションは、クラスターの計算機能を利用し、クラスターで使用可能なデータにアクセスできます。 これにより、データが存在するアプリケーションを管理しながら、アプリケーションのスケーラビリティとパフォーマンスが向上します。 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] でサポートされているアプリケーション ランタイムは、R、Python、SSIS、MLeap です。

以降のセクションでは、アプリケーション展開のアーキテクチャと機能について説明します。

## <a name="application-deployment-architecture"></a>アプリケーション展開アーキテクチャ

アプリケーション展開は、コントローラーとアプリのランタイム ハンドラーで構成されます。 アプリケーションを作成するときに、仕様ファイル (`spec.yaml`) が提供されます。 この `spec.yaml` ファイルには、アプリケーションを正常に展開するためにコントローラーが認識する必要があるすべてのものが含まれています。 `spec.yaml` の内容例を次に示します。

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

コントローラーは、`spec.yaml` ファイル内で指定された `runtime` を検査し、対応するランタイム ハンドラーを呼び出します。 ランタイム ハンドラーによってアプリケーションが作成されます。 まず、Kubernetes ReplicaSet が作成されます。これには、それぞれに展開するアプリケーションが含まれた 1 つ以上のポッドが含まれます。 ポッドの数は、アプリケーションの `spec.yaml` ファイルで設定された `replicas` パラメーターによって定義されます。 各ポッドには、1 つ以上のプールを含めることができます。 プールの数は、`spec.yaml` ファイルの `poolsize` パラメーター セットによって定義されます。

これらの設定は、展開が並列で処理できる要求の量に影響します。 指定された時間内の要求の最大数は、`replicas` に `poolsize` を掛けた数と等しくなります。 5 つのレプリカがあり、レプリカあたり 2 つのプールがある場合、展開では 10 個の要求を並行して処理できます。 次の図は、`replicas` と `poolsize` をグラフィカルに表現したものです。

![Poolsize と replicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

ReplicaSet が作成され、ポッドが開始されると、`spec.yaml` ファイルで `schedule` が設定されている場合は、cron ジョブが作成されます。 最後に、アプリケーションの管理と実行に使用できる Kubernetes サービスが作成されます (以下を参照)。

アプリケーションが実行されると、アプリケーションの Kubernetes サービスによって、レプリカに対する要求がプロキシされ、結果が返されます。

## <a name="security-considerations-for-applications-deployments-on-openshift"></a><a id="app-deploy-security"></a> OpenShift でのアプリケーション展開のセキュリティに関する考慮事項

SQL Server 2019 CU5 により、Red Hat OpenShift でのビッグ データ クラスターの展開、および BDC の更新されたセキュリティ モデルがサポートされるため、特権コンテナーは不要になります。 SQL Server 2019 CU5 を使用するすべての新しいデプロイでは、非特権だけでなく、コンテナーも既定では非ルート ユーザーとして実行されます。

CU5 リリースの時点では、 [アプリ展開]()インターフェイスを使用して展開されたアプリケーションのセットアップ手順は、引き続き *ルート* ユーザーとして実行されます。 これは、セットアップ中に、アプリケーションで使用する追加のパッケージがインストールされるために必要です。 アプリケーションの一部として展開された他のユーザー コードは、特権の低いユーザーとして実行されます。 

また、 **CAP_AUDIT_WRITE** 機能は、cron ジョブを使用して SSIS アプリケーションをスケジュールするために必要なオプションの機能です。 アプリケーションの yaml 仕様ファイルでスケジュールが指定されている場合、アプリケーションは cron ジョブによってトリガーされるため、追加の機能が必要になります。  または、Web サービスの呼び出しを使用して *azdata app run* で必要に応じてアプリケーションをトリガーすることもできます。この場合、CAP_AUDIT_WRITE 機能は必要ありません。 

> [!NOTE]
> この機能は、ビッグ データ クラスターの既定のデプロイでは必須ではないため、[OpenShift デプロイの記事](deploy-openshift.md) のカスタム SCC には含まれていません。 この機能を有効にするには、まず、カスタム SCC yaml ファイルを更新して、CAP_AUDIT_WRITE を含める必要があります。 

```yml
...
allowedCapabilities:
- SETUID
- SETGID
- CHOWN
- SYS_PTRACE
- AUDIT_WRITE
...
```

## <a name="how-to-work-with-application-deployment"></a>アプリケーション展開を使用する方法

アプリケーション展開には、次の 2 つの主要なインターフェイスがあります。 
- [コマンド ライン インターフェイス [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](app-create.md)
- [Visual Studio Code と Azure Data Studio 拡張機能](app-deployment-extension.md)

RESTful Web サービスを使用してアプリケーションを実行することもできます。 詳細については、[ビッグ データ クラスターでのアプリケーションの使用](app-consume.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]でアプリケーションを作成して実行する方法の詳細については、次を参照してください。

- [azdata を使用してアプリケーションを展開する](app-create.md)
- [アプリケーション展開の拡張機能を使用してアプリケーションを展開する](app-deployment-extension.md)
- [ビッグ データ クラスターでアプリケーションを使用する](app-consume.md)

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、次の概要を参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)