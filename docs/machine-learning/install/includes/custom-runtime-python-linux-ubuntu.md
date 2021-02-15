---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0c0efdc599574748112c1d5909404603de24da2c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072950"
---
## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

次のコマンドを実行して、Python カスタム ランタイムに使用される Ubuntu Linux に [SQL Server 言語拡張機能](../../../language-extensions/language-extensions-overview.md)をインストールします。

1. 可能であれば、次のコマンドを実行して、インストールの前にシステム上のパッケージを更新しておきます。

    ```bash
    # Install as root or sudo
    sudo apt-get update
    ```

1. Ubuntu には、https apt transport オプションがない可能性があります。 これをインストールするには、次のコマンドを実行します。

    ```bash
    # Install as root or sudo
    apt-get install apt-transport-https
    ```

1. 次のコマンドを使用して **mssql-server-extensibility** をインストールします。

    ```bash
    # Install as root or sudo
    sudo apt-get install mssql-server-extensibility
    ```

## <a name="install-python-37-and-pandas"></a>Python 3.7 と pandas をインストールする

Python カスタム ランタイムに使用される Python 言語拡張機能では、現在、[Python 3.7](https://www.python.org/) のみがサポートされています。 別のバージョンの Python を使用する場合は、[Python 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python)の指示に従って、拡張機能を変更し、再構築してください。

1. 次のコマンドを実行して、Python 3.7 をインストールします。

    ```bash
    # Install python3.7 and the corresponding library:
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt-get update
    sudo apt-get install python3.7 python3-pip libpython3.7
    ```

1. 次のコマンドを実行して、pandas パッケージをインストールします。

    ```bash
    # Install pandas to /usr/lib:
    sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
    ```
