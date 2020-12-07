---
title: R ツールを使用してパッケージをインストールする
description: 標準の R ツールを使用して、新しい R パッケージを SQL Server Machine Learning Services または SQL Server R Services のインスタンスにインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 55d2917d149a4c88dbfddf614971c8d4f1e60d26
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869955"
---
# <a name="install-packages-with-r-tools"></a>R ツールを使用してパッケージをインストールする

[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

この記事では、標準の R ツールを使用して、新しい R パッケージを SQL Server Machine Learning Services または SQL Server R Services のインスタンスにインストールする方法について説明します。 インターネットに接続されている SQL Server だけでなく、インターネットから切り離されている SQL Server にもパッケージをインストールできます。

標準の R ツールの他に、次のものを使用して R パッケージをインストールできます。

+ [RevoScaleR](install-r-packages-with-revoscaler.md)
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [T-SQL](install-r-packages-with-tsql.md) (CREATE EXTERNAL LIBRARY)
::: moniker-end

## <a name="general-considerations"></a>一般的な考慮事項

+ SQL Server で実行されている R コードでは、既定のインスタンス ライブラリにインストールされているパッケージのみを使用できます。 SQL Server では、外部ライブラリからパッケージを読み込むことはできません。これには同じコンピューター上にある外部ライブラリや、
他の Microsoft 製品と共にインストールされた R ライブラリも含まれます。

+ R パッケージ ライブラリは SQL Server インスタンスの Program Files フォルダー内にあります。既定では、このフォルダーにインストールするには管理者権限が必要です。 詳細については、[パッケージ ライブラリの場所](../package-management/r-package-information.md#default-r-library-location)に関するページを参照してください。

  ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
  管理者以外のユーザーは、RevoScaleR 9.0.1 以降または CREATE EXTERNAL LIBRARY を使用してパッケージをインストールできます。 **dbo_owner** ユーザー、または CREATE EXTERNAL LIBRARY 権限を持つユーザーは、現在のデータベースに R パッケージをインストールできます。 詳細については、次を参照してください。
  + [RevoScaleR を使用して R パッケージをインストールする](install-r-packages-with-revoscaler.md)
  + [T-SQL (CREATE EXTERNAL LIBRARY) を使用して SQL Server に R パッケージをインストールする](install-r-packages-with-tsql.md)
  ::: moniker-end

  ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  管理者以外のユーザーは、RevoScaleR 9.0.1 以降を使用してパッケージをインストールできます。 **dbo_owner** ユーザーは、現在のデータベースに R パッケージをインストールできます。 詳細については、「[RevoScaleR を使用して R パッケージをインストールする](install-r-packages-with-revoscaler.md)」を参照してください。
  ::: moniker-end

+ 強化された SQL Server 環境では、次のパッケージを避けることをお勧めします。
  + ネットワーク アクセスを必要とするパッケージ
  + 管理者特権でのファイル システム アクセスが必要なパッケージ
  + Web 開発、または SQL Server 内で実行しても効果のないタスクに使用されるパッケージ

## <a name="online-installation-with-internet-access"></a>オンライン インストール (インターネット アクセスあり)

SQL Server からインターネットにアクセスできる場合は、標準のパッケージ インストール ツールを使用して R パッケージをインストールできます。

1. インスタンス ライブラリの場所を特定し (「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照)、R ツールがインストールされているフォルダーに移動します。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   たとえば、SQL Server の既定のインスタンスの既定のパスは次のようになります。

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   たとえば、SQL Server の既定のインスタンスの既定のパスは次のようになります。

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. このフォルダーから管理者として **R** または **Rgui** を実行します。

1. R コマンド `install.packages` を実行し、パッケージ名を指定します。 パッケージに依存関係がある場合、インストーラーは自動的に依存関係をダウンロードしてインストールします。

SQL Server のサイド バイ サイド インスタンスが複数ある場合は、パッケージを使用するインスタンスごとに個別にインストールを実行します。 パッケージをインスタンス間で共有することはできません。

## <a name="offline-installation-no-internet-access"></a><a name = "bkmk_offlineInstall"></a> オフライン インストール (インターネット アクセスなし)

多くの場合、実稼働データベースをホストするサーバーにはインターネット接続がありません。 そのような環境に R パッケージをインストールするには、あらかじめパッケージと依存関係を (ZIP ファイルとして) ダウンロードして準備し、ファイルをサーバー上のフォルダーにコピーします。 ファイルが配置されたら、パッケージをオフラインでインストールできます。

すべての依存関係を識別するのは複雑な作業です。 R については、[**miniCRAN**](https://andrie.github.io/miniCRAN/) を使用してローカル リポジトリを作成することをお勧めします。
**miniCRAN** は、インストールするパッケージの一覧を取得し、依存関係を分析し、必要な ZIP ファイルをすべて収集します。 次に、分離された SQL Server インスタンスにコピーできる単一のリポジトリを作成します。 [**igraph**](https://igraph.org/r/) パッケージも、パッケージの依存関係を分析する際に役立ちます。

詳細については、「[miniCRAN を使用してローカル R パッケージ リポジトリを作成する](create-a-local-package-repository-using-minicran.md)」を参照してください。

ZIP ファイルが SQL Server インスタンス上にある場合は、標準の R ツールを使用してサーバーにインストールできます。

1. インスタンス ライブラリの場所を特定し (「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照)、R ツールがインストールされているフォルダーに移動します。 

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   たとえば、SQL Server の既定のインスタンスの既定のパスは次のようになります。

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   たとえば、SQL Server の既定のインスタンスの既定のパスは次のようになります。

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. このフォルダーから管理者として **R** または **Rgui** を実行します。

1. R コマンドを実行して、`install.packages`パッケージまたはリポジトリの名前と、zip 形式のファイルの場所を指定します。 次に例を示します。

   ```R
   install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
   ```

   このコマンドはローカルの ZIP ファイルから R パッケージ `mynewpackage` を抽出し、このパッケージをインストールします。 パッケージに依存関係がある場合、インストーラーはライブラリ内の既存のパッケージを確認します。 依存関係を含むリポジトリを作成した場合は、必要なパッケージもインストーラーによってインストールされます。

   > [!NOTE]
   > 必要なパッケージがインスタンス ライブラリに存在せず、zip 形式のファイルに見つからない場合、ターゲット パッケージのインストールは失敗します。

**miniCRAN** の代替手段として、次の手順を手動で実行することもできます。

1. パッケージのすべての依存関係を特定します。
1. 必要なすべてのパッケージが既にサーバーにインストールされているかどうかを確認します。 パッケージがインストールされている場合は、バージョンが正しいことを確認します。
1. パッケージとすべての依存関係を、インターネットにアクセスできる別のコンピューターにダウンロードします。
1. パッケージと依存関係を 1 つのパッケージ アーカイブに配置します。
1. アーカイブがまだ ZIP 形式になっていない場合は、ZIP 圧縮します。
1. サーバーからアクセス可能なフォルダーにファイルを移動します。
1. サポートされているインストール コマンドまたは DDL ステートメントを実行して、インスタンス ライブラリにパッケージをインストールします。

## <a name="see-also"></a>参照

+ [R パッケージ情報の取得](r-package-information.md)
+ [R パッケージを使用するためのヒント](tips-for-using-r-packages.md)
+ [SQL Server の R 言語のチュートリアル](../tutorials/r-tutorials.md)