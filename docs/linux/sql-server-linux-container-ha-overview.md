---
title: SQL Server コンテナーの高可用性
description: SQL Server コンテナーの高可用性について説明します。 また、Kubernetes 上の SQL Server でのコンテナーのデプロイについても説明します。
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: d7e15c070b17fd0a3682f5572c9b7cd3ce2c1dee
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115655"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server コンテナーの高可用性

Kubernetes で ネイティブに SQL Server インスタンスを作成して管理します。

SQL Server を [Kubernetes](https://kubernetes.io/) によって管理される docker コンテナーにデプロイします。 Kubernetes では、クラスター ノードで障害が発生した場合に、SQL Server インスタンスを含むコンテナーを自動的に回復できます。

SQL Server 2017 では、Kubernetes にデプロイできる Docker イメージが導入されています。 Kubernetes 永続ボリューム要求 (PVC) を使用してイメージを構成できます。 Kubernetes は、コンテナー内の SQL Server プロセスをモニターします。 プロセス、ポッド、コンテナー、またはノードで障害が発生した場合、Kubernetes は自動的に別のインスタンスをブートストラップし、ストレージに再接続します。

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Kubernetes 上の SQL Server インスタンスを含むコンテナー

Kubernetes 1.6 以降では、"[*ストレージ クラス*](https://kubernetes.io/docs/concepts/storage/storage-classes/)"、"[*永続ボリューム要求*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)"、および "[*Azure ディスク ボリューム タイプ*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)" がサポートされます。 

この構成では、Kubernetes はコンテナー オーケストレーターの役割を果たします。 

![Kubernetes SQL Server クラスターの図](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

上の図で、`mssql-server` は "[*ポッド*](https://kubernetes.io/docs/concepts/workloads/pods/pod/)" 内の SQL Server インスタンス (コンテナー) です。 [レプリカ セット](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)によって、ノード障害が発生した後でポッドが自動的に復旧されます。 アプリケーションがサービスに接続します。 このケースでは、サービスは、`mssql-server` の障害後も変化しない IP アドレスがホストされているロード バランサーを表します。

Kubernetes により、クラスター内のリソースが調整されます。 SQL Server インスタンス コンテナーをホストしているノードで障害が発生すると、SQL Server インスタンスを含む新しいコンテナーがブートストラップされ、同じ永続ストレージにアタッチされます。

SQL Server 2017 以降では、Kubernetes 上のコンテナーがサポートされます。

Kubernetes にコンテナーを作成するには、「[Kubernetes に SQL Server コンテナーをデプロイする](tutorial-sql-server-containers-kubernetes.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ

SQL Server コンテナーを Azure Kubernetes Service (AKS) にデプロイするには、次の例を参照してください。
* [Docker コンテナーに SQL Server をデプロイする](./sql-server-linux-docker-container-deployment.md)
* [Kubernetes に SQL Server コンテナーをデプロイする](tutorial-sql-server-containers-kubernetes.md)