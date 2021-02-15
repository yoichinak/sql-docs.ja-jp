---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: a10c54f61151835692f2bc05de440062fe2f3cfb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072793"
---
## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

次のコマンドを実行して、R カスタム ランタイムに使用される SUSE Linux Enterprise Server (SLES) に [SQL Server 言語拡張機能](../../../language-extensions/language-extensions-overview.md)をインストールします。

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-r"></a>R のインストール

1. [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、R が既に `/opt/microsoft/ropen/3.5.2/lib64/R` にインストールされています。 このパスを R_HOME として引き続き使用する場合は、この手順を省略できます。

    R の別のランタイムを使用する場合は、新しいバージョンのインストールを続ける前に、まず `microsoft-r-open-mro` を削除する必要があります。

    ```bash
    sudo zypper remove microsoft-r-open-mro-3.5.2
    ```

1. SUSE Linux Enterprise Server (SLES) 用に [R (3.3 以降)](https://www.r-project.org/) をインストールします。 既定では、R は **/usr/lib/R** にインストールされます。 このパスは **R_HOME** です。 R を別の場所にインストールする場合は、**R_HOME** としてそのパスを記録しておきます。
