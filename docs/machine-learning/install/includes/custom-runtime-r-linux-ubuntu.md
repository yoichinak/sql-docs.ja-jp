---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: 83b39be5be128ba4fbda17765a7b67deead2c80c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072788"
---
## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

次のコマンドを実行して、R カスタム ランタイムに使用される Ubuntu Linux に [SQL Server 言語拡張機能](../../../language-extensions/language-extensions-overview.md)をインストールします。

1. 可能であれば、次のコマンドを実行して、インストールの前にシステム上のパッケージを更新しておきます。

    ```bash
    # Install as root or sudo
    sudo apt-get update
    ```

1. 次のコマンドを使用して **mssql-server-extensibility** をインストールします。

    ```bash
    # Install as root or sudo
    sudo apt-get install mssql-server-extensibility
    ```

## <a name="install-r"></a>R のインストール

1. [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、R が既に `/opt/microsoft/ropen/3.5.2/lib64/R` にインストールされています。 このパスを R_HOME として引き続き使用する場合は、この手順を省略できます。

    R の別のランタイムを使用する場合は、新しいバージョンのインストールを続ける前に、まず `microsoft-r-open-mro` を削除する必要があります。

    ```bash
    sudo apt remove microsoft-r-open-mro-3.5.2
    ```

1. Ubuntu 用の [R (3.3 以降)](https://www.r-project.org/) をインストールします。 既定では、R は **/usr/lib/R** にインストールされます。 このパスは **R_HOME** です。 R を別の場所にインストールする場合は、**R_HOME** としてそのパスを記録しておきます。

    Ubuntu 用の指示の例を次に示します。 お使いの R のバージョンに応じて、次のリポジトリの URL を変更します。

    ```bash
    export DEBIAN_FRONTEND=noninteractive
    sudo apt-get update
    sudo apt-get --no-install-recommends -y install curl zip unzip apt-transport-https libstdc++6
    
    # Add R CRAN repository. This repository works for R 4.0.x.
    #
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu xenial-cran40/'
    sudo apt-get update
    
    # Install R runtime.
    #
    sudo apt-get -y install r-base-core
    ```
