---
title: curl を使用して HDFS にデータを読み込む |Microsoft Docs
titleSuffix: SQL Server big data clusters
description: curl を使用して、SQL Server 2019 ビッグ データ クラスター上の HDFS にデータを読み込みます。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ae893bb1e291b244b5101ccfb2ed66bcf765f049
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866846"
---
# <a name="use-curl-to-load-data-into-hdfs-on-big-data-clusters-2019"></a>curl を使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上の HDFS にデータを読み込む

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、**curl** を使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上の HDFS にデータを読み込む方法について説明します。

## <a name="prerequisites"></a><a id="prereqs"></a> 前提条件

- [ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)

## <a name="obtain-the-service-external-ip"></a>サービスの外部 IP を取得する

WebHDFS は展開が完了すると開始され、そのアクセスは Knox を経由します。 Knox エンドポイントは、**gateway-svc-external** という Kubernetes サービスを介して公開されます。  ファイルをアップロードまたはダウンロードするために必要な WebHDFS URL を作成するには、**gateway-svc-external** サービスの外部 IP アドレスとビッグ データ クラスターの名前が必要です。 次のコマンドを実行して、**gateway-svc-external** サービスの外部 IP アドレスを取得できます。

```terminal
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<big data cluster name>` は、ここでは、展開構成ファイル内に指定したクラスターの名前です。 既定の名前は `mssql-cluster` です。

## <a name="construct-the-url-to-access-webhdfs"></a>WebHDFS にアクセスするための URL を作成する

次のように、WebHDFS にアクセスするための URL を作成できます。

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

次に例を示します。

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="authentication-with-active-directory"></a>Active Directory での認証

Active Directory でのデプロイの場合は、ネゴシエート認証で、認証パラメーターと `curl` を使用します。 

Active Directory 認証で `curl` を使用するには、次のコマンドを実行します。

```
kinit <username>
```

このコマンドによって、使用する `curl` に対して Kerberos トークンが生成されます。 次のセクションで説明するコマンドによって、`curl` の `--anyauth` パラメーターが指定されます。 ネゴシエート認証が必要な URL の場合、`curl` を使用することで、その URL に対して認証を行うためのユーザー名とパスワードではなく、生成された Kerberos トークンが自動的に検出および使用されます。

## <a name="list-a-file"></a>ファイルの一覧表示

**hdfs:///product_review_data** の下のファイルを一覧表示するには、次の curl コマンドを使用します。

```terminal
curl -i -k --anyauth -u root:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

ルートを使用しないエンドポイントの場合は、次の curl コマンドを使用します。

```terminal
curl -i -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>ローカル ファイルを HDFS に配置する

**test.csv** という新しいファイルをローカル ディレクトリから product_review_data ディレクトリに配置するには、次の curl コマンドを使用します (**Content-Type** パラメーターは必須です)。

```terminal
curl -i -L -k --anyauth -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

ルートを使用しないエンドポイントの場合は、次の curl コマンドを使用します。

```terminal
curl -i -L -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>ディレクトリを作成する

`hdfs:///` の下に **test** というディレクトリを作成するには、次のコマンドを使用します。

```terminal
curl -i -L -k --anyauth -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]
ルートを使用しないエンドポイントの場合は、次の curl コマンドを使用します。

```terminal
curl -i -L -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>次のステップ

SQL Server ビッグ データ クラスターの詳細については、「[SQL Server ビッグ データ クラスターとは](big-data-cluster-overview.md)」を参照してください。
