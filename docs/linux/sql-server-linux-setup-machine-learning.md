---
title: Linux をインストールする
titleSuffix: SQL Server Machine Learning Services
description: Linux に SQL Server Machine Learning Services (Python と R) をインストールする方法を説明します:(Red Hat、Ubuntu、SUSE)。
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 11/24/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d236f70a3fdc3e03909078e366ec1f776b68c689
ms.sourcegitcommit: f2bdebed3efa55a2b7e64de9d6d9d9b1c85f479e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "96129430"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Linux に SQL Server Machine Learning Services (Python と R) をインストールする

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

この記事では、Linux に [SQL Server Machine Learning Services](../machine-learning//sql-server-machine-learning-services.md) をインストールする方法について説明します。 Machine Learning Services を使用して、データベース内で Python と R のスクリプトを実行できます。

Machine Learning Services は、Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES)、および Ubuntu にインストールできます。 詳細については、[「SQL Server on Linux のインストール ガイド」の「サポートされているプラットフォーム」](sql-server-linux-setup.md#supportedplatforms)を参照してください。

> [!NOTE]
> Machine Learning Services は、既定で SQL Server ビッグ データ クラスターにインストールされます。 詳細については、[ビッグ データ クラスターでの Machine Learning Services (Python および R) の使用](../big-data-cluster/machine-learning-services.md)に関するページを参照してください

<a name="mro"></a>

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

* [SQL Server on Linux をインストール](sql-server-linux-setup.md)し、インストールを確認します。

* SQL Server Linux リポジトリで、Python と R の拡張機能を確認します。 
  データベース エンジンのインストール用にソース リポジトリを既に構成している場合は、同じリポジトリ登録を使用して **mssql-mlservices** パッケージ インストール コマンドを実行できます。

* (R のみ) Microsoft R Open (MRO) は、SQL Server の R 機能用の基本 R ディストリビューションを提供します。また、RevoScaleR、MicrosoftML、および Machine Learning Services と共にインストールされるその他の R パッケージを使用するための前提条件です。
    * 必要なバージョンは MRO 3.5.2 です。
    * MRO をインストールするには、次の 2 つのアプローチを使用します。
        * MRAN から MRO tarball をダウンロードし、展開して、その install.sh スクリプトを実行します。 このアプローチを使用する場合は、[MRAN のインストール手順](https://mran.microsoft.com/releases/3.5.2)に従うことができます。
        * 以下の説明に従って **packages.microsoft.com** リポジトリを登録して、MRO ディストリビューション (microsoft-r-open-mro と microsoft-r-open-mkl) をインストールします。 
    * MRO のインストール方法については、次のインストールに関するセクションを参照してください。

* T-SQL コマンドを実行するためのツールを用意しておく必要があります。 

  * [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) を使用できます。これは、Linux、Windows、macOS で実行される無料のデータベース ツールです。

## <a name="package-list"></a>パッケージ一覧

インターネットに接続されたデバイス上で、各オペレーティング システム用のパッケージ インストーラーを使用して、パッケージがデータベース エンジンとは別個にダウンロードされてインストールされます。 次の表では、使用可能なすべてのパッケージについて説明します。ただし、R および Python の場合は、完全な機能のインストールまたは最小限の機能のインストールを提供するパッケージを指定します。

使用可能なインストール パッケージ:

| パッケージ名 | 適用先 | 説明 |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | Python と R を実行するために使用される拡張機能のフレームワーク。 |
| microsoft-openmpi  | Python、R | Linux での並列化用に Rev* ライブラリによって使用されるメッセージ パッシング インターフェイス。 |
| mssql-mlservices-python | Python | Anaconda と Python のオープンソース ディストリビューション。 |
|mssql-mlservices-mlm-py  | Python | *完全インストール*。 イメージの特性付けとテキストのセンチメント分析のための、revoscalepy、microsoftml、事前トレーニング済みのモデルを提供します。| 
|mssql-mlservices-packages-py  | Python | *最小インストール*。 revoscalepy と microsoftml を提供します。 <br/>事前トレーニング済みモデルは除外されます。 | 
| [microsoft-r-open*](#mro) | R | R のオープンソース ディストリビューション。3 つのパッケージで構成されています。 |
|mssql-mlservices-mlm-r  | R | *完全インストール*。 提供するもの: イメージの特性付けとテキストのセンチメント分析のための、RevoScaleR、MicrosoftML、sqlRUtils、olapR、事前トレーニング済みのモデル。| 
|mssql-mlservices-packages-r  | R | *最小インストール*。 RevoScaleR、sqlRUtils、MicrosoftML、olapR を提供します。 <br/>事前トレーニング済みモデルは除外されます。 |

<a name="RHEL"></a>

## <a name="install-on-rhel"></a>RHEL へのインストール

Red Hat Enterprise Linux (RHEL) に SQL Server Machine Learning Services をインストールするには、次の手順に従います。

### <a name="install-mro-on-rhel"></a>RHEL に MRO をインストールする

次のコマンドは、MRO を提供するリポジトリを登録します。 登録後、他の R パッケージをインストールするためのコマンド (mssql-mlservices-mml など) には、パッケージの依存関係として MRO が自動的に含まれます。
```bash
# Import the Microsoft repository key

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```

Python と R のインストール オプション:

*  要件に基づいて言語サポートをインストールします (1 つまたは複数の言語)。
*  "*フル インストール*" では、トレーニング済みの機械学習モデルを含む、使用可能なすべての機能が提供されます。
*  "*最小インストール*" では、モデルは除外されますが、すべての機能が含まれます。

> [!Tip]
> 可能であれば、`yum clean all` を実行して、インストールの前にシステム上のパッケージを更新しておきます。

### <a name="full-installation"></a>完全インストール

含まれるもの:
*  オープンソースの Python
*  オープンソースの R
*  機能拡張フレームワーク
*  Microsoft-openmpi
*  拡張機能 (Python、R)
*  機械学習ライブラリ
*  Python および R 用のトレーニング済みモデル

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="minimum-installation"></a>最小インストール

含まれるもの:
*  オープンソースの Python
*  オープンソースの R
*  機能拡張フレームワーク
*  Microsoft-openmpi
*  コア Revo* ライブラリ
*  機械学習ライブラリ

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>Ubuntu にインストールする

Ubuntu に SQL Server Machine Learning Services をインストールするには、次の手順に従います。

### <a name="install-mro-on-ubuntu"></a>Ubuntu に MRO をインストールする

次のコマンドは、MRO を提供するリポジトリを登録します。 登録後、他の R パッケージをインストールするためのコマンド (mssql-mlservices-mml など) には、パッケージの依存関係として MRO が自動的に含まれます。

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

Python と R のインストール オプション:

*  要件に基づいて言語サポートをインストールします (1 つまたは複数の言語)。
*  "*フル インストール*" では、トレーニング済みの機械学習モデルを含む、使用可能なすべての機能が提供されます。
*  "*最小インストール*" では、モデルは除外されますが、すべての機能が含まれます。

> [!Tip]
> 可能であれば、`apt-get update` を実行して、インストールの前にシステム上のパッケージを更新しておきます。 

### <a name="full-installation"></a>完全インストール 

含まれるもの:
*  オープンソースの Python
*  オープンソースの R
*  機能拡張フレームワーク
*  Microsoft-openmpi
*  Python 拡張機能
*  R 拡張機能
*  機械学習ライブラリ
*  Python および R 用のトレーニング済みモデル

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="minimum-installation"></a>最小インストール 

含まれるもの:
*  オープンソースの Python
*  オープンソースの R
*  機能拡張フレームワーク
*  Microsoft-openmpi
*  コア Revo* ライブラリ
*  機械学習ライブラリ

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-sles"></a>SLES へのインストール

SUSE Linux Enterprise Server (SLES) に SQL Server Machine Learning Services をインストールするには、次の手順に従います。

### <a name="install-mro-on-sles"></a>SLES に MRO をインストールする

次のコマンドは、MRO を提供するリポジトリを登録します。 登録後、他の R パッケージをインストールするためのコマンド (mssql-mlservices-mml など) には、パッケージの依存関係として MRO が自動的に含まれます。

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SLES in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Python と R のインストール オプション:

*  要件に基づいて言語サポートをインストールします (1 つまたは複数の言語)。
*  "*フル インストール*" では、トレーニング済みの機械学習モデルを含む、使用可能なすべての機能が提供されます。
*  "*最小インストール*" では、モデルは除外されますが、すべての機能が含まれます。

### <a name="full-installation"></a>完全インストール 

含まれるもの:
*  オープンソースの Python
*  オープンソースの R
*  機能拡張フレームワーク
*  Microsoft-openmpi
*  Python と R 用の拡張機能
*  機械学習ライブラリ
*  Python および R 用のトレーニング済みモデル

```bash
# Install as root or sudo
# Add everything (all R, Python)
sudo zypper install mssql-mlservices-mlm-py
sudo zypper install mssql-mlservices-mlm-r
```

### <a name="minimum-installation"></a>最小インストール 

含まれるもの:
*  オープンソースの Python
*  オープンソースの R
*  機能拡張フレームワーク
*  Microsoft-openmpi
*  コア Revo* ライブラリ
*  機械学習ライブラリ 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
sudo zypper install mssql-mlservices-packages-py
sudo zypper install mssql-mlservices-packages-r
```

## <a name="post-install-config-required"></a>インストール後の構成 (必須)

追加の構成には、主に [mssql-conf ツール](sql-server-linux-configure-mssql-conf.md)を利用します。

1. パッケージのインストールが完了したら、mssql-conf setup を実行し、プロンプトに従って SA パスワードを設定して、エディションを選択します。 SQL Server on Linux をまだ構成していない場合にのみ、このステップを実行します。 

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. オープンソースの Python および R の拡張機能のライセンス契約に同意します。 次のコマンドを使用します。

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
   `mssql-conf setup` が実行されると、セットアップによって mssql-mlservices パッケージが検出され、EULA の同意が求められます (事前に同意されていない場合)。 EULA パラメーターの詳細については、[mssql-conf ツールを使用した SQL Server の構成](sql-server-linux-configure-mssql-conf.md#mlservices-eula)に関するページを参照してください。

3. 送信ネットワーク アクセスを有効にします。 既定では、送信ネットワーク アクセスは無効になっています。 送信要求を有効にするには、mssql-conf ツールを使用して "outboundnetworkaccess" ブール型プロパティを設定します。 詳しくは、「[mssql-conf ツールを利用して SQL Server on Linux を構成する](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)」をご覧ください。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. R 機能の統合のみの場合、**MKL_CBWR** 環境変数を設定して、Intel Math Kernel Library (MKL) 計算からの [一貫した出力を保証](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)します。

   + ユーザーのホーム ディレクトリでファイル `.bash_profile` を編集または作成し、行 `export MKL_CBWR="AUTO"` をファイルに追加します。

   + bash コマンド プロンプトで「`source .bash_profile`」と入力して、このファイルを実行します。

5. SQL Server Launchpad サービスとデータベース エンジン インスタンスを再起動して、INI ファイルから更新後の値を読み込みます。 拡張機能関連の設定が変更されると、通知メッセージが表示されます。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Azure Data Studio または Transact-SQL を実行する SQL Server Management Studio (Windows のみ) などの別のツールを使用して、外部スクリプトの実行を有効にします。

   ```sql
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. スタート パッド サービスをもう一度再起動します。

## <a name="verify-installation"></a>インストールの確認

R ライブラリ (MicrosoftML、RevoScaleR など) については、`/opt/mssql/mlservices/libraries/RServer` を参照してください。

Python ライブラリ (microsoftml および revoscalepy) については、`/opt/mssql/mlservices/libraries/PythonServer` を参照してください。

インストールを検証するには:

* クエリ プールを使用して Python または R を呼び出すシステム ストアド プロシージャが実行される T-SQL スクリプトを実行します。 

* 次の SQL コマンドを実行して、SQL Server で R の実行をテストします。 エラーの場合。 `sudo systemctl restart mssql-server.service` でサービスを再起動してみます。
  ```sql
  EXEC sp_execute_external_script   
  @language =N'R', 
  @script=N' 
  OutputDataSet <- InputDataSet', 
  @input_data_1 =N'SELECT 1 AS hello' 
  WITH RESULT SETS (([hello] int not null)); 
  GO 
  ```
 
* 次の SQL コマンドを実行して、SQL Server で Python の実行をテストします。 
 
  ```sql
  EXEC sp_execute_external_script  
  @language =N'Python', 
  @script=N' 
  OutputDataSet = InputDataSet; 
  ', 
  @input_data_1 =N'SELECT 1 AS hello' 
  WITH RESULT SETS (([hello] int not null)); 
  GO 
  ```

<a name="install-all"></a>

## <a name="unattended-installation"></a>自動実行インストール

データベース エンジンの[無人インストール](sql-server-linux-setup.md#unattended)を使用して、mssql-mlservices と EULA を追加します。

 オープンソースの R および Python ディストリビューションに対し、mlservices 固有の EULA パラメーターのいずれかを使用します。

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

完全な EULA のドキュメントについては、「[mssql-conf ツールを使用して SQL Server on Linux を構成する](sql-server-linux-configure-mssql-conf.md#mlservices-eula)」をご覧ください。

## <a name="offline-installation"></a>オフライン インストール

パッケージをインストールする手順については、[オフライン インストール](sql-server-linux-setup.md#offline)の手順に従います。 ダウンロード サイトを検索し、以下のパッケージ一覧を使用して特定のパッケージをダウンロードします。

> [!Tip]
> いくつかのパッケージ管理ツールには、パッケージの依存関係を判断するのに役立つコマンドが用意されています。 yum の場合は、`sudo yum deplist [package]` を使用します。 Ubuntu の場合は、`sudo apt-get install --reinstall --download-only [package name]` の後に `dpkg -I [package name].deb` を続けて使用します。

 
### <a name="download-site"></a>ダウンロード サイト

[https://packages.microsoft.com/](https://packages.microsoft.com/) からパッケージをダウンロードします。 Python および R 用の mlservices パッケージはすべて、データベース エンジン パッケージと併置されています。 mlservices パッケージの基本バージョンは、9.4.6 です。 microsoft-r-open パッケージが[別のリポジトリ](#mro)にあることを思い出してください。

### <a name="rhel7-paths"></a>RHEL/7 パス

|Package|ダウンロード場所|
|--|----|
| mssql/mlservices パッケージ | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| microsoft-r-open パッケージ | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 

### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 パス

|Package|ダウンロード場所|
|--|----|
| mssql/mlservices パッケージ | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| microsoft-r-open パッケージ | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

### <a name="sles12-paths"></a>SLES/12 パス

|Package|ダウンロード場所|
|--|----|
| mssql/mlservices パッケージ | [https://packages.microsoft.com/sles/12/mssql-server-2019/](https://packages.microsoft.com/sles/12/mssql-server-2019/) |
| microsoft-r-open パッケージ | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

使用する拡張機能を選択し、特定の言語に必要なパッケージをダウンロードします。 ファイル名のサフィックスにはプラットフォームの情報が含まれます。

### <a name="package-list"></a>パッケージ一覧

使用する拡張機能に応じて、特定の言語に必要なパッケージをダウンロードします。 正確なファイル名にはサフィックス内のプラットフォーム情報が含まれますが、以下のファイル名では、取得するファイルを十分に判断できる程度に近いものにしておく必要があります。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="next-steps"></a>次のステップ

Python 開発者は、次のチュートリアルに従って、SQL Server で Python を使用する方法を学習できます。

+ [Python のチュートリアル:SQL Server Machine Learning Services での線形回帰を使用したスキー レンタルの予測](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python のチュートリアル:SQL Server Machine Learning Services と K-Means クラスタリングを使用して顧客を分類する](../machine-learning/tutorials/python-clustering-model.md)

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクを参照してください。

+ [クイック スタート: T-SQL での R の実行](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [チュートリアル:R 開発者向けのデータベース内分析](../machine-learning/tutorials/r-taxi-classification-introduction.md)
