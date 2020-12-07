---
title: azdata を使用してアプリケーションをデプロイする
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスターに、Python または R スクリプトをアプリケーションとして展開します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e91315b5ec79c136b4d84a7fbc36a707cc3d82f
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257302"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-clusters"></a>SQL Server ビッグ データ クラスターにアプリを展開する方法

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

アプリケーションを SQL Server ビッグ データ クラスター (BDC) に展開すると、クラスターの計算機能などの多くの利点を活用できるだけでなく、クラスターで使用可能なデータにアクセスすることもできます。 アプリはデータが存在するのと同じクラスターに配置されるため、パフォーマンスが劇的に向上します。

この記事では、SQL Server ビッグ データ クラスター内でアプリケーションとして R および Python スクリプトを展開して管理する方法について説明します。

## <a name="whats-new-and-improved"></a>新機能と強化された機能

- クラスターとアプリを管理する 1 つのコマンドライン ユーティリティ。
- アプリの展開が簡単になり、さらに仕様ファイルを細かく制御できるようになりました。
- ホストされるアプリケーションの種類が増えました (SQL Server Integration Services (SSIS) と MLeap)。
- アプリケーションの展開を管理する [Visual Studio Code 拡張機能](app-deployment-extension.md)。

アプリケーションは [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] を使用してデプロイおよび管理されます。 この記事では、コマンド ラインからアプリを展開する方法の例を示します。 Visual Studio Code でこれを使用する方法については、[Visual Studio Code 拡張機能](app-deployment-extension.md)に関する記事を参照してください。

サポートされているアプリの種類は次のとおりです。

- **Python** - データ エンジニア、データ サイエンティスト、DevOps エンジニアなどのさまざまなペルソナにとって最も人気のある一般的なプログラミング言語の 1 つです。データ ラングリング、自動化、プロトタイプ作成などのさまざまなシナリオがある程度サポートされています。また、さまざまなビジネス要件に対応するために、Flask や Django などの Web 開発フレームワークと連携して機能するエンタープライズ レベルのアプリケーションのプログラミングに使用されることが増えています。  
- **R** - データ エンジニアリングおよびデータ サイエンティスト向けのもう 1 つの一般的なプログラミング言語です。 Python と比較すると、R は統計的計算やグラフィックに特化したプログラミング言語です。  
- **SQL Server Integration Services (SSIS)** - ETL パッケージを構築およびデバッグするための高パフォーマンスのデータ統合ソリューションです。データ変換サービスパッケージ ファイル形式 (DTSX) が使用されます。これは、データベース間でのデータの移行と外部データ ソースの統合の処理手順が格納された XML ベースのファイル形式です。   
- **MLeap** - 共通のシリアル化形式であり、SparkML パイプラインなどを実行およびシリアル化するために必要なすべてのものが提供されます。これを実行時に読み込んで、ほぼリアルタイムでデータの近くで ML スコアリング タスクを処理できます。  

## <a name="prerequisites"></a>前提条件

- [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>機能

SQL Server 2019 では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、 **azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |説明 |
|:---|:---|
|`azdata login` | SQL Server ビッグ データ クラスターにサインインします |
|`azdata app create` | アプリケーションを作成します。 |
|`azdata app delete` | アプリケーションを削除します。 |
|`azdata app describe` | アプリケーションについて記述します。 |
|`azdata app init` | 新しいアプリケーションのスケルトンを開始します。 |
|`azdata app list` | アプリケーションを一覧表示します。 |
|`azdata app run` | アプリケーションを実行します。 |
|`azdata app update`| アプリケーションを更新します。 |

次の例のように、`--help` パラメーターを使用してヘルプを取得できます。

```bash
azdata app create --help
```

以下のセクションでは、これらのコマンドについて詳しく説明します。

## <a name="sign-in"></a>サインイン

アプリケーションを展開または操作する前に、まず、`azdata login` コマンドを使用して SQL Server ビッグ データ クラスターにサインインします。 `controller-svc-external` サービスの外部 IP アドレス (例: `https://ip-address:30080`) を、クラスターのユーザー名とパスワードと共に指定します。

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

AKS を使用している場合は、次のコマンドを実行し、Bash または cmd ウィンドウで次のコマンドを実行することで `controller-svc-external` サービスの IP アドレスを取得します。


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubernetes-clusters-created-with-kubeadm"></a>Kubeadm で作成された Kubernetes クラスター

次のコマンドを実行して、クラスターにサインインするための IP アドレスを取得します

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app-skeleton"></a>アプリのスケルトンを作成する

**azdata app init** コマンドには、アプリの展開に必要な関連する成果物を含むスキャフォールディングが用意されています。 次の例では、次のコマンドを実行して、これを実行できる add-app を作成します。

```bash
azdata app init --name add-app --version v1 --template python
```

これにより、hello という名前のフォルダーが作成されます。  `cd` コマンドを使用してディレクトリに移動し、フォルダー内に生成されたファイルを調べることができます。 spec.yaml には、名前、バージョン、ソース コードなどのアプリが定義されています。 仕様を編集して、名前、バージョン、入力、および出力を変更することができます。

フォルダーに表示される init コマンドからの出力例を次に示します。

```
add-app.py
run-spec.yaml
spec.yaml
```

## <a name="create-an-app"></a>アプリを作成する

アプリケーションを作成するには、[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] コマンドと共に `app create` を使用します。 これらのファイルは、アプリを作成するマシンのローカルに展開されます。

ビッグ データ クラスターに新しいアプリを作成するには、次の構文を使用します。

```bash
azdata app create --spec <directory containing spec file>
```

次のコマンドは、このコマンドの例を示しています。

```bash
azdata app create --spec ./addpy
```

これは、アプリケーションが `addpy` フォルダーに格納されていることを前提としています。 このフォルダーには、`spec.yaml` というアプリケーションの仕様ファイルも含まれています。 詳細については、[アプリケーションの展開に関するページ](concept-application-deployment.md)で `spec.yaml` ファイルを参照してください。

このアプリ サンプル アプリを展開するには、`addpy` というディレクトリに次のファイルを作成します。

- `add.py`. 次の Python コードをこのファイルにコピーします。
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml`. 次のコードをこのファイルにコピーします。
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

次に、次のコマンドを実行します。

```bash
azdata app create --spec ./addpy
```

list コマンドを使用してアプリが展開されているかどうかを確認できます。

```bash
azdata app list
```

展開が完了していない場合は、次の例のように `state` に `WaitingforCreate` が表示されます。

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

展開が正常に完了すると、`state` は `Ready` 状態に変わります。

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>アプリを一覧表示する

`app list` コマンドを使用して、正常に作成されたすべてのアプリを一覧表示できます。

次のコマンドで、ビッグ データ クラスターで使用できるすべてのアプリケーションが一覧表示されます。

```bash
azdata app list
```

名前とバージョンを指定すると、その特定のアプリとその状態 (Creating または Ready) が一覧表示されます。

```bash
azdata app list --name <app_name> --version <app_version>
```

このコマンドについて次の例を示します。

```bash
azdata app list --name add-app --version v1
```

次の例のような出力が表示されます。

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="delete-an-app"></a>アプリを削除する

ビッグ データ クラスターからアプリを削除するには、次の構文を使用します。

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]に展開されているアプリをご使用のアプリケーションに統合する方法の詳細については、[ビッグ データ クラスター上でのアプリケーションの実行](app-run.md)に関するページと[ビッグ データ クラスター上のアプリケーションの使用](app-consume.md)に関するページを参照してください。 その他のサンプルにはついては、[アプリの展開サンプル](https://aka.ms/sql-app-deploy)に関するページを参照してください。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。