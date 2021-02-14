---
title: mssql-cli
description: mssql-cli は、Windows、macOS、または Linux 上で実行される SQL Server 用の対話型コマンドライン クエリ ツールです。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein, maghan
ms.custom: tools|mssql-cli
ms.date: 02/22/2018
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 1514c776944b66757a23baf06bb5169f66171f2d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033522"
---
# <a name="mssql-cli-command-line-query-tool-for-sql-server-preview"></a>SQL Server 用 mssql-cli コマンドライン クエリ ツール (プレビュー)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

mssql-cli は、SQL Server のクエリを実行するための対話型コマンドライン ツールであり、Windows、macOS、または Linux 上で実行されます。

## <a name="install-mssql-cli"></a>mssql-cli をインストールする

インストール手順の詳細については、[インストール ガイド](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)を参照してください。 最も一般的なインストール シナリオは以下のようにまとめられます。

### <a name="windows-and-macos-installation"></a>Windows と macOS のインストール

mssql-cli は `pip` を利用し、Windows と macOS にインストールされます。

```$ pip install mssql-cli```

手順の詳細については、[インストール ガイド](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)を参照してください。

### <a name="linux-installation"></a>Linux インストール

Microsoft リポジトリの登録後、mssql-cli は、複数の Linux ディストリビューションでパッケージマネージャーを使用してインストールしたり、アップグレードしたりできます。

次の例は Ubuntu 18.04 (Bionic) に当てはまります。その他のディストリビューションの詳細や例は[インストール ガイド](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)にあります。

```
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod

# Update the list of products
sudo apt-get update

# Install mssql-cli
sudo apt-get install mssql-cli

# Install missing dependencies
sudo apt-get install -f
```

## <a name="mssql-cli-documentation"></a>mssql-cli ドキュメント

mssql-cli のドキュメントは、[mssql-cli GitHub リポジトリ](https://github.com/dbcli/mssql-cli)にあります。

- [メイン ページ/readme](https://github.com/dbcli/mssql-cli)
- [インストール ガイド](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)
- [使用ガイド](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)

その他のドキュメントは、[doc フォルダー](https://github.com/dbcli/mssql-cli/tree/master/doc)にあります。
