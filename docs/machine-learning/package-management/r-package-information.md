---
title: R パッケージ情報の取得
description: SQL Server Machine Learning Services と SQL Server R Services にインストールされている R パッケージに関する情報を取得する方法について説明します。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/27/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 0bbc530a84ca09ce5e2797bc770e50a20fc5113e
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869971"
---
# <a name="get-r-package-information"></a>R パッケージ情報の取得

[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この記事では、[SQL Server 上の Machine Learning Services](../sql-server-machine-learning-services.md) および[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)にインストールされている R パッケージに関する情報を取得する方法について説明します。 R スクリプトの例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。
::: moniker-end
::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
この記事では、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) にインストールされている R パッケージに関する情報を取得する方法について説明します。 R スクリプトの例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この記事では、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) にインストールされている R パッケージに関する情報を取得する方法について説明します。 R スクリプトの例では、インストール パスやバージョンなどのパッケージ情報を一覧表示する方法を示しています。
::: moniker-end

## <a name="default-r-library-location"></a>R ライブラリの既定の場所

SQL Server と共に機械学習をインストールすると、インストールした言語ごとに 1 つのパッケージ ライブラリがインスタンス レベルで作成されます。 このインスタンス ライブラリは、Windows では SQL Server に登録されているセキュリティで保護されたフォルダーです。

SQL Server のデータベース内で実行されるすべてのスクリプトは、インスタンス ライブラリから関数を読み込む必要があります。 SQL Server は、他のライブラリにインストールされているパッケージにはアクセスできません。 これはリモート クライアントにも当てはまります。サーバーの計算のコンテキストで実行されているすべての R スクリプトは、インスタンス ライブラリにインストールされているパッケージしか使用できません。
既定のインスタンス ライブラリは、サーバーの資産を保護するために、コンピューターの管理者のみが変更できるようになっています。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
R のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
R のバイナリの既定のパスは次のとおりです。

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`

既定の SQL インスタンスは、MSSQLSERVER と想定されています。 SQL Server がユーザー定義の名前付きインスタンスとしてインストールされている場合、代わりにその指定の名前を使用します。
::: moniker-end

次のステートメントを実行すると、現在のインスタンスの既定の R パッケージ ライブラリを確認することができます。

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

## <a name="default-microsoft-r-packages"></a>既定の Microsoft R パッケージ

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

次の Microsoft R パッケージは、SQL Server R Services と共にインストールされます。

|パッケージ | Version | 説明 |
|---------|---------|-------------|
| [RevoScaleR](/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | ストアド プロシージャに R スクリプトを含めるために使用します。 |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

次の Microsoft R パッケージは、セットアップ時に R 機能を選択すると、SQL Server Machine Learning Services と共にインストールされます。

|パッケージ | Version | 説明 |
|---------|---------|-------------|
| [RevoScaleR](/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | ストアド プロシージャに R スクリプトを含めるために使用します。 |
| [MicrosoftML](/r-server/r-reference/microsoftml/microsoftml-package)| 1.4.0 | R に機械学習アルゴリズムを追加します。 | 
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | 1.0.0 | R で MDX ステートメントを記述するために使用します。 |

::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"

次の Microsoft R パッケージは、セットアップ時に R 機能を選択すると、SQL Server Machine Learning Services と共にインストールされます。

|パッケージ | Version | 説明 |
|---------|---------|-------------|
| [RevoScaleR](/r-server/r-reference/revoscaler/revoscaler)  | 9.4.7 | リモートでの計算のコンテキスト、ストリーミング、データのインポートと変換、モデリング、視覚化、および分析での rx 関数の並列実行で使用します。 |
| [sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | ストアド プロシージャに R スクリプトを含めるために使用します。 |
| [MicrosoftML](/r-server/r-reference/microsoftml/microsoftml-package)| 9.4.7 | R に機械学習アルゴリズムを追加します。 |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | 1.0.0 | R で MDX ステートメントを記述するために使用します。 |

::: moniker-end

### <a name="component-upgrades"></a>コンポーネントのアップグレード

既定で R パッケージは、サービス パックと累積的な更新プログラムで更新されます。 その他のパッケージおよび R のコア コンポーネントのバージョンの完全アップグレードは、製品のアップグレード、または Microsoft Machine Learning Server への R サポートのバインドによってのみ可能です。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
また、コンポーネントをアップグレードすると、MicrosoftML および olapR パッケージを SQL Server インスタンスに追加することもできます。
::: moniker-end

詳細については、[SQL Server での R および Python コンポーネントのアップグレード](../install/upgrade-r-and-python.md)に関する記事を参照してください。

## <a name="default-open-source-r-packages"></a>既定のオープンソースの R パッケージ

R では、オープンソースの R をサポートしているので、base R 関数を呼び出して、オープンソースおよびサードパーティ パッケージを追加インストールできます。 R 言語では、**base**、**stats**、**utils** などのコア機能をサポートしています。 R の基本インストールには、**RGui** (軽量の対話型エディター) や **RTerm** (R のコマンド プロンプト) などの多数のサンプル データセットや、標準の R ツールも含まれています。

お使いのインストールに含まれるオープンソースの R のディストリビューションは、[Microsoft R Open (MRO)](https://mran.microsoft.com/open) です。 MRO では、base R に [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library) などのオープンソースのパッケージの付加価値が追加されています。

SQL Server バージョンごとに含まれている R のバージョンの詳細については、「[Python および R のバージョン](../sql-server-machine-learning-services.md#versions)」を参照してください。

> [!IMPORTANT]
> SQL Server のセットアップでインストールされた R のバージョンは、手動で Web 上の新しいバージョンに上書きしないでください。 Microsoft R パッケージは、R の特定のバージョンに基づいています。インストールを変更すると、それが不安定になる可能性があります。

## <a name="list-all-installed-r-packages"></a>インストールされているすべての R パッケージの列挙

次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャの例では、R 関数 `installed.packages()` を使用して、現在の SQL インスタンスの R_SERVICES ライブラリにインストールされている R パッケージを一覧表示します。 このスクリプトでは、DESCRIPTION ファイルのパッケージ名とバージョン フィールドを返します。

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

R パッケージの DESCRIPTION フィールドのオプション フィールドおよび既定フィールドの詳細については、「[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)」を参照してください。

## <a name="find-a-single-r-package"></a>1 つの R パッケージの検索

インストールした R パッケージが、特定の SQL Server インスタンスで使用できることを確認したい場合、ストアド プロシージャを実行してパッケージを読み込み、メッセージが返されるようにします。

たとえば、次のステートメントは、使用可能な場合に [glue](https://cran.r-project.org/web/packages/glue/) パッケージを検索して読み込みます。
パッケージが見つからないか、または読み込めない場合は、エラーが発生します。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'
require("glue")
'
```

パッケージの詳細については、「`packageDescription`」を参照してください。
次のステートメントでは、**MicrosoftML** パッケージの情報が返されます。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("MicrosoftML"))
'
```

## <a name="next-steps"></a>次のステップ

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [R ツールを使用してパッケージをインストールする](install-r-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [sqlmlutils で新しい R パッケージをインストールする](install-additional-r-packages-on-sql-server.md)
::: moniker-end