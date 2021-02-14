---
title: Kubeadm を使用して Kubernetes を構成する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスターの展開のために、複数の Ubuntu 16.04 または18.04 マシン (物理または仮想) 上に Kubernetes を構成する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8c189f3a77f68dc212ead363b935016931b1dd6c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100038892"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>SQL Server ビッグ データ クラスターの展開のために複数のマシン上に Kubernetes を構成する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、**kubeadm** を使用して、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] の展開のために複数のコンピューター上に Kubernetes を構成する方法の例を示します。 この例では、複数の Ubuntu 16.04 または 18.04 LTS マシン (物理または仮想) を対象とします。 別の Linux プラットフォームに展開する場合は、お使いのシステムに合わせてコマンドの一部を変更する必要があります。  

> [!TIP] 
> Kubernetes を構成するサンプル スクリプトについては、「[Ubuntu 16.04 LTS または 18.04 LTS 上で Kubeadm を使用して Kubernetes クラスターを作成する](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)」を参照してください。
また、VM 上での単一ノードの kubeadm の展開を自動化して、その上にビッグ データ クラスターの既定の構成を展開するサンプル スクリプトについては、[こちら](deployment-script-single-node-kubeadm.md)のトピックを参照してください。

## <a name="prerequisites"></a>前提条件

- 最低 3 台の Linux 物理マシンまたは仮想マシン
- マシンごとに推奨される構成:
   - 8 個の CPU
   - 64 GB のメモリ
   - 100 GB のストレージ
 
> [!Important] 
> ビッグ データ クラスターの展開を開始する前に、展開の対象となっているすべての Kubernetes ノード間でクロックが同期されていることを確認します。 ビッグ データ クラスターには、時間の影響を受け、時計のずれが原因で不正な状態になる可能性があるさまざまなサービス用に、正常性プロパティが組み込まれています。

## <a name="prepare-the-machines"></a>マシンを準備する

各マシンには、必須の前提条件がいくつかあります。 bash 端末で、各マシン上で次のコマンドを実行します。

1. 現在のマシンを `/etc/hosts` ファイルに追加します。

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. すべてのデバイスでのスワップを無効にします。

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. キーをインポートし、Kubernetes 用のリポジトリを登録します。

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. マシン上に docker と Kubernetes の前提条件を構成します。

   ```bash
   KUBE_DPKG_VERSION=1.15.0-00 #or your other target K8s version, which should be at least 1.13.
   sudo apt-get update && \
   sudo apt-get install -y ebtables ethtool && \
   sudo apt-get install -y docker.io && \
   sudo apt-get install -y apt-transport-https && \
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && \
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. `net.bridge.bridge-nf-call-iptables=1` を設定します。 Ubuntu 18.04 の場合は、次のコマンドで最初に `br_netfilter` が有効にされます。

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Kubernetes マスターを構成する

各マシン上で上記のコマンドを実行した後、Kubernetes マスターにするマシンを 1 つ選択します。 その後、そのマシン上で次のコマンドを実行します。

1. まず、次のコマンドを使用して、現在のディレクトリに rbac. yaml ファイルを作成します。 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. このマシン上で Kubernetes マスターを初期化します。 次のサンプル スクリプトでは、Kubernetes バージョン `1.15.0` を指定しています。 使用するバージョンは、Kubernetes クラスターによって異なります。

   ```bash
   KUBE_VERSION=1.15.0
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

   Kubernetes マスターが正常に初期化されたことを示す出力が表示されます。

1. Kubernetes クラスターに参加するために、他のサーバー上で使用する必要がある `kubeadm join` コマンドに注意してください。 後で使用するために、これをコピーします。

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. ホーム ディレクトリに Kubernetes 構成ファイルを設定します。

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. クラスターと Kubernetes ダッシュボードを構成します。

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Kubernetes エージェントを構成する

他のマシンは、クラスターでの Kubernetes エージェントとして機能します。 

他の各マシン上で、前のセクションでコピーした `kubeadm join` コマンドを実行します。

![kubeadm join エージェント](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>クラスターの状態を表示する

クラスターへの接続を確認するには、クラスター ノードの一覧を返す [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) コマンドを使用します。

```bash
kubectl get nodes
```

## <a name="next-steps"></a>次のステップ

この記事の手順では、複数の Ubuntu マシン上に Kubernetes クラスターを構成しました。 次のステップとして、SQL Server 2019 ビッグ データ クラスターを展開します。 手順については、次の記事を参照してください。

[Kubernetes 上に SQL Server を展開する](deployment-guidance.md#deploy)
