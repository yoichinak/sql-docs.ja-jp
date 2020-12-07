---
title: T-SQL (CREATE EXTERNAL LIBRARY) を使用して R パッケージをインストールする
description: R パッケージを SQL Server 2016 R Services または SQL Server Machine Learning Services (データベース内) に追加します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: b525a2cd2a5450aec3df9a7d3157bc4aff05735f
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870117"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>T-SQL (CREATE EXTERNAL LIBRARY) を使用して SQL Server に R パッケージをインストールする
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

この記事では、機械学習が有効になっている SQL Server のインスタンスに、新しい Python パッケージをインストールする方法について説明します。 複数のアプローチから選択できます。 R に慣れていないサーバー管理者については、T-SQL を使用することをお勧めします。

[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md) ステートメントを使用すると、R または Python コードを直接実行せずに、パッケージまたはパッケージ セットを、インスタンスまたは特定のデータベースに追加できます。 ただし、この方法を使用するには、パッケージの準備と追加のデータベース権限が必要です。

+ すべてのパッケージが、インターネットからオンデマンドでダウンロードするのではなく、ローカルの zip 形式ファイルとして使用できる必要があります。

+ すべての依存関係が名前とバージョンで特定され、ZIP ファイルに含まれている必要があります。 ダウンストリーム パッケージの依存関係を含め、必要なパッケージが使用できない場合、ステートメントは失敗します。 

+ 自分が **db_owner** であるか、データベース ロールに CREATE EXTERNAL LIBRARY 権限がある必要があります。 詳細については、「[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)」を参照してください。

## <a name="download-packages-in-archive-format"></a>アーカイブ形式でパッケージをダウンロードする

1 つのパッケージをインストールする場合は、そのパッケージを zip 形式でダウンロードします。

パッケージの依存関係により、複数のパッケージをインストールする方が一般的です。 パッケージに他のパッケージが必要な場合は、インストール中にすべてのパッケージが相互にアクセスできることを確認する必要があります。 [miniCRAN](https://andrie.github.io/miniCRAN/) を使用して[ローカル リポジトリを作成](create-a-local-package-repository-using-minicran.md)し、パッケージの完全なコレクションをアセンブルすること、また [igraph](https://igraph.org/r/) を使用して、パッケージの依存関係を分析することをお勧めします。 間違ったバージョンのパッケージをインストールしたり、パッケージの依存関係を省略したりすると、CREATE EXTERNAL LIBRARY ステートメントが失敗することがあります。 

## <a name="copy-the-file-to-a-local-folder"></a>ファイルをローカル フォルダーにコピーする

すべてのパッケージを含む zip 形式のファイルを、サーバー上のローカル フォルダーにコピーします。 サーバー上のファイル システムへのアクセス権がない場合は、バイナリ形式を使用して、完全なパッケージを変数として渡すこともできます。 詳細については、「[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)」を参照してください。

## <a name="run-the-statement-to-upload-packages"></a>ステートメントを実行してパッケージをアップロードする

管理特権を持つアカウントを使用して、**クエリ** ウィンドウを開きます。

T-SQL ステートメント `CREATE EXTERNAL LIBRARY` を実行して、zip 形式のパッケージ コレクションをデータベースにアップロードします。

たとえば、次のステートメントは、**randomForest** パッケージを含む miniCRAN リポジトリとその依存関係を、パッケージ ソースとして指定します。 

```sql
CREATE EXTERNAL LIBRARY [randomForest]
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

任意の名前を使用することはできません。外部ライブラリ名には、パッケージの読み込み時または呼び出し時に使用する名前を指定する必要があります。

## <a name="verify-package-installation"></a>パッケージのインストールを確認する

ライブラリが正常に作成されている場合、ストアド プロシージャ内でパッケージを呼び出すと、SQL Server でパッケージを実行できます。
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>関連項目

+ [R パッケージ情報の取得](r-package-information.md)
+ [R のチュートリアル](../tutorials/r-tutorials.md)