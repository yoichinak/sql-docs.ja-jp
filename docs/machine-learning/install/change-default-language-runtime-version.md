---
title: 既定の R または Python 言語ランタイム バージョンを変更する
description: SQL Server 2017 Machine Learning Services または SQL Server R Services を使用して、SQL インスタンスで使用される R または Python ランタイムの既定のバージョンを変更する方法について説明します。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/14/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 457d728bd0e4abb5c2cf70063c0330924104c482
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869984"
---
# <a name="change-the-default-r-or-python-language-runtime-version"></a>既定の R または Python 言語ランタイム バージョンを変更する

[!INCLUDE[SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

この記事では、[SQL Server 2016 R Services](../r/sql-server-r-services.md) または [SQL Server 2017 Machine Learning Services](../sql-server-machine-learning-services.md) で使用される R または Python の既定のバージョンを変更する方法について説明します。

次に、さまざまな SQL Server バージョンに含まれる R および Python ランタイムのバージョンを示します。

| SQL Server のバージョン | サービス | 累積的な更新プログラム | R ランタイムのバージョン | Python ランタイムのバージョン |
|-|-|-|-|-|
| SQL Server 2016 | R Services | RTM - SP2 CU13 | 3.2.2 | 使用できません |
| SQL Server 2016 | R Services | SP2 CU14 以降 | 3.2.2 および 3.5.2 | 使用できません |
| SQL Server 2017 | Machine Learning サービス | RTM - CU21 | 3.3.3 | 3.5.2 |
| SQL Server 2017 | Machine Learning サービス | CU22 以降 | 3.3.3 および 3.5.2 | 3.5.2 および 3.7.2 |

## <a name="prerequisites"></a>前提条件

既定の R または Python 言語ランタイム バージョンを変更するには、累積的な更新プログラム (CU) をインストールする必要があります。

- **SQL Server 2016:** Services Pack (SP) 2 の累積的な更新プログラム (CU) 14 以降
- **SQL Server 2017:** 累積的な更新プログラム (CU) 22 以降

最新の累積的な更新プログラムをダウンロードするには、「[Microsoft SQL Server の最新の更新プログラム](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)」をご覧ください。

> [!NOTE]
> SQL Server の新規インストールで累積的な更新プログラムをスリップストリームすると、最新バージョンの R および Python ランタイムのみがインストールされます。

## <a name="change-r-runtime-version"></a>R ランタイムのバージョンを変更する

SQL Server 2016 または 2017 に対して上記の累積的な更新プログラムのいずれかをインストールしている場合は、SQL インスタンスに複数のバージョンの R が存在する可能性があります。 各バージョンは、`R_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* という名前のインスタンス フォルダーのサブフォルダーに含まれています (元のインストールからのフォルダーには、フォルダー名にバージョン番号が付加されていない場合があります)。

R 3.5 を含む CU をインストールした場合、新しい `R_SERVICES` フォルダーは次のようになります。

- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.<INSTANCE_NAME>\R_SERVICES.3.5`
- SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\R_SERVICES.3.5`

各 SQL インスタンスでは、これらのバージョンのいずれかが R の既定のバージョンとして使用されます。既定のバージョンを変更するには、**RegisterRext.exe** コマンドライン ユーティリティを使用します。 このユーティリティは、各 SQL インスタンスの R フォルダーにあります。

*&lt;SQL インスタンス パス&gt;* \R_SERVICES.n.n\library\RevoScaleR\rxLibs\x64\RegisterRext.exe

> [!Note]
> この記事で説明している機能は、SQL CU に含まれている **RegisterRext.exe** のコピーでのみ使用できます。 元の SQL インストールに付属するコピーは使用しないでください。

R ランタイム バージョンを変更するには、次のコマンド ライン引数を **RegisterRext.exe** に渡します。

- `/configure` - 必須。既定の R バージョンを構成していることを示します。

- `/instance:`*&lt;インスタンス名&gt;* - 省略可能。構成するインスタンスです。 指定しない場合、既定のインスタンスが構成されます。

- `/rhome:`*&lt;R_SERVICES [n. n] フォルダーのパス&gt;* - 省略可能。既定の R バージョンとして設定するランタイム バージョン フォルダーへのパスです。

  /rhome を指定しない場合、構成されるパスは **RegisterRext.exe** が配置されているパスになります。

### <a name="examples"></a>例

SQL Server 2016 および 2017 で R ランタイム バージョンを変更する方法の例を次に示します。

#### <a name="change-r-runtime-version-in-sql-server-2016"></a>SQL Server 2016 で R ランタイム バージョンを変更する

たとえば、SQL Server 2016 でインスタンス MSSQLSERVER01 に対し R の既定のバージョンとして **R 3.5** を構成するには、次のようにします。

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

#### <a name="change-r-runtime-version-in-sql-server-2017"></a>SQL Server 2017 で R ランタイム バージョンを変更する

たとえば、SQL Server 2017 でインスタンス MSSQLSERVER01 に対し R の既定のバージョンとして **R 3.5** を構成するには、次のようにします。

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

これらの例では、**RegisterRext.exe** が配置されているフォルダーと同じフォルダーを指定しているため、`/rhome` 引数を含める必要はありません。

## <a name="change-python-runtime-version"></a>Python ランタイムのバージョンを変更する

SQL Server 2017 に対して CU22 以降がインストールされている場合は、SQL インスタンスに複数バージョンの Python が存在する可能性があります。 各バージョンは、`PYTHON_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* という名前のインスタンス フォルダーのサブフォルダーに含まれています (元のインストールからのフォルダーには、フォルダー名にバージョン番号が付加されていない場合があります)。

たとえば、Python 3.7 を含む CU をインストールした場合、新しい `PYTHON_SERVICES` フォルダーが作成されます。

`C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\PYTHON_SERVICES.3.7`  

各 SQL インスタンスは、これらのバージョンのいずれかを Python の既定のバージョンとして使用します。 既定のバージョンを変更するには、**RegisterRExt.exe** コマンドライン ユーティリティを使用します。 このユーティリティは、各 SQL インスタンスの Python フォルダーにあります。

*&lt;SQL インスタンス パス&gt;* `\PYTHON_SERVICES.n.n\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.exe`

> [!Note]
> この記事で説明している機能は、SQL CU に含まれている **RegisterRExt.exe** のコピーでのみ使用できます。 元の SQL インストールに付属するコピーは使用しないでください。

Python ランタイム バージョンを変更するには、次のコマンド ライン引数を **RegisterRext.exe** に渡します。

- `/configure` - 必須。既定の Python バージョンを構成していることを示します。

- `/python` - 既定の Python バージョンを構成していることを示します。 `/pythonhome` を指定した場合は、省略可能です。

- `/instance:`*&lt;インスタンス名&gt;* - 省略可能。構成するインスタンスです。 指定しない場合、既定のインスタンスが構成されます。

- `/pythonhome:`*&lt;PYTHON_SERVICES[n.n] フォルダーのパス&gt;* - 省略可能。既定の Python バージョンとして設定するランタイム バージョン フォルダーへのパスです。

  /pythonhome を指定しない場合、構成されるパスは **RegisterRExt.exe** が配置されているパスになります。

### <a name="example"></a>例

たとえば、SQL Server 2017 でインスタンス MSSQLSERVER01 に対し Python の既定のバージョンとして **Python 3.7** を構成するには、次のようにします。

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7\Lib\site-packages\revoscalepy\rxLibs"

.\RegisterRext.exe /configure /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

この例では、**RegisterRext.exe** が配置されているフォルダーと同じフォルダーを指定しているため、`/pythonhome` 引数を含める必要はありません。

## <a name="remove-a-runtime-version"></a>ランタイム バージョンを削除する

R または Python のバージョンを削除するには、前述のものと同じ `/rhome`、`/pythonhome`、および `/instance` 引数を使用して、`/cleanup` コマンドライン引数と共に **RegisterRExt.exe** を使用します。

たとえば、**R 3.2** フォルダーをインスタンス MSSQLSERVER01 から削除するには、次のようにします。

```cmd
.\RegisterRext.exe /cleanup /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES" /instance:MSSQLSERVER01
```

たとえば、**Python 3.7** フォルダーをインスタンス MSSQLSERVER01 から削除するには、次のようにします。

```cmd
.\RegisterRExt.exe /cleanup /python /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

**RegisterRext.exe** では、指定された R ランタイムのクリーンアップを確認するように求める次のメッセージが表示されます。

> *Are you sure you want to permanently delete the given runtime along with all the packages installed on it? (指定されたランタイムと、それにインストールされているすべてのパッケージを完全に削除しますか?)\[Yes(Y)/No(N)/Default(Yes) (はい (Y)/いいえ (N)/既定 (はい))\]:*

確認するには、`Y` と回答するか、Enter キーを押します。 または、`/y` または `/Yes` を `/cleanup` オプションと共に渡すことで、このプロンプトをスキップすることもできます。

> [!NOTE]
> バージョンを削除できるのは、そのバージョンが既定値として構成されておらず、**RegisterRext.exe** の実行に現在使用されていない場合のみです。

## <a name="next-steps"></a>次のステップ

- [R パッケージ情報の取得](../package-management/r-package-information.md)
- [Python パッケージ情報の取得](../package-management/python-package-information.md)
- [R ツールを使用してパッケージをインストールする](../package-management/install-r-packages-standard-tools.md)
- [Python ツールを使用してパッケージをインストールする](../package-management/install-python-packages-standard-tools.md)
