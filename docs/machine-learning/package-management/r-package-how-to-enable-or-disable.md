---
title: R パッケージのリモート管理を有効または無効にする
description: SQL Server 2016 R Services または SQL Server Machine Learning Services 上の R パッケージのリモート管理を有効にします (データベース内)
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 1b3c857d5ba86fa1cb10097cf91ee5d591b67f94
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869910"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>SQL Server のパッケージのリモート管理を有効または無効にする
[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

この記事では、クライアント ワークステーションまたは別の Machine Learning Server から R パッケージのリモート管理を有効にする方法について説明します。 SQL Server でパッケージ管理機能が有効になったら、クライアントで RevoScaleR コマンドを使用して SQL Server にパッケージをインストールできます。

既定では、SQL Server の外部パッケージ管理機能は無効になっています。 次のセクションで説明するように、別のスクリプトを実行してこの機能を有効にする必要があります。

## <a name="overview-of-process-and-tools"></a>プロセスとツールの概要

SQL Server でパッケージ管理を有効または無効にするには、コマンドライン ユーティリティ **RegisterRExt.exe** を使用します。これは、**RevoScaleR** パッケージに含まれています。

この機能を[有効にする](#bkmk_enable)には、データベース管理者が 2 段階のプロセスを実行する必要があります。まず、SQL Server インスタンスでパッケージ管理を有効にし (SQL Server インスタンスごとに 1 回)、次に SQL データベースでパッケージ管理を有効にします (SQL Server データベースごとに 1 回)。

パッケージ管理機能を[無効にする](#bkmk_disable)場合も、複数の手順が必要です。まず、データベースレベルのパッケージとアクセス許可を削除し (データベースごとに 1 回)、次にサーバーからロールを削除します (インスタンスごとに 1 回)。

## <a name="enable-package-management"></a><a name="bkmk_enable"></a> パッケージ管理を有効にする

1. SQL Server で、管理者特権でコマンド プロンプトを開き、RegisterRExt.exe ユーティリティが格納されているフォルダーに移動します。 既定の場所は `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` です。

2. 次のコマンドを実行して、環境に適した引数を指定します。

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    このコマンドにより、パッケージ管理に必要なインスタンスレベルのオブジェクトが SQL Server コンピューターに作成されます。 また、インスタンスの Launchpad の再起動も行われます。

    インスタンスを指定しない場合は、既定のインスタンスが使用されます。 ユーザーを指定しない場合は、現在のセキュリティ コンテキストが使用されます。 たとえば、次のコマンドにより、コマンド プロンプトを開いたユーザーの資格情報を使用して、既定のインスタンスのパッケージ管理が有効になります。

    `REgisterRExt.exe /install pkgmgmt`

3. 特定のデータベースにパッケージ管理を追加するには、管理者特権のコマンド プロンプトから次のコマンドを実行します。

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    このコマンドにより、ユーザーのアクセス許可を制御するために使用されるデータベース ロール (`rpkgs-users`、`rpkgs-private`、`rpkgs-shared` など) を含む、いくつかのデータベース成果物が作成されます。

    たとえば、次のコマンドにより、既定のインスタンスで、データベースのパッケージ管理が有効になります。 ユーザーを指定しない場合は、現在のセキュリティ コンテキストが使用されます。

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. パッケージをインストールする必要があるデータベースごとに、このコマンドを繰り返します。

5. 新しいロールが正常に作成されたことを確認するには、SQL Server Management Studio でデータベースをクリックし、 **[セキュリティ]** 、 **[データベース ロール]** の順に展開します。

    sys.database_principals に対して、次のようにクエリを実行することもできます。

    ```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

この機能を有効にしたら、リモートの R クライアントから RevoScaleR 関数を使用して、パッケージをインストールまたはアンインストールすることができます。

## <a name="disable-package-management"></a><a name="bkmk_disable"></a> パッケージ管理を無効にする

1. 管理者特権のコマンド プロンプトから、RegisterRExt ユーティリティを再度実行して、データベース レベルでパッケージ管理を無効にします。

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    このコマンドにより、指定したデータベースからパッケージ管理に関連するデータベース オブジェクトが削除されます。 また、このコマンドにより、SQL Server コンピューター上の保護ファイル システムの場所からインストールされたすべてのパッケージも削除されます。

2. このコマンドは、パッケージ管理が使用されていたデータベースごとに繰り返す必要があります。

3.  (省略可能) 前の手順ですべてのデータベースからパッケージを削除したら、管理者特権のコマンド プロンプトから次のコマンドを実行します。

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    このコマンドにより、インスタンスからパッケージ管理機能が削除されます。 変更を確認するには、Launchpad サービスを手動でもう一度再起動する必要がある場合があります。

## <a name="next-steps"></a>次のステップ

+ [RevoScaleR を使用して R パッケージをインストールする](install-r-packages-with-revoscaler.md)
+ [R パッケージ情報の取得](r-package-information.md)
+ [R パッケージを使用するためのヒント](tips-for-using-r-packages.md)
