---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: 91252fc0789825beda34467d117d7a840d074acb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072764"
---
## <a name="prerequisites"></a>前提条件

R カスタム ランタイムをインストールする前に、次のものをインストールします。

+ Linux 用 SQL Server 2019 をインストールします。 SQL Server は、Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES)、および Ubuntu にインストールできます。 詳細については、[SQL Server on Linux のインストール ガイダンス](../../../linux/sql-server-linux-setup.md)を参照してください。

+ SQL Server 2019 の累積的な更新プログラム (CU) 3 以降にアップグレードします。 次の手順に従います。
    1. 累積的な更新プログラムのリポジトリを構成します。 詳細については、「[SQL Server on Linux のインストールとアップグレードを行うためのリポジトリを構成する](../../../linux/sql-server-linux-change-repo.md)」を参照してください。

    1. **mssql-server** パッケージを、最新の累積更新プログラムに更新します。 詳細については、[「SQL Server on Linux のインストール ガイド」の「SQL Server の更新またはアップグレード」](../../../linux/sql-server-linux-setup.md#upgrade)を参照してください。
