---
title: Docker にインストールする
titleSuffix: SQL Server Machine Learning Services
description: Docker に SQL Server Machine Learning Services (Python と R) をインストールする方法を説明します。
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/11/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e53acfa9e0fdfb7f7ee9b1ab6b7de5cd43ba8a9d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870040"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Docker に SQL Server Machine Learning Services (Python と R) をインストールする

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

この記事では、Docker に SQL Server Machine Learning Services をインストールする方法について説明します。 Machine Learning Services を使用して、データベース内で Python または R スクリプトを実行できます。 Machine Learning Services には、事前に構築されたコンテナーは用意されていません。 [GitHub で入手できるテンプレートの例](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)使用して、SQL Server コンテナーから作成できます。

## <a name="prerequisites"></a>前提条件

- Git のコマンド ライン インターフェイス。

- サポートされているいずれかの Linux ディストリビューションの Docker エンジン 1.8 以降 または Mac/Windows 用 Docker。 詳細については、「[Get Docker](https://docs.docker.com/get-docker/)」を参照してください。

- 「[SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)」も参照してください。

## <a name="clone-the-mssql-docker-repository"></a>mssql-docker リポジトリをクローンする

次のコマンドによって `mssql-docker` git リポジトリがローカル ディレクトリにクローンされます。

1. Linux または Mac で Bash ターミナルを開きます。

2. mssql-docker リポジトリのローカル コピーを保持するディレクトリを作成します。

3. git clone コマンドを実行して、mssql-docker リポジトリを複製します。

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>SQL Server の Linux コンテナー イメージをビルドする

次の手順で Docker イメージをビルドします。

1. ディレクトリを mssql-mlservices ディレクトリに変更します。
    
    ```bash
    /mssql-docker/linux/preview/examples/mssql-mlservices
    ```

2. 同じディレクトリで、次のコマンドを実行します。

    ```bash
    docker build -t mssql-server-mlservices .
    ```

3. 次のコマンドを実行します。

    ```bash
    docker run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=<password> -v <directory on the host OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```
  
    > [!NOTE]
    > MSSQL_PID の値には、次の値のいずれかを使用できます:Developer (無料)、Express (無料)、Enteprise (有料)、Standard (有料)。 有料エディションを使用している場合は、ライセンスを購入していることを確認してください。 (パスワード) は、実際のパスワードで置き換えてください。 -v を使用したボリューム マウントはオプションです。 (ホスト OS 上のディレクトリ) は、データベース データとログ ファイルをマウントする実際のディレクトリに置き換えてください。
    

4. 次のコマンドを実行して確認します。

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > Docker イメージをビルドするには、サイズが数 GB のパッケージをいくつかインストールする必要があります。 このスクリプトは、ネットワークの帯域幅によっては完了までに時間がかかることがあります。

## <a name="run-the-sql-server-linux-container-image"></a>SQL Server Linux コンテナー イメージを実行する

1. コンテナーを実行する前に環境変数を設定します。 PATH_TO_MSSQL 環境変数をホスト ディレクトリに設定します。

   ```bash
   export MSSQL_PID='Developer'
   export ACCEPT_EULA='Y'
   export ACCEPT_EULA_ML='Y'
   export PATH_TO_MSSQL='/home/mssql/'
   ```
  
   > [!NOTE]
   > SQL Server の実稼働エディションをコンテナーで実行するプロセスは、若干異なります。 詳細については、「[Docker で SQL Server コンテナーイメージを構成する](./sql-server-linux-docker-container-deployment.md)」を参照してください。 同じコンテナー名とポートを使う場合でも、このチュートリアルの残りの部分を引き続き実稼働のコンテナーに適用できます。

2. Docker コンテナーを表示するには、`docker ps` コマンドを実行します。

   ```bash
   sudo docker ps -a
   ```

3. **[STATUS]** 列に表示されている状態が **[Up]** の場合、SQL Server はコンテナーで実行されており、 **[PORTS]** 列で指定されているポートでリッスンしています。 SQL Server コンテナーの **[STATUS]** 列に **[Exited]** と表示されている場合は、[構成ガイドのトラブルシューティングのセクション](./sql-server-linux-docker-container-troubleshooting.md)を参照してください。

 
    出力:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>Machine Learning Services を有効にする

Machine Learning Services を有効にするには、SQL Server インスタンスに接続し、次の T-SQL ステートメントを実行します。

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>次のステップ

Python 開発者は、次のチュートリアルに従って、SQL Server で Python を使用する方法を学習できます。

+ [Python のチュートリアル:SQL Server Machine Learning Services での線形回帰を使用したスキー レンタルの予測](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python のチュートリアル:SQL Server Machine Learning Services と K-Means クラスタリングを使用して顧客を分類する](../machine-learning/tutorials/python-clustering-model.md)

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクを参照してください。

+ [クイック スタート: T-SQL での R の実行](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [チュートリアル:R 開発者向けのデータベース内分析](../machine-learning/tutorials/r-taxi-classification-introduction.md)