---
title: ファイル システムからの R パッケージの同期
description: SQL Server の R ライブラリを、ファイル システムにインストールされている新しいバージョンで更新します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 87ac1a75940de892e9796139a4ba0f08263da417
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870074"
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server の R パッケージの同期
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

SQL Server 2017 に含まれるバージョンの RevoScaleR には、パッケージが使用されるインスタンスやデータベースとファイル システムの間で R パッケージのコレクションを同期する機能が含まれています。

この機能は、SQL Server データベースに関連付けられている R パッケージ コレクションを容易にバックアップするために用意されています。 この機能を使用すると、管理者はデータベースだけでなく、そのデータベースで作業するデータ サイエンティストが使用していた R パッケージも復元できます。

この記事では、パッケージの同期機能について説明すると共に、[rxSyncPackages](/machine-learning-server/r-reference/revoscaler/rxsyncpackages) 関数を使用して、以下のタスクを実行する方法について説明します。

+ SQL Server データベース全体について、パッケージの一覧を同期します

+ 個々のユーザーまたはユーザー グループが使用するパッケージを同期します

+ ユーザーが別の SQL Server に移動した場合は、そのユーザーの作業データベースのバックアップを作成し、新しいサーバーに復元することができます。このユーザーのパッケージは、R での必要性に応じて、新しいサーバーのファイル システムにインストールされます。

たとえば、次のようなシナリオでパッケージの同期を使用できます。

+ DBA が SQL Server のインスタンスを新しいマシンに復元し、ユーザーに対して、R クライアントから接続して `rxSyncPackages` を実行し、パッケージの更新と復元を行うように求めている。

+ ファイル システム上の R パッケージが破損していると思われるため、SQL Server で `rxSyncPackages` を実行する。

## <a name="requirements"></a>必要条件

パッケージの同期を使用するには、適切なバージョンの Microsoft R または Machine Learning Server が必要です。 この機能は、Microsoft R バージョン9.1.0 以降で提供されています。 

また、サーバーで[パッケージ管理機能](r-package-how-to-enable-or-disable.md)を有効にする必要もあります。

### <a name="determine-whether-your-server-supports-package-management"></a>使用しているサーバーでパッケージ管理がサポートされているかどうかを判断する

この機能は、SQL Server 2017 CTP 2 以降で使用できます。

この機能を SQL Server 2016 のインスタンスに追加するには、最新バージョンの Microsoft R を使用するようにインスタンスをアップグレードします。詳細については、[SqlBindR.exe を使用した SQL Server R Services のアップグレード](../install/upgrade-r-and-python.md)に関するページをご覧ください。

### <a name="enable-the-package-management-feature"></a>パッケージ管理機能を有効にする

パッケージの同期を使用するには、SQL Server インスタンスと個々のデータベースで、新しいパッケージ管理機能が有効になっている必要があります。 詳細については、[SQL Server のパッケージ管理の有効化または無効化](r-package-how-to-enable-or-disable.md)に関する記事をご覧ください。

1. サーバー管理者が、SQL Server インスタンスでこの機能を有効にします。
2. 各データベースについては、管理者がデータベース ロールを使用して、個々のユーザーに R パッケージをインストールまたは共有する権限を付与します。

この処理が完了したら、[rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages) などの RevoScaleR 関数を使用して、データベースにパッケージをインストールできます。  ユーザーおよびユーザーが使用できるパッケージに関する情報は、SQL Server インスタンスに格納されます。 

パッケージ管理機能を使用して新しいパッケージを追加するたびに、SQL Server のレコードとファイル システムの両方が更新されます。 この情報は、データベース全体のパッケージ情報を復元する際に使用できます。

### <a name="permissions"></a>アクセス許可

+ パッケージ同期関数を実行するユーザーは、SQL Server インスタンスと、パッケージが含まれているデータベースのセキュリティ プリンシパルである必要があります。

+ 関数の呼び出し元は、パッケージ管理ロールの **rpkgs-shared** または **rpkgs-private** のメンバーである必要があります。

+ **共有** とマークされたパッケージを同期するには、その関数を実行しているユーザーが **rpkgs-shared** ロールのメンバーシップを持っている必要があります。また、移動されるパッケージは共有スコープ ライブラリにインストールされている必要があります。

+ **プライベート** とマークされたパッケージを同期するには、パッケージの所有者または管理者が関数を実行する必要があります。また、パッケージはプライベートである必要があります。

+ 他のユーザーの代わりにパッケージを同期するには、所有者が **db_owner** データベース ロールのメンバーである必要があります。

## <a name="how-package-synchronization-works"></a>パッケージの同期のしくみ

パッケージの同期を使用するには、[rxSyncPackages](/r-server/r-reference/revoscaler/rxsyncpackages)を呼び出します。これは [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) の新しい関数です。 

`rxSyncPackages` を呼び出すたびに、SQL Server インスタンスとデータベースを指定する必要があります。 次に、同期するパッケージの一覧またはパッケージのスコープを指定します。

1. `RxInSqlServer` 関数を使用して、SQL Server のコンピューティング コンテキストを作成します。 コンピューティング コンテキストを指定しない場合は、現在のコンピューティング コンテキストが使用されます。

2. 指定されたコンピューティング コンテキストで、インスタンス上のデータベースの名前を指定します。 パッケージはデータベースごとに同期されます。

3. スコープ引数を使用して、同期するパッケージを指定します。

    **プライベート** スコープを使用する場合は、指定された所有者が所有するパッケージのみが同期されます。 **共有** スコープを指定した場合、データベース内のすべての非プライベート パッケージが同期されます。 
    
    **プライベート** または **共有** スコープのいずれも指定せずに関数を実行すると、すべてのパッケージが同期されます。

4. コマンドが正常に実行された場合は、指定されたスコープと所有者を使用して、ファイル システム内の既存のパッケージがデータベースに追加されます。

    ファイル システムが破損している場合は、データベースに保持されている一覧に基づいてパッケージが復元されます。

    ターゲット データベースでパッケージ管理機能が使用できない場合は、次のエラーが発生します。"The package management feature is either not enabled on the SQL Server or version is too old (パッケージ管理機能が SQL Server で有効になっていないか、バージョンが古すぎます)"

### <a name="example-1-synchronize-all-package-by-database"></a>例 1. すべてのパッケージをデータベースごとに同期する

この例では、ローカル ファイル システムから新しいパッケージを取得し、データベース TestDB にパッケージをインストールします。 所有者が指定されていないため、一覧には、インストールされているすべてのパッケージ (プライベート スコープと共有スコープ) が含まれます。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>例 2. 同期されるパッケージをスコープで制限する

次の例では、指定したスコープ内のパッケージのみを同期します。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>例 3. 同期されるパッケージを所有者で制限する

次の例は、特定のユーザーに対してインストールされたパッケージのみを同期する方法を示しています。 この例では、ユーザーは SQL ログイン名 *user1* によって識別されます。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>関連リソース

[SQL Server の R パッケージの管理](install-additional-r-packages-on-sql-server.md)