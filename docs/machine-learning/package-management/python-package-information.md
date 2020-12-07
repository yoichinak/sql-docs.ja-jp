---
title: Python パッケージ情報の取得
description: SQL Server Machine Learning Services にインストールした Python パッケージのバージョンやインストール場所などの情報を取得する方法について説明します。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/03/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 9bb55bf9bac934f78b0a309663ced729a8ef6534
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869833"
---
# <a name="get-python-package-information"></a>Python パッケージ情報の取得

[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この記事では、[SQL Server 上の Machine Learning Services](../sql-server-machine-learning-services.md) および[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)にインストールした Python パッケージのバージョンやインストール場所などの情報を取得する方法について説明します。 Python のスクリプト例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この記事では、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) にインストールした Python パッケージのバージョンやインストール場所などの情報を取得する方法について説明します。 Python のスクリプト例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この記事では、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) にインストールした Python パッケージのバージョンやインストール場所などの情報を取得する方法について説明します。 Python のスクリプト例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。
::: moniker-end

## <a name="default-python-library-location"></a>Python ライブラリの既定の場所

SQL Server と共に機械学習をインストールすると、インストールした言語ごとに 1 つのパッケージ ライブラリがインスタンス レベルで作成されます。 このインスタンス ライブラリは、SQL Server に登録されているセキュリティで保護されたフォルダーです。

SQL Server のデータベース内で実行されるすべてのスクリプトまたはコードは、このインスタンス ライブラリから関数を読み込む必要があります。 SQL Server は、他のライブラリにインストールされているパッケージにはアクセスできません。 これはリモート クライアントにも当てはまります。サーバーの計算のコンテキストで実行されているすべての Python コードは、インスタンス ライブラリにインストールされているパッケージしか使用できません。
既定のインスタンス ライブラリは、サーバーの資産を保護するために、コンピューターの管理者のみが変更できるようになっています。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Python のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Python のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。
::: moniker-end

次の SQL コマンドを実行して、外部スクリプトを有効にします。

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH override;
```

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
> [!IMPORTANT]
> Azure SQL Managed Instance 上で、sp_configure および RECONFIGURE コマンドを実行すると、SQL サーバーの再起動がトリガーされ、RG 設定が有効になります。 これにより、使用不可の状態が数秒間生じる可能性があります。
::: moniker-end

現在のインスタンスの既定のライブラリを確認する場合は、次の SQL ステートメントを実行します。 この例では、Python の `sys.path` 変数に含まれるフォルダーの一覧が返されます。 一覧には、現在のディレクトリと標準ライブラリ パスが含まれています。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

変数 `sys.path` の詳細と、これを使用したモジュールのインタープリターの検索パスの設定方法については、[モジュールの検索パス](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)に関する記事を参照してください。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
> [!NOTE]
> **pip** または同様の方法を使用して、Python パッケージを SQL パッケージ ライブラリに直接インストールしないようにしてください。 SQL インスタンスにパッケージをインストールするには、代わりに **sqlmlutils** を使用します。 詳細については、「[sqlmlutils を使用した Python パッケージのインストール](install-additional-python-packages-on-sql-server.md)」を参照してください。
::: moniker-end

## <a name="default-microsoft-python-packages"></a>既定の Microsoft Python パッケージ

セットアップ時に Python の機能を選択すると、SQL Server Machine Learning Services と共に次の Microsoft Python パッケージがインストールされます。

| パッケージ | Version |  説明 |
| ---------|---------|--------------|
| [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.4.7 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.4.7 | Python に機械学習アルゴリズムを追加します。 |

含まれている Python のバージョンの詳細については、「[Python および R のバージョン](../sql-server-machine-learning-services.md#versions)」を参照してください。

### <a name="component-upgrades"></a>コンポーネントのアップグレード

既定で Python パッケージは、サービス パックと累積的な更新プログラムで更新されます。 その他のパッケージおよび Python のコア コンポーネントのバージョンの完全アップグレードは、製品のアップグレード、または Microsoft Machine Learning Server に Python サポートをバインドすることによってのみ可能です。

詳細については、[SQL Server での R および Python コンポーネントのアップグレード](../install/upgrade-r-and-python.md)に関する記事を参照してください。

## <a name="default-open-source-python-packages"></a>既定のオープンソースの Python パッケージ

セットアップ時に Python の言語オプションを選択すると、(Python 3.5 に) Anaconda 4.2 のディストリビューションがインストールされます。 標準インストールには、Python のコード ライブラリに加え、サンプル データ、単体テスト、およびサンプル スクリプトが含まれます。

> [!IMPORTANT]
> SQL Server のセットアップでインストールされた Python のバージョンは、手動で Web 上の新しいバージョンに上書きしないでください。 Microsoft Python のパッケージは、特定のバージョンの Anaconda に基づいています。 インストールを変更すると、それが不安定になる可能性があります。

## <a name="list-all-installed-python-packages"></a>インストールされているすべての Python パッケージの一覧表示

次のスクリプトの例では、SQL Server インスタンスにインストールされているすべての Python パッケージの一覧を表示します。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
import pandas
OutputDataSet = pandas.DataFrame(sorted([(i.key, i.version) for i in pkg_resources.working_set]))'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128)));
```

## <a name="find-a-single-python-package"></a>1 つの Python パッケージの検索

インストールした Python パッケージが、特定の SQL Server インスタンスで使用できることを確認したい場合、ストアド プロシージャを実行してパッケージを検索し、メッセージが返されるようにします。

たとえば、次のコードでは `scikit-learn` パッケージが検索されます。
パッケージが見つかった場合、コードによりパッケージのバージョンが出力されます。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "scikit-learn"
try:
    version = pkg_resources.get_distribution(pkg_name).version
    print("Package " + pkg_name + " is version " + version)
except:
    print("Package " + pkg_name + " not found")
'
```

結果:

```text
STDOUT message(s) from external script: Package scikit-learn is version 0.20.2
```

<a name="bkmk_SQLPythonVersion"></a>
## <a name="view-the-version-of-python"></a>Python のバージョンの表示

次のコード例では、SQL Server のインスタンスにインストールされている Python のバージョンを返します。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import sys
print(sys.version)
'
```

## <a name="next-steps"></a>次のステップ

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [Python ツールを使用してパッケージをインストールする](install-python-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [sqlmlutils を使用した新しい Python パッケージのインストール](install-additional-r-packages-on-sql-server.md)
::: moniker-end