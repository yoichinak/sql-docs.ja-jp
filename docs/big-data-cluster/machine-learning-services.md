---
title: Machine Learning Services (Python、R)
titleSuffix: SQL Server Big Data Clusters
description: Machine Learning Services を使用して SQL Server ビッグ データ クラスターのマスター インスタンスで Python や R のスクリプトを実行する方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 11/19/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: aa71450a1c16c9239a0dc74403a1989b5a9a1986
ms.sourcegitcommit: ce15cbbcb0d5f820f328262ff5451818e508b480
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94947967"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>SQL Server ビッグ データ クラスターで Machine Learning Services を使用して Python および R のスクリプトを実行する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[Machine Learning Services](../machine-learning/index.yml) を使用して [SQL Server ビッグ データ クラスター](big-data-cluster-overview.md)のマスター インスタンスで Python や R のスクリプトを実行できます。

> [!NOTE]
> また、[Java 言語拡張機能](../language-extensions/java-overview.md)を使用して、SQL Server ビッグ データ クラスターのマスター インスタンスで Java コードを実行することもできます。 以下の手順に従うと、[SQL Server言語拡張機能](../language-extensions/language-extensions-overview.md)も有効になります。

## <a name="enable-machine-learning-services"></a>Machine Learning Services を有効にする

Machine Learning Services は、既定ではビッグ データ クラスターにインストールされるため、個別のインストールは必要ありません。

Machine Learning Services を有効にするには、マスター インスタンスで次のステートメントを実行します。

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

ビッグ データ クラスターのマスター インスタンスで、Python および R のスクリプトを実行する準備ができました。 初めてスクリプトを実行する場合は、「[次のステップ](#next-steps)」の下のクイックスタートを参照してください。

>[!NOTE]
>可用性グループ リスナー接続で構成設定を設定することはできません。 ビッグ データ クラスターが高可用性で展開されている場合は、レプリカごとに `external scripts enabled` を設定します。 「[クラスターで高可用性を有効にする](#enable-on-cluster-with-high-availability)」を参照してください。

## <a name="enable-on-cluster-with-high-availability"></a>クラスターで高可用性を有効にする

[高可用性で SQL Server ビッグ データ クラスターを展開する](deployment-high-availability.md)と、その展開によってマスター インスタンスの可用性グループが作成されます。 Machine Learning Services を有効にするには、可用性グループの各インスタンスに `external scripts enabled` を設定します。 ビッグ データ クラスターの場合は、SQL Server マスター インスタンスの各レプリカで `sp_configure` を実行する必要があります。

次のセクションでは、各インスタンスで外部スクリプトを有効にする方法について説明します。

### <a name="create-an-external-load-balancer-for-each-instance"></a>各インスタンスに対して外部ロード バランサーを作成する

可用性グループの各レプリカに対して、インスタンスへの接続を許可するロード バランサーを作成します。 

`kubectl expose pod <pod-name> --port=<connection port number> --name=<load-balancer-name> --type=LoadBalancer -n <kubernetes namespace>`

この記事の例では、次の値を使用します。

- `<pod-name>`: `master-#`
- `<connection port number>`: `1533`
- `<load-balancer-name>`: `mymaster-#`
- `<kubernetes namespace>`: `mssql-cluster`

ご利用の環境に合わせて次のスクリプトを更新して、コマンドを実行します。

```bash
kubectl expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer -n mssql-cluster 
kubectl expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer -n mssql-cluster
kubectl expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer -n mssql-cluster 
```

`kubectl` によって次の出力が返されます。

```bash
service/mymaster-0 exposed
service/mymaster-1 exposed
service/mymaster-2 exposed
```

各ロード バランサーは、マスター レプリカのエンドポイントです。

### <a name="enable-script-execution-on-each-replica"></a>各レプリカでスクリプトの実行を有効にする

1. マスター レプリカ エンドポイントの IP アドレスを取得します。

   次のコマンドは、レプリカ エンドポイントの外部 IP アドレスを返します。 

   `kubectl get services <load-balancer-name> -n <kubernetes namespace>`

   このシナリオで各レプリカの外部 IP アドレスを取得するには、次のコマンドを実行します。

   ```bash
   kubectl get services mymaster-0 -n mssql-cluster
   kubectl get services mymaster-1 -n mssql-cluster
   kubectl get services mymaster-2 -n mssql-cluster
   ```

   >[!NOTE]
   > 外部 IP アドレスが使用可能になるまでに少し時間がかかることがあります。 各エンドポイントが外部 IP アドレスを返すまで、上記のスクリプトを定期的に実行します。

1. マスター レプリカ エンドポイントに接続し、スクリプトの実行を有効にします。

    次のステートメントを実行します。

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

   たとえば、`sqlcmd` を使用して上記のコマンドを実行できます。 次の例では、マスター レプリカ エンドポイントに接続し、スクリプトの実行を有効にします。 スクリプトの値を実際の環境に合わせて更新します。

   ```bash
   sqlcmd -S <IP address>,1533 -U <user name> -P <password> -Q "EXEC sp_configure 'external scripts enabled', 1; RECONFIGURE WITH OVERRIDE;"
   ```

   レプリカごとにこのステップを繰り返します。

### <a name="demonstration"></a>デモンストレーション

次の図は、このプロセスを示しています。

[![デモ](media/machine-learning-services/example-kube-enable-scripts.png "Kubernetes でのデモンストレーション対応機能")](media/machine-learning-services/example-kube-enable-scripts.png#lightbox)

ビッグ データ クラスターのマスター インスタンスで、Python および R のスクリプトを実行する準備ができました。 初めてスクリプトを実行する場合は、「[次のステップ](#next-steps)」の下のクイックスタートを参照してください。

### <a name="delete-the-master-replica-endpoints"></a>マスター レプリカ エンドポイントを削除する

Kubernetes クラスターで、各レプリカのエンドポイントを削除します。 エンドポイントは、負荷分散サービスとして Kubernetes で公開されます。

次のコマンドを実行すると、負荷分散サービスが削除されます。

`kubectl delete svc <load-balancer-name> -n mssql-cluster`

この記事の例では、次のコマンドを実行します。

```bash
kubectl delete svc mymaster-0 -n mssql-cluster
kubectl delete svc mymaster-1 -n mssql-cluster
kubectl delete svc mymaster-2 -n mssql-cluster
```

## <a name="next-steps"></a>次のステップ

+ [単純な Python スクリプトを実行する](../machine-learning/tutorials/quickstart-python-create-script.md?toc=/sql/toc.json)
+ [Python での予測モデルのトレーニングとスコア付け](../machine-learning/tutorials/quickstart-python-train-score-model.md?toc=/sql/toc.json)
+ [単純な R スクリプトを実行する](../machine-learning/tutorials/quickstart-r-create-script.md?toc=/sql/toc.json)
+ [R での予測モデルのトレーニングとスコア付け](../machine-learning/tutorials/quickstart-r-train-score-model.md?toc=/sql/toc.json)
