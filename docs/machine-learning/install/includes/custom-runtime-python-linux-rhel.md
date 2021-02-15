---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: c6d15087150e914e62b5d19951715198ced47512
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072926"
---
## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

次のコマンドを実行して、Python カスタム ランタイムに使用される Red Hat Enterprise Linux (RHEL) に [SQL Server 言語拡張機能](../../../language-extensions/language-extensions-overview.md)をインストールします。

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

## <a name="install-python-37-and-pandas"></a>Python 3.7 と pandas をインストールする

Python カスタム ランタイムに使用される Python 言語拡張機能では、現在、[Python 3.7](https://www.python.org/) のみがサポートされています。 別のバージョンの Python を使用する場合は、[Python 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python)の指示に従って、拡張機能を変更し、再構築してください。

1. 次のコマンドを実行して、Python 3.7 をインストールします。

    ```bash
    # Install python3.7 and the corresponding library:
    yum install gcc openssl-devel bzip2-devel libffi-devel zlib-devel
    
    cd /usr/src
    wget https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tgz
    tar xzf Python-3.7.9.tgz
    
    cd Python-3.7.9
    ./configure --enable-optimizations --prefix=/usr
    make altinstall
    ```

1. 次のコマンドを実行して、pandas パッケージをインストールします。

    ```bash
    # Install pandas to /usr/lib:
    sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
    ```
