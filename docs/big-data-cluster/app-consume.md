---
title: アプリケーションの使用
titleSuffix: SQL Server Big Data Clusters
description: RESTful Web サービスを使用して SQL Server ビッグ データ クラスターに展開されたアプリケーションを使用します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 307d1cf41c319debad4b0fc06b8ba0da516491bd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257322"
---
# <a name="consume-an-app-deployed-on-big-data-clusters-2019-using-a-restful-web-service"></a>RESTful Web サービスを使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]に展開されたアプリを使用する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、RESTful Web サービスを使用して SQL Server ビッグ データ クラスターに展開されたアプリを使用する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [SQL Server ビッグ データ クラスター](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)
- [azdata](app-create.md) または [App Deploy](app-deployment-extension.md) 拡張機能を使用して展開されたアプリ

> [!NOTE]
> アプリケーションの yaml 仕様ファイルでスケジュールが指定されている場合、アプリケーションは cron ジョブによってトリガーされます。 OpenShift にビッグ データ クラスターがデプロイされている場合、cron ジョブを起動するには追加の機能が必要です。 具体的な手順については、[OpenShift のセキュリティに関する考慮事項](concept-application-deployment.md#app-deploy-security)に関する記事を参照してください。

## <a name="capabilities"></a>機能

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]にアプリケーションを展開した後は、RESTful Web サービスを使用してそのアプリケーションにアクセスして使用することができます。 これにより、そのアプリを他のアプリケーションやサービス (モバイル アプリや Web サイトなど) と統合できるようになります。 次の表では、**azdata** と共に使用して、アプリの RESTful Web サービスに関する情報を取得できるアプリケーションの展開コマンドについて説明します。

|command |説明 |
|:---|:---|
|`azdata app describe` | アプリケーションについて記述します。 |

次の例のように、`--help` パラメーターを使用してヘルプを取得できます。

```bash
azdata app describe --help
```

以下のセクションでは、アプリケーションのエンドポイントを取得する方法と、アプリケーション統合のために RESTful Web サービスを使用する方法について説明します。

## <a name="retrieve-the-endpoint"></a>エンドポイントを取得する

ビッグ データ クラスター (BDC) には、RESTful Web サービスを使用してそのアプリケーションにアクセスして使用できるエンドポイントが用意されています。主な目的は、他の Web またはモバイル アプリケーションとのやり取りを容易にし、これらのマイクロサービス アーキテクチャをよりプロアクティブに利用することです。 **azdata app describe** コマンドでは、クラスター内のエンド ポイントを含め、アプリに関する詳細情報が提供されます。 通常、これは、アプリ開発者が swagger クライアントを使用してアプリを構築するときや、Web サービスを使用して RESTful 方式でアプリと対話するときに使用されます。

次の例のようなコマンドを実行して、アプリについて記述します。

```bash
azdata app describe --name add-app --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

出力の IP アドレス (この例では `10.1.1.3`) とポート番号 (`30080`) に注意してください。

この情報を取得する他の方法の 1 つとして、Azure Data Studio でサーバー上の [管理] を右クリックする方法があります。ここで、一覧表示されているサービスのエンドポイントを確認できます。

![ADS エンドポイント](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>JWT アクセス トークンを生成する

展開したアプリの RESTful Web サービスにアクセスするには、まず JWT アクセス トークンを生成する必要があります。 アクセス トークンの URL は、ビッグ データ クラスターのバージョンによって異なります。 

|Version |URL|
|------------|------|
|GDR1|  `https://[IP]:[PORT]/docs/swagger.json`|
|CU1 以降| `https://[IP]:[PORT]/api/v1/swagger.json`|

 前の例の出力である CU4 リリース、コントローラーの IP アドレス (例では 10.1.1.3)、およびポート番号 (30080) から、URL は次のようになります。 
 
 ```bash
    https://10.1.1.3 :30080/api/v1/swagger.json
```
 
> バージョン情報については、[リリース履歴](release-notes-big-data-cluster.md#release-history)に関するセクションを参照してください。

ブラウザーで、上の [`describe`](#retrieve-the-endpoint) コマンドを実行して取得した IP アドレスとポートを使用して、適切な URL を開きます。 `azdata login` に使用したものと同じ資格情報でサインインします。

`swagger.json` の内容を [Swagger エディター](https://editor.swagger.io)に貼り付けて、使用できるメソッドを確認します。

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

`app` が GET メソッドであり、`token` の取得に POST メソッドが使用されることに注目してください。 アプリの認証には JWT トークンが使用されるため、`token` メソッドへの POST 呼び出しを行うには、任意のツールを使用してトークンを取得する必要があります。 同じ例で、JWT トークンを取得するための URL は次のようになります。

 ```bash
    https://10.1.1.3 :30080/api/v1/token
```


[Postman](https://www.getpostman.com/) でこれを行う方法の例を次に示します。

![Postman トークン](media/big-data-cluster-consume-apps/postman_token.png)


この要求の出力により、JWT `access_token` を取得できます。この場合、アプリを実行するために URL を呼び出す必要があります。

## <a name="execute-the-app-using-the-restful-web-service"></a>RESTful Web サービスを使用してアプリを実行する

BDC でアプリを使用する方法は複数ありますが、[azdata app run command](app-create.md) を使用することもできます。 このセクションでは、Postman などの一般的な開発者ツールを使用してアプリを実行する方法について説明します。 

ブラウザーで `azdata app describe --name [appname] --version [version]` を実行したときに返された `swagger` の URL を開くことができます。これは、`https://[IP]:[PORT]/app/[appname]/[version]/swagger.json` に似ています。 

> [!NOTE]
> `azdata login` に使用したものと同じ資格情報を使用してログインする必要があります。 同じ例では、コマンドは次のようになります。

 ```bash
    azdata app describe --name add-app --version v1
```

`swagger.json` の内容を [Swagger エディター](https://editor.swagger.io)に貼り付けることができます。 Web サービスによって `run` メソッドが公開され、その下でユーザーを認証し、アプリケーションに要求をルーティングする Web API であるアプリケーション プロキシを経由していたことがわかります。 上部に表示されているベース URL に注目してください。 任意のツールを使用して `run` メソッド (`https://[IP]:30778/api/app/[appname]/[version]/run`) を呼び出し、json として POST 要求の本文でパラメーターを渡すことができます。 


この例では、[Postman](https://www.getpostman.com/) を使用します。 呼び出しを行う前に、`Authorization` を `Bearer Token` に設定し、前の手順で取得したトークンを貼り付ける必要があります。 これにより、要求にヘッダーが設定されます。 次のスクリーンショットを見てください。

![Postman の実行ヘッダー](media/big-data-cluster-consume-apps/postman_run_1.png)

次に、要求本文で、呼び出しているアプリにパラメーターを渡し、`content-type` を `application/json` に設定します。

![Postman の実行本文](media/big-data-cluster-consume-apps/postman_run_2.png)

要求を送信すると、`azdata app run` を介してアプリを実行したときと同じ出力が得られます。

![Postman の実行結果](media/big-data-cluster-consume-apps/postman_result.png)

これで、Web サービスを介してアプリが正常に呼び出されるようになりました。 同様の手順に従って、この Web サービスをアプリケーションに統合することができます。


## <a name="next-steps"></a>次のステップ

[ビッグ データ クラスターでのアプリケーションの監視](app-monitor.md)方法について確認します。 その他のサンプルにはついては、[アプリの展開サンプル](https://aka.ms/sql-app-deploy)に関するページを参照してください。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。