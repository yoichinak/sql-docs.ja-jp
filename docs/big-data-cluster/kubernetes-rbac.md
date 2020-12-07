---
title: Kubernetes RBAC
titleSuffix: SQL Server big data clusters
description: この記事では、SQL Server ビッグ データ クラスターで RBAC と Kubernetes がどのように使用されるかについて説明します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 315752ffc775aa1db1970e3fef5c807e0f8e1708
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257133"
---
# <a name="kubernetes-rbac-model--impact-on-users-and-service-accounts-managing-bdc"></a>Kubernetes RBAC モデルと BDC を管理するユーザーおよびサービス アカウントへの影響

この記事では、ビッグ データ クラスターと既定のサービス アカウントのセマンティクスを管理するユーザーのアクセス許可要件と、ビッグ データ クラスター内からの Kubernetes アクセスについて説明します。

> [!NOTE]
> Kubernetes RBAC モデルのその他のリソースについては、「[Using RBAC Authorization - Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)」 (RBAC 承認の使用 - Kubernetes) と「[Using RBAC to define and apply permissions - OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html)」 (RBAC を使用してアクセス許可を定義および適用する - OpenShift) を参照してください。

## <a name="role-required-for-deployment"></a>デプロイに必要なロール

BDC では、サービス アカウント (`sa-mssql-controller` や `master` など) を使用して、クラスター ポッド、サービス、高可用性、監視などのプロビジョニングを調整します。BDC のデプロイが開始されると (たとえば、`azdata bdc create`)、[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] によって以下が行われます。

1. 指定された名前空間が存在するかどうかが確認されます。
2. 存在しない場合は作成され、`MSSQL_CLUSTER` ラベルが適用されます。
3. `sa-mssql-controller` サービス アカウントが作成されます。
4. クラスター レベルのアクセス許可ではなく、名前空間またはプロジェクトに対する完全なアクセス許可を持つ `<namespaced>-admin` ロールが作成されます。
5. そのロールに対して、そのサービス アカウントのロールの割り当てが作成されます。

これらの手順が完了すると、コントロール プレーン ポッドがプロビジョニングされ、サービス アカウントによって残りのビッグ データ クラスターがデプロイされます。  

そのため、デプロイするユーザーには次のアクセス許可が必要です。

- クラスター内の名前空間を一覧表示する (1)。
- 新規または既存の名前空間にラベルを適用する (2)。
- サービス アカウント `sa-mssql-controller`、`<namespaced>-admin` ロールおよびロール バインディングを作成する (3-5)。

既定の `admin` ロールにはこれらのアクセス許可がないため、ビッグ データ クラスターをデプロイするユーザーには、少なくとも名前空間レベルの管理者アクセス許可が必要です。

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>ポッドとノードのメトリック コレクションに必要なクラスターのロール

SQL Server 2019 CU5 以降、ポッドとノードのメトリックを収集するには、Telegraf にクラスター全体のロール アクセス許可を持つサービス アカウントが必要です。 デプロイ (または既存のデプロイのアップグレード) 時に、必要なサービス アカウントとクラスターのロールの作成が試行されます。ただし、クラスターをデプロイしたり、アップグレードを実行したりするユーザーに十分なアクセス許可がない場合でも、デプロイまたはアップグレードは警告は生成されますが続行され、成功します。 この場合、ポッドとノードのメトリックは収集されません。 クラスターをデプロイするユーザーは、(デプロイまたはアップグレードの前または後に) クラスター管理者にロールとサービス アカウントの作成を依頼する必要があります。 それらが作成されると、BDC によって使用されます。 

必要な成果物を作成する方法を表示する手順は次のようになります。

1. 以下の内容を含む *metrics-role.yaml* ファイルを作成します。 *<clusterName>* プレースホルダーをビッグ データ クラスターの名前に置き換えます。

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: <clusterName>:cr-mssql-metricsdc-reader
   rules:
   - apiGroups:
     - '*'
     resources:
     - pods
     - nodes/stats
     verbs:
     - get
   ---
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRoleBinding
   metadata:
     name: <clusterName>:crb-mssql-metricsdc-reader
   roleRef:
     apiGroup: rbac.authorization.k8s.io
     kind: ClusterRole
     name: <clusterName>:cr-mssql-metricsdc-reader
   subjects:
   - kind: ServiceAccount
     name: sa-mssql-metricsdc-reader
     namespace: <clusterName>
   ```

2. クラスター ロールとクラスター ロールのバインドを作成します。

   ```bash
   kubectl create -f metrics-role.yaml
   ```

サービス アカウント、クラスター ロール、およびクラスター ロールのバインドは、BDC デプロイの前または後に作成できます。 Kubernetes によって、Telegraf サービス アカウントのアクセス許可が自動的に更新されます。 これらがポッドのデプロイとして作成されている場合、ポッドとノードのメトリックが収集されるまでに数分の遅延が発生します。

> [!NOTE]
> SQL Server 2019 CU5 では、ポッドとノードのメトリックのコレクションを制御する 2 つの機能スイッチが導入されました。 既定では、これらのパラメーターは、既定値がオーバーライドされている OpenShift を除き、すべての環境ターゲットで true に設定されています。 

これらの設定は、`control.json` デプロイ構成ファイルのセキュリティ セクションでカスタマイズできます。

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

これらの設定が `false` に設定されている場合、BDC デプロイのワークフローでは、サービス アカウント、クラスター ロール、および Telegraf のバインディングの作成が試行されます。

## <a name="default-service-account-usage-from-within-a-bdc-pod"></a>BDC ポッド内からの既定のサービス アカウントの使用

より厳密なセキュリティ モデルのために、SQL Server 2019 CU5 では、BDC ポッド内における既定の Kubernetes サービス アカウント用の既定の資格情報によるマウントが無効になりました。 これは、CU5 以降のバージョンで、新しいデプロイとアップデートされたデプロイの両方に適用されます。
ポッド内の資格情報トークンを使用し、Kubernetes API サーバーにアクセスできます。アクセス許可のレベルは、Kubernetes 承認ポリシー設定によって異なります。 特定の用途で以前の CU5 動作に戻す必要がある場合、CU6 では、デプロイ時にのみ自動マウントをオンにできる新しい機能スイッチが導入されています。 これを行うには、control.json 構成デプロイ ファイルを使用し、 *automountServiceAccountToken* を *true* に設定します。 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] を使用して次のコマンドを実行し、 *control.json* カスタム構成ファイル内のこの設定を更新します。 

``` bash
azdata bdc config replace -c custom-bdc/control.json -j "$.security.automountServiceAccountToken=true"
```
