---
title: SQL Server ビッグ データ クラスターの HDFS 階層アクセス許可
titleSuffix: Manage HDFS tiering permissions for SQL Server Big Data Clusters
description: 他の Linux ベースのシステムに対するアクセス許可など、SQL Server ビッグ データ クラスターでの HDFS 階層のセキュリティを管理します。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ef2a1097d07494ca74ed2afe50c93922de83838c
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257172"
---
# <a name="manage-hdfs-permissions-for-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] の HDFS アクセス許可を管理する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

ファイル システムとしての HDFS は、ファイルのアクセス許可に POSIX を使用する Linux ベースのファイル システムに似ています。 従来の POSIX アクセス許可モデルに加えて、HDFS では POSIX アクセス制御リスト (ACL) もサポートされています。 詳細については、[Apache Hadoop の ACL に関する記事](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_.28Access_Control_Lists.29)を参照してください。

次のセクションでは、[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] を使用して、HDFS ファイルとディレクトリのアクセス許可を管理する方法の例を示します。

## <a name="prerequisites"></a>前提条件

- [展開済みのビッグ データ クラスター](deployment-guidance.md)
- [ビッグ データ ツール](deploy-big-data-tools.md)
  
## <a name="hdfs-shell"></a>HDFS シェル

[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] の `hdfs` シェル機能を使用すると、コマンドをシェルで直接発行して、ファイルやディレクトリに対する HDFS アクセス許可を管理できます。 基になるメカニズムでは WebHdfs 呼び出しを使用して、コマンドを発行します

次のコマンドではシェルを開きます。

```bash
azdata bdc hdfs shell
```

`hdfs` シェルのヘルプにアクセスし、コマンドを発行する方法を理解するには、シェルがアクティブになってから次のコマンドを実行します。

```bash
[hdfs] ?
```

次の例では、ディレクトリの作成、ディレクトリの一覧表示、ディレクトリに対するアクセス許可の変更、および名前付きユーザー `bob` へのディレクトリ `sales` の読み取り、書き込み、実行アクセス権の付与方法を示します。

```bash
[hdfs] mkdir sales
[hdfs] ls
rwxr-xr-x  hdfs bdcadmins        0 Oct 09 18:02 system/
rwxrwxr-x admin bdcadmins        0 Oct 10 16:47 sales/
--xrwxrwxrwx  hdfs bdcadmins        0 Oct 09 18:03 tmp/
rwxrwxrwx  hdfs bdcadmins        0 Oct 09 17:59 user/

[hdfs] acl modify  '/sales/' 'user:bob:rwx'
acl modify: Change completed.
[hdfs] acl status  '/sales/'
{
  `AclStatus`: {
    `entries`: [
      `user:bob:rwx`,
      `group::r-x`
    ],
    `group`: `bdcadmins`,
    `owner`: `admin`,
    `permission`: `775`,
    `stickyBit`: false
  }
}
```

## <a name="create-a-directory-in-hdfs-using-azure-data-cli-azdata"></a>[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] を使用して HDFS にディレクトリを作成する

パス `/sales` に `data` というディレクトリを作成します。

```bash
azdata bdc hdfs mkdir --path '/sales/data'
```

## <a name="change-owner-of-a-directory-or-file"></a>ディレクトリまたはファイルの所有者を変更する

HDFS でディレクトリ `data` の所有ユーザーを変更し、 *`alice`* を所有ユーザーに、 *`salesgroup`* を所有グループにします。 所有者を変更するには、所有者である必要があります。

```bash
azdata bdc hdfs chown --owner alice --group 'salesgroup' --path '/sales/data'
```

## <a name="change-permissions-of-a-file-or-directory-with-chmod"></a>`chmod` でファイルまたはディレクトリのアクセス許可を変更する

`chmod` を使用して、ファイルやディレクトリ (所有者、所有グループなど) のアクセス許可を変更します。 詳細については、[Linux ファイル システムに対するアクセス許可の変更](https://www.lifewire.com/uses-of-command-chmod-2201064)に関するページを参照してください。 hdfs でのパターンは同じです。 次に例を示します。

```bash
azdata bdc hdfs chmod --permission 750 --path /sales/data
```

```bash
azdata bdc hdfs chmod --permission 775 --path /sales/data/file.txt
```

## <a name="set-sticky-bit-on-directories"></a>ディレクトリにスティッキー ビットを設定する

意図しないファイルの削除や再配置を防ぐために、ディレクトリにスティッキー ビットを設定します。 スティッキー ビットでは、ファイルを削除または移動するアクセス許可を、スーパーユーザー、ディレクトリ所有者、またはファイル所有者に制限します。 この設定はファイルには影響しません。 以下の例では、アクセス許可の前に `1` を付けて、ディレクトリ `users` にスティッキー ビットを設定しています。

```bash
azdata bdc hdfs chmod --path /sales/users --permission 1750
```

## <a name="setting-acls-on-files-and-directories"></a>ファイルとディレクトリへの ACL の設定

HDFS 内のファイルとディレクトリに ACL を設定するには、[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] コマンドを使用します。

ディレクトリに ACL を設定し、名前付きユーザー *`tom`* に、ディレクトリ *`data`* に対する読み取り、書き込み、実行アクセス権を付与します。 

> [!NOTE]
> `set` コマンドを使用する場合は、所有ユーザーや所有グループなどの ACL 仕様を含む、完全な ACL 仕様を必ず指定してください。

```bash
azdata bdc hdfs acl set --path '/sales' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-'
```

## <a name="default-acl-on-directories"></a>ディレクトリの既定の ACL

既定の ACL を使用すると、サブディレクトリで親ディレクトリからアクセス許可を継承できます。 既定の ACL を指定できるのは、ディレクトリのみです。 新しいファイルまたはサブディレクトリが作成されるときに、その親の既定の ACL が自動的に独自のアクセス許可 ACL に継承されます。 この方法では、新しいサブディレクトリが作成されると、既定の ACL が任意の深さのディレクトリ レベルにわたって継承されます。

以下は、azdata を使用して既定の ACL を設定する方法の例です。

```bash
azdata bdc hdfs acl set --path '/sale' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-,default:group::rw-,default:user::rw-,default:other::rw-'
```

## <a name="next-steps"></a>次のステップ

- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] リファレンス](../azdata/reference/reference-azdata.md)

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)