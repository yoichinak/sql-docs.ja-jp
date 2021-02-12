---
title: SQL Server ビッグ データ クラスターのパフォーマンスに関するベスト プラクティス
description: この記事では、Kubernetes 上で SQL Server ビッグ データ クラスターを実行する場合のパフォーマンスのベスト プラクティスおよびガイドラインを示します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7b430e09a06523bc3ee369434911738f83ab5ee4
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100044172"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-big-data-clusters"></a>SQL Server ビッグ データ クラスターのパフォーマンスに関するベスト プラクティスと構成ガイドライン

[!INCLUDE [sqlserver2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、ビッグ データ クラスター内で実行されているサービスをターゲットとするアプリケーションのパフォーマンスを最大限に高めるためのベストプラクティスと推奨事項について説明します。

次のガイドラインでは、BDC が展開される Kubernetes ワーカー ノードをホストする Linux オペレーティング システムの構成に関する推奨事項に焦点を当てています。 ベスト プラクティスとして、ビッグ データ クラスターを展開する前にチューニング プロファイルを構成しま。 提案されたチューニング プロファイルに含まれている設定は、Microsoft および Intel によって実行されたケース スタディ中に検証されたものです。 調査結果は、ダウンロードできるように公開されていて、この[ホワイトペーパー](https://aka.ms/sql-bdc-spark-perf/)に記載されています。

> [!TIP]
> SQL Server on Linux に固有のチューニング構成については、「[パフォーマンスのベスト プラクティスと SQL Server on Linux の構成ガイドライン](../linux/sql-server-linux-performance-best-practices.md)」を参照してください。 また、SQL Server データベース用のインデックス設計のようなその他のベスト プラクティスも引き続き適用されます。

## <a name="proposed-linux-settings-using-a-tuned-mssql-bdc-profile"></a>チューニングされた `mssql-bdc` プロファイルを使用した Linux 設定の提案

以下のコンテンツを使用して、**tuned.conf** 構成プロファイルを作成します。

```bash
[main]
summary=Optimize for Microsoft SQL Server Big Data Clusters TPC-DS performance
include=throughput-performance
 
[sysctl]
#network tunings
net.ipv4.conf.default.rp_filter=1
net.ipv4.tcp_timestamps=0
net.ipv4.tcp_sack = 1
net.core.netdev_max_backlog = 25000
net.core.rmem_max = 2147483647
net.core.wmem_max = 2147483647
net.core.rmem_default = 33554431
net.core.wmem_default = 33554432
net.core.optmem_max = 33554432
net.ipv4.tcp_rmem =8192 33554432 2147483647
net.ipv4.tcp_wmem =8192 33554432 2147483647
net.ipv4.tcp_low_latency=1
net.ipv4.tcp_adv_win_scale=1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv4.conf.all.arp_filter=1
net.ipv4.tcp_retries2=5
net.ipv6.conf.lo.disable_ipv6 = 1
net.core.somaxconn = 65535
 
#memory cache settings
vm.swappiness=1
vm.overcommit_memory=0
vm.dirty_background_ratio=1
 
#kernel NUMA
kernel.numa_balancing=0

#filesystem
fs.aio-max-nr=1048576
 
[vm]
#should be revisited for SQL large pages use in master/data/compute pods
transparent_hugepages=never
```

## <a name="install-tuned-utility-on-all-the-kubernetes-worker-nodes"></a>すべての Kubernetes ワーカー ノードに **tuned** ユーティリティをインストールする

**tuned** をインストールするには、次のように実行します。

```bash
apt-get -y install tuned
```

## <a name="apply-tuning-settings-to-all-kubernetes-worker-nodes"></a>すべての Kubernetes ワーカー ノードにチューニング設定を適用する

ターゲットとする各ワーカー ノード上に、前に作成した **tuned.conf** ファイルをコピーします。

```bash
cd /usr/lib/tuned
scp -r <sourcePath> ./mssql-bdc
```

このチューニングされたプロファイル **mssql-bdc** を有効にするには、それらの定義を、すべての Kubernetes ワーカー ノード上で `/usr/lib/tuned/mssql-bdc` フォルダーの下にある **tuned.conf** ファイルに保存し、以下を使用してプロファイルを有効にします

```bash
chmod +x /usr/lib/tuned/mssql-bdc/tuned.conf
tuned-adm profile mssql-bdc
```

次のコマンドを使用して、有効になっていることを確認します。

```bash
tuned-adm active
```

or

```bash
tuned-adm list
```

プロファイルが動的に変更される場合、新しい変更を有効にするには、影響を受けるすべてのワーカー ノード上で **tuned** を再起動する必要があります。

```bash
systemctl restart tuned
```
 
**tuned** サービスのログは */var/log/tuned/tuned.log* にあります。

必要に応じて、Kubernetes クラスター内の 1 つのノード上でチューニング プロファイルを構成してから、それを、以下のスクリプトを使用して残りのノードにコピーして構成することができます。

```bash
#!/bin/bash -e
# This script takes a list of servers (IPs like `cat ~administrator/workerhosts)) as input
# and update these servers with the local version of mssql-bdc tuned.conf.
 
is_root() {
    local is_root_set=0
    if [ "$EUID" -ne 0 ]; then
        echo "Please run as root"
    else
        is_root_set=1
    fi
    return "${is_root_set}"
}
 
# function main
if is_root -eq 0; then
    exit 0
fi
 
while [ $# -gt 0 ]
do
    # sometimes, people add non-breaking space characters to their *host* files.
    WORKER_IP=$(echo "$1" | sed -e 's/\xC2\xA0//g')
    echo -e "updating mssql-bdc tuned on \e[42m${WORKER_IP}\e[0m"
    # the following commands assume tuned was not set up and active...
    # TODO: add the tuned install and status checks
    ssh "${WORKER_IP}" mkdir -p /usr/lib/tuned/mssql-bdc
    scp ~administrator/tuned.conf "${WORKER_IP}":/usr/lib/tuned/mssql-bdc/tuned.conf
    ssh "${WORKER_IP}" tuned-adm profile mssql-bdc
    ssh "${WORKER_IP}" systemctl restart tuned
    ssh "${WORKER_IP}" tuned-adm active
    shift
done

```

## <a name="next-steps"></a>次のステップ

SQL Server ビッグ データ クラスターの参照アーキテクチャを含むその他のリソースについては、以下を参照してください。

* [ケース スタディ: MS SQL Server 2019 ビッグ データ クラスターの Apache Spark で実行されている SQL ワークロード](https://aka.ms/sql-bdc-spark-perf/)

* [Microsoft SQL Server 2019 ビッグ データ クラスターを使用してご利用のすべてのデータに関する分析情報を提供する HPE 参照アーキテクチャ](https://h20195.www2.hpe.com/V2/GetDocument.aspx?docname=a50001963enw)

* [Dell EMC PowerStore: SQL Server 2019 ビッグ データ クラスター](https://www.dellemc.com/resources/en-us/asset/white-papers/products/storage/h18231-dell-emc-powerstore-sql-server-big-data-clusters.pdf)

* [SQL Server 2019 ビッグ データ クラスター: Dell EMC インフラストラクチャを使用したビッグ データ ソリューション](https://infohub.delltechnologies.com/t/microsoft-sql-server-2019-big-data-clusters-a-big-data-solution-using-dell-emc-infrastructure/)

* [Cisco UCS 参照アーキテクチャ上の Microsoft SQL Server 2019 ビッグ データ クラスター](https://www.cisco.com/c/en/us/solutions/collateral/data-center-virtualization/unified-computing/sql-server-on-big-data-cluster-on-ucs.html)