---
title: azdata を使用してアプリケーションを実行する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスターで azdata を利用し、アプリケーションを実行する
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 13639627081a9bb9cb1309bcd0793653c7900ac8
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257272"
---
# <a name="run-apps-with-azdata---sql-server-big-data-clusters"></a>azdata でアプリを実行する - SQL Server ビッグ データ クラスター

この記事では、SQL Server ビッグ データ クラスター内でアプリケーションを実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>機能

SQL Server 2019 では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、**azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |説明 |
|:---|:---|
|`azdata app describe` | アプリケーションについて記述します。 |
|`azdata app run` | アプリケーションを実行します。 |


以下のセクションでは、これらのコマンドについて詳しく説明します。


## <a name="run-an-app"></a>アプリを実行する

アプリが `Ready` 状態の場合は、それを使用するには、指定された入力パラメーターを使用して実行します。 次の構文を使用してアプリを実行します。

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

run コマンドについて、次のコマンド例を示します。

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

実行が成功した場合は、アプリの作成時に指定した出力が表示されます。 次の出力は例です。

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```


## <a name="describe-an-app"></a>アプリの説明

describe コマンドでは、クラスター内のエンドポイントを含め、アプリに関する詳細情報が提供されます。 通常、これは、アプリ開発者が swagger クライアントを使用してアプリを構築するときや、Web サービスを使用して RESTful 方式でアプリと対話するときに使用されます。 詳細については、[ビッグ データ クラスターでアプリケーションを使用する](app-consume.md)方法に関するページを参照してください。

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
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
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

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]に展開されているアプリを独自のアプリケーションに統合する方法の詳細については、[ビッグ データ クラスター上でのアプリケーションの使用](app-consume.md)に関するページを参照してください。 その他のサンプルにはついては、[アプリの展開サンプル](https://aka.ms/sql-app-deploy)に関するページを参照してください。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。