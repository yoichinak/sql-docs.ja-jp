---
title: Python ツールを使用してパッケージをインストールする
description: 標準の Python ツールを使用して、新しい Python パッケージを SQL Server Machine Learning Services のインスタンスにインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/21/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 67d5a323cfdbdb7eb765430ba264ff0bde2074f5
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870480"
---
# <a name="install-packages-with-python-tools-on-sql-server"></a>Python ツールを使用して SQL Server 上にパッケージをインストールする
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

この記事では、標準の Python ツールを使用して、新しい Python パッケージを SQL Server Machine Learning Services のインスタンスにインストールする方法について説明します。 一般に、新しいパッケージをインストールするプロセスは、標準の Python 環境のプロセスと似ています。 ただし、サーバーからインターネットに接続できない場合は、いくつかの追加の手順が必要です。

パッケージの場所とインストール パスの詳細については、「[Get Python package information](python-package-information.md)」(Python パッケージ情報の取得) を参照してください。

## <a name="prerequisites"></a>前提条件

+ Python 言語オプションと共に [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) がインストールされている必要があります。

### <a name="other-considerations"></a>その他の考慮事項

+ パッケージは Python 3.5 に準拠し、Windows で実行する必要があります。

+ Python パッケージ ライブラリは SQL Server インスタンスの Program Files フォルダー内にあります。既定では、このフォルダーにインストールするには管理者権限が必要です。 詳細については、[パッケージ ライブラリの場所](../package-management/python-package-information.md#default-python-library-location)に関するページを参照してください。

+ パッケージのインストールはインスタンス単位です。 Machine Learning Services のインスタンスが複数ある場合は、各インスタンスにパッケージを追加する必要があります。

+ 多くの場合、データベース サーバーはロック ダウンされています。 多くの場合、インターネット アクセスは完全にブロックされています。 依存関係が多数あるパッケージの場合、それらの依存関係を事前に特定し、各依存関係を手動でインストールする準備ができている必要があります。

+ パッケージを追加する前に、パッケージが SQL Server 環境に適しているかどうかを検討してください。

  + データベースをクエリするだけのタスクではなく、データベース エンジンとの緊密な統合からメリットが得られるタスク (機械学習など) には、データベース内の Python を使用することをお勧めします。

  + サーバーに対して計算の負荷が大きくなるパッケージを追加すると、パフォーマンスが低下します。

  + 強化された SQL Server 環境では、次のパッケージを避けることをお勧めします。
    + ネットワーク アクセスを必要とするパッケージ
    + 管理者特権でのファイル システム アクセスが必要なパッケージ
    + Web 開発、または SQL Server 内で実行しても効果のないタスクに使用されるパッケージ

## <a name="add-a-python-package-on-sql-server"></a>SQL Server への Python パッケージのインストール

スクリプトで使用できる新しい Python パッケージを SQL Server にインストールするには、Machine Learning Services のインスタンスにパッケージをインストールします。 Machine Learning Services のインスタンスが複数ある場合は、各インスタンスにパッケージを追加する必要があります。

次の例でインストールされるパッケージは [CNTK](/cognitive-toolkit/) です。これは、さまざまな種類のニューラル ネットワークのカスタマイズ、トレーニング、および共有をサポートする Microsoft のディープ ラーニング用フレームワークです。

### <a name="for-offline-install-download-the-python-package"></a>オフライン インストールの場合は、Python パッケージをダウンロードします

インターネットにアクセスできないサーバーに Python パッケージをインストールする場合は、インターネットにアクセスできるコンピューターから WHL ファイルをダウンロードしてから、そのファイルをサーバーにコピーする必要があります。

たとえば、インターネットに接続されたコンピューターには、サイト `cntk-2.1-cp35-cp35m-win_amd64.whl`[https://cntk.ai/PythonWheel/CPU-Only からファイル ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl) をダウンロードし、そのファイルを SQL Server コンピューターのローカル フォルダーにコピーできます。

> [!IMPORTANT]
> 必ず Windows バージョンのパッケージを入手します。 ファイルの末尾が .gz の場合は、正しいバージョンではない可能性があります。

複数のプラットフォーム用の CNTK フレームワークと複数のバージョンの Python のダウンロードの詳細については、「[マシン上で CNTK をセットアップする](/cognitive-toolkit/Setup-CNTK-on-your-machine)」を参照してください。

### <a name="locate-the-python-library"></a>Python ライブラリを見つける

SQL Server によって使用される既定の Python ライブラリの場所を見つけます。 複数のインスタンスをインストールした場合は、パッケージを追加するインスタンスの `PYTHON_SERVICES` フォルダーを見つけます。

たとえば、既定値を使用して Machine Learning Services をインストールし、既定のインスタンスで機械学習を有効にした場合のパスは次のとおりです。

```console
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"
```

> [!TIP]
> 今後のデバッグとテストのために、インスタンス ライブラリに固有の Python 環境を設定することができます。

### <a name="install-the-package-using-pip"></a>pip を使用してパッケージをインストールする

**pip** インストーラーを使用して、新しいパッケージをインストールします。 `pip.exe` フォルダーの `Scripts` サブフォルダーに `PYTHON_SERVICES` があります。 SQL Server のセットアップでは、システム パスに `Scripts` サブフォルダーは追加されないため、完全なパスを指定するか、Windows で PATH 変数に Scripts フォルダーを追加できます。

> [!NOTE]
> Visual Studio 2017 を使用している場合、または Python 拡張機能と共に Visual Studio 2015 を使用している場合は、`pip install`[Python 環境]**ウィンドウから** を実行できます。 **[パッケージ]** をクリックし、インストールするパッケージの名前または場所をテキスト ボックスに入力します。 「`pip install`」と入力する必要はありません。自動的に入力されます。

+ コンピューターからインターネットにアクセスできる場合は、パッケージの名前を指定します。

  ```console
  scripts\pip.exe install cntk
  ```
  また、次の例のように、特定のパッケージとバージョンの URL を指定することもできます。

  ```console
  scripts\pip.exe install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

+ コンピューターからインターネットにアクセスできない場合は、上記の手順でダウンロードした WHL ファイルを指定します。 次に例を示します。

  ```console
  scripts\pip.exe install C:\Downloads\cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

インストールを完了するためにアクセス許可を昇格するように求めるメッセージが表示される場合があります。
インストール手順を進めると、コマンド プロンプト ウィンドウに状態メッセージが表示されます。

### <a name="load-the-package-or-its-functions-as-part-of-your-script"></a>スクリプトの一部としてパッケージまたはその関数を読み込む

インストールが完了すると、すぐに SQL Server の Python スクリプトでパッケージを使い始められます。

スクリプトでパッケージの関数を使用するには、スクリプトの最初の行に標準の `import <package_name>` ステートメントを挿入します。

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import cntk
# Python statements ...
'
```

## <a name="see-also"></a>参照

+ [Python パッケージ情報の取得](python-package-information.md)
+ [SQL Server Machine Learning Services 用の Python のチュートリアル](../tutorials/python-tutorials.md)
+ [Python API for CNTK](https://cntk.ai/pythondocs/tutorials.html)。