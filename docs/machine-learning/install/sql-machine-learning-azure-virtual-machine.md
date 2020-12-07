---
title: Azure 仮想マシンにインストールする
description: Azure クラウドの仮想マシンの SQL Server Machine Learning Services で、Python と R のデータ サイエンス ソリューションおよび機械学習ソリューションを実行できます。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/02/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 576a19cf5a86893c248f11897f9a2d83a80598bc
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956973"
---
# <a name="install-sql-server-machine-learning-services-with-python-and-r-on-an-azure-virtual-machine"></a>Azure 仮想マシンに SQL Server Machine Learning Services と共に Python および R をインストールする
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Azure の仮想マシンに SQL Server Machine Learning Services と共に Python および R をインストールする方法について説明します。 これにより、Machine Learning Services のインストールと構成タスクが不要になります。

次の手順に従います。

1. Azure に SQL Server 仮想マシンをプロビジョニングする
1. ファイアウォールのブロックを解除する
1. リモート クライアントの ODBC コールバックを有効にする
1. ネットワーク プロトコルを追加する

## <a name="provision-sql-server-virtual-machine-in-azure"></a>Azure に SQL Server 仮想マシンをプロビジョニングする

詳細な手順については、「[Azure portal で Windows SQL Server 仮想マシンをプロビジョニングする方法](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)」を参照してください。 

Machine Learning Services をお使いのインスタンスに追加する手順は、「[SQL Server の設定を構成する](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings)」にあります。

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>ファイアウォールのブロックを解除する

既定では、Azure 仮想マシン上のファイアウォールには、ローカル ユーザー アカウントのネットワーク アクセスをブロックする規則が含まれます。

リモートのデータ サイエンス クライアントから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにアクセスできるようにするために、この規則を無効にする必要があります。  このようにしないと、仮想マシンのワークスペースを使用するコンピューティング コンテキストで機会学習コードを実行できなくなります。

リモートのデータ サイエンス クライアントからのアクセスを有効にするには、次の手順に従います。

1. 仮想マシン で、[セキュリティが強化された Windows ファイアウォール] を開きます。
2. **[送信の規則]** を選択します
3. 次の規則を無効にします。
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>リモート クライアントの ODBC コールバックを有効にする

サーバーを呼び出すクライアントから、機械学習ソリューションの一部として ODBC クエリを発行する必要がある場合は、リモート クライアントの代わりに Launchpad から ODBC 呼び出しを実行できるようにする必要があります。 

これを行うには、スタート パッドによって使用される SQL ワーカー アカウントがインスタンスにログインするできるようにする必要があります。 詳細については、[データベース ユーザーとしての SQLRUserGroup の追加](../security/create-a-login-for-sqlrusergroup.md)に関する記事を参照してください。

<a name="network"></a>

## <a name="add-network-protocols"></a>ネットワーク プロトコルを追加する

+ 名前付きパイプを有効にする
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] では、クライアントとサーバー コンピューター間の接続 (および一部の内部接続) に、名前付きパイプ プロトコルが使用されます。 名前付きパイプが有効になっていない場合は、Azure 仮想マシンと、サーバーに接続するデータ サイエンス クライアントの両方に名前付きパイプをインストールし、有効化する必要があります。
  
+ TCP/IP を有効にする

  TCP/IP は、ループバック接続に必要です。 "DBNETLIB; SQL Server が存在しないか、アクセスが拒否されました" というエラーが発生した場合、インスタンスをサポートする仮想マシンで TCP/IP を有効にしてください。