---
title: Kubernetes でのデータ永続化
titleSuffix: SQL Server big data clusters
description: 永続ボリュームでは、Kubernetes のストレージ向けのプラグイン モデルが提供されます。そのしくみについて説明します。 SQL Server 2019 ビック データ クラスターのデータ永続化のしくみについても説明します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 563dc8fbbb7f866dd91f7a982813fe2e5b0a2e83
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907360"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-in-kubernetes"></a>Kubernetes の SQL Server ビッグ データ クラスターでのデータ永続化

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[永続ボリューム](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)では、Kubernetes のストレージ向けのプラグイン モデルが提供されます。 このモデルでは、ストレージの提供方法は、その使用方法から抽象化されます。 そのため、独自の高可用性ストレージを利用して、SQL Server ビッグ データ クラスターに接続できます。 これにより、必要としているストレージの種類、可用性、およびパフォーマンスを完全に制御できます。 Kubernetes では、Azure ディスクとファイル、ネットワーク ファイル システム (NFS)、ローカル ストレージなどの[さまざまな種類のストレージ ソリューション](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner)がサポートされます。

## <a name="configure-persistent-volumes"></a>永続ボリュームを構成する

SQL Server ビッグ データ クラスターでは、[ストレージ クラス](https://kubernetes.io/docs/concepts/storage/storage-classes/)を利用してこれらの永続ボリュームが使用されます。 異なるストレージの種類に対して異なるストレージ クラスを作成し、ビッグ データ クラスターの展開時に指定できます。 特定の目的に使用するストレージ クラスと永続ボリューム要求のサイズをプール レベルで構成できます。 SQL Server ビッグ データ クラスターでは、永続ボリュームを必要とするコンポーネントごとに指定したストレージ クラス名を使って、[永続ボリューム要求](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)が作成されます。 その後、ポッド内で該当の 1 つの永続ボリューム (または複数のボリューム) がマウントされます。 

ここでは、ビッグ データ クラスターのストレージ構成を計画する際に考慮する重要な事項について説明します。

- ビッグ データ クラスターの展開を成功させるには、必要な数の永続ボリュームが使用可能であることを確認する必要があります。 Azure Kubernetes Service (AKS) クラスターに展開していて、組み込みのストレージ クラス (`default` または `managed-premium`) を使用している場合、このクラスでは永続ボリュームの動的プロビジョニングがサポートされます。 そのため、永続ボリュームを事前に作成する必要はありませんが、AKS クラスター内で使用可能なワーカー ノードが、展開に必要な永続ボリュームと同じ数のディスクを接続できることを確認する必要があります。 ワーカー ノードに対して指定されている [VM サイズ](/azure/virtual-machines/linux/sizes)によっては、各ノードが特定の数のディスクを接続できます。 既定のサイズのクラスター (高可用性なし) の場合は、少なくとも 24 個のディスクが必要です。 高可用性を有効にする場合、またはプールをスケール アップする場合は、スケール アップするリソースに関係なく、追加のレプリカごとに少なくとも 2 つの永続化ボリュームを確保する必要があります。

- 構成内で指定しているストレージ クラスのストレージ プロビジョナーによって動的プロビジョニングがサポートされていない場合は、永続化ボリュームを事前に作成する必要があります。 たとえば、`local-storage` プロビジョナーでは動的プロビジョニングが有効になりません。 `kubeadm` を使用して展開された Kubernetes クラスター内での作業の進め方に関するガイダンスについては、この[サンプル スクリプト](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)を参照してください。

- ビッグ データ クラスターを展開するときに、クラスター内のすべてのコンポーネントで使用する、同一のストレージ クラスを構成できます。 ただし、運用環境での展開のベスト プラクティスとして、さまざまなコンポーネントでは、サイズやスループットに関してさまざまなワークロードに対応するために、異なるストレージ構成が必要になります。 コントローラーで指定されている既定のストレージ構成は、SQL Server マスター インスタンス、データセット、および記憶域プールごとに上書きできます。 この記事では、これを行う方法の例を示します。

- 記憶域プールのサイズ要件を計算するときは、HDFS の構成に使用されているレプリケーション係数を考慮する必要があります。  レプリケーション係数は、展開時にクラスター展開構成ファイルで構成できます。 開発テスト プロファイル (つまり、`aks-dev-test` または `kubeadm-dev-test`) の既定値は 2 で、運用環境のデプロイに推奨されるプロファイル (つまり `kubeadm-prod`) の既定値は 3 です。 ベスト プラクティスとして、3 以上の HDFS のレプリケーション係数を使用して、ビッグ データ クラスターの運用環境の展開を構成することをお勧めします。 レプリケーション係数の値は、記憶域プール内のインスタンスの数に影響します。少なくとも、レプリケーション係数の値と同じ数の記憶域プール インスタンスを展開する必要があります。 また、ストレージのサイズを適切に変更し、レプリケーション係数の値と同じ回数だけ HDFS でデータがレプリケートされるように構成する必要があります。 HDFS でのデータ レプリケーションの詳細については、[こちら](https://hadoop.apache.org/docs/r3.2.1/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Data_Replication)を参照してください。 

- SQL Server 2019 CU1 リリースの時点で、BDC では、展開後にストレージ構成設定を更新するエクスペリエンスを使用できません。 この制約があるため、BDC 操作を使用して、展開後に各インスタンスの永続ボリューム要求のサイズ変更や、プールのスケーリングを行うことはできません。 そのため、ビッグ データ クラスターを展開する前に、ストレージのレイアウトを計画することが非常に重要です。 ただし、Kubernetes API を直接使用して永続ボリューム サイズを拡張することができます。 この場合、BDC メタデータは更新されず、構成クラスター メタデータのボリューム サイズに関する不整合が表示されます。

- Kubernetes にコンテナー化されたアプリケーションとして展開し、ステートフル セットや永続ストレージなどの機能を使用することにより、Kubernetes では、正常性の問題が発生した場合にポッドが再起動され、同じ永続ストレージに接続されるようになります。 ただし、ノードで障害が発生し、ポッドを別のノードで再起動する必要がある場合は、ストレージが障害ノードに対してローカルであると、使用できなくなるリスクが高くなります。 このリスクを減らすには、追加の冗長性を構成し、[高可用性機能](deployment-high-availability.md)を有効にするか、リモート冗長ストレージを使用する必要があります。 ここでは、ビッグ データ クラスター内のさまざまなコンポーネントのストレージ オプションの概要について説明します。

| リソース | データのストレージの種類 | ログのストレージの種類 |  Notes |
|---|---|---|--|
| SQL Server マスター インスタンス | ローカル (レプリカ > = 3) またはリモート冗長ストレージ (レプリカ = 1) | ローカル ストレージ | ステートフル セット ベースの実装であり、この場合、ノードに対して維持されるポッドの再起動が確実に行われ、一時的なエラーによってデータ損失が発生しません。 |
| 計算プール | ローカル ストレージ | ローカル ストレージ | ユーザー データが格納されていません。 |
| データ プール | ローカル/リモート冗長ストレージ | ローカル ストレージ | データ プールを他のデータ ソースから再構築できない場合は、リモート冗長ストレージを使用します。  |
| 記憶域プール (HDFS) | ローカル/リモート冗長ストレージ | ローカル ストレージ | HDFS レプリケーションが有効になっている場合。 |
| Spark プール | ローカル ストレージ | ローカル ストレージ | ユーザー データが格納されていません。 |
| コントロール (controldb、metricsdb、logsdb)| リモート冗長ストレージ | ローカル ストレージ | ビッグ データ クラスターのメタデータにストレージ レベルの冗長性を使用することが重要です。 |

> [!IMPORTANT]
> 制御関連コンポーネントがリモート冗長ストレージ デバイス上にあることを確認してください。 `controldb-0` ポッドは、クラスター サービスの状態、さまざまな設定、その他の関連情報に関するすべてのメタデータを格納するデータベースを使用して、SQL Server インスタンスをホストします。 このインスタンスが使用できなくなると、クラスター内の他の依存サービスに正常性の問題が生じます。

## <a name="configure-big-data-cluster-storage-settings"></a>ビッグ データ クラスターのストレージ設定を構成する

他のカスタマイズと同様に、`bdc.json` 構成ファイル内の各プールと `control.json` ファイル内のコントロール サービスに対して、展開時にクラスター構成ファイル内にストレージの設定を指定できます。 プールの仕様にストレージ構成設定がない場合は、SQL Server マスター (`master` リソース)、HDFS (`storage-0` リソース)、データ プール コンポーネントなど、他のすべてのコンポーネントに対してコントロールのストレージ設定が使用されます。 次のコード サンプルは、仕様に含めることができるストレージ構成セクションを表しています。

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

ビッグ データ クラスターの展開では、永続ストレージを使用して、さまざまなコンポーネントに関するデータ、メタデータ、およびログが格納されます。 展開の一部として作成された永続ボリューム要求のサイズをカスタマイズできます。 ベスト プラクティスとして、 *Retain* [再要求ポリシー](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)によってストレージ クラスを使用することをお勧めします。

> [!WARNING]
> 永続ストレージを使用せずに実行すると、テスト環境内では動作しますが、クラスターが機能しなくなる可能性があります。 ポッドの再起動時には、クラスターのメタデータやユーザー データが完全に失われます。 この構成での実行はお勧めしません。

[ストレージの構成](#config-samples)に関するセクションで、SQL Server ビッグ データ クラスターの展開に対するストレージ設定の構成方法の例をさらに紹介しています。

## <a name="aks-storage-classes"></a>AKS のストレージ クラス

AKS には、対応する動的プロビジョナーを備えた [2 つの組み込みのストレージ クラス](/azure/aks/azure-disks-dynamic-pv/)である `default` と `managed-premium` が付属しています。 そのうちどちらかを指定するか、または、独自のストレージ クラスを作成して、永続ストレージが有効になったビッグ データ クラスターを展開できます。 既定では、AKS の `aks-dev-test` に対する組み込みのクラスター構成ファイルは、`default` ストレージ クラスを使用する永続ストレージ構成を備えています。

> [!WARNING]
> 組み込みのストレージ クラスである `default` および `managed-premium` によって作成された永続ボリュームには、 *Delete* の再要求ポリシーが用意されています。 そのため、SQL Server ビッグ データ クラスターを削除すると、永続ボリューム要求は、永続ボリュームと同様に削除されます。 [ストレージの概念](/azure/aks/concepts-storage/#storage-classes)に関する記事に示すように、`Retain` 再要求ポリシーによって `azure-disk` プロビジョナーを使用して、カスタム ストレージ クラスを作成できます。

## <a name="storage-classes-for-kubeadm-clusters"></a>`kubeadm` クラスターのストレージ クラス 

`kubeadm` を使用して展開された Kubernetes クラスターには、組み込みのストレージ クラスはありません。 ローカル ストレージまたは[推奨のストレージ プロビジョナー](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner)を使用して、独自のストレージ クラスと永続ボリュームを作成する必要があります。 その場合は、構成したストレージ クラスに `className` を設定します。

> [!IMPORTANT]
>  kubeadm 用の組み込みの展開構成ファイル (`kubeadm-dev-test` または `kubeadm-prod`) では、データおよびログのストレージ用のストレージ クラス名は指定されていません。 展開の前に、構成ファイルをカスタマイズして `className` に値を設定する必要があります。 そうしないと、展開前の検証でエラーになります。 また、展開には、ストレージ クラスの存在について確認する検証手順が含まれますが、必要な永続ボリュームについては含まれません。 クラスターのスケールに応じた十分なボリュームを確実に作成しておく必要があります。 既定の最小クラスター サイズ (既定のスケール、高可用性なし) では、少なくとも 24 個の永続ボリュームを作成する必要があります。 ローカル プロビジョナーを利用した永続ボリュームの作成方法を示す例については、[Kubeadm を使用した Kubernetes クラスターの作成](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu)に関する記事を参照してください。

## <a name="customize-storage-configurations-for-each-pool"></a>各プール用のストレージ構成をカスタマイズする

すべてのカスタマイズにおいて、使用する組み込みの構成ファイルのコピーを最初に作成しておく必要があります。 たとえば、次のコマンドでは、`aks-dev-test` 展開構成ファイルのコピーが `custom` という名前のサブディレクトリに作成されます。

```bash
azdata bdc config init --source aks-dev-test --target custom
```

このプロセスでは `bdc.json` と `control.json` の 2 つのファイルが作成されます。これらは、手動で編集するか `azdata bdc config` コマンドを使用することによってカスタマイズできます。 jsonpath および jsonpatch ライブラリを組み合わせて使用すると、構成ファイルを編集する手段を提供できます。


### <a name="configure-storage-class-name-andor-claims-size"></a><a id="config-samples"></a>ストレージ クラス名および要求サイズを構成する

既定では、クラスター内にプロビジョニングされた各ポッドに対応する、プロビジョニングされた永続ボリューム要求のサイズは、10 ギガバイト (GB) です。 この値は、クラスターの展開前にカスタム構成ファイル内で実行しているワークロードに合わせて更新できます。

次の例では、`control.json` 内で永続ボリューム要求のサイズが 32 GB に更新されています。 プール レベルで上書きされない場合、この設定はすべてのプールに適用されます。

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

次の例は、`control.json` ファイルでのストレージ クラスの変更方法を示しています。

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

また、カスタム構成ファイルを手動で編集したり、次の例にあるように .json パッチを使用して Storage プールに対するストレージ クラスを変更したりするオプションもあります。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

パッチ ファイルを適用します。 `azdata bdc config patch` コマンドを使用して、.json パッチ ファイルでの変更を適用します。 次の例では、`patch.json` ファイルをターゲットの展開構成ファイルである `custom.json` に適用します。

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>次のステップ

- Kubernetes でのボリュームに関する詳細なドキュメントについては、[ボリュームに関する Kubernetes ドキュメント](https://kubernetes.io/docs/concepts/storage/volumes/)を参照してください。

- SQL Server ビッグ データ クラスターの展開の詳細については、「[Kubernetes に SQL Server ビッグ データ クラスターを展開する方法](deployment-guidance.md)」を参照してください。
