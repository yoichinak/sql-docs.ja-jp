---
title: レプリケーションの設定 (SSMS)
description: Linux 上で SQL Server レプリケーションを構成する方法について説明します。 SQL Server Management Studio (SSMS) または Transact-SQL ストアド プロシージャを使用して、レプリケーションを構成します。
ms.custom: seo-dt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
titleSuffix: SQL Server on Linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0c4a22b43650292055a7b1c48b9408b4d8e85f6c
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785052"
---
# <a name="configure-sql-server-replication-on-linux"></a>Linux 上で SQL Server レプリケーションを構成する

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] では、SQL Server on Linux インスタンス用の SQL Server レプリケーションが導入されています。

レプリケーションの詳細については、[SQL Server レプリケーションのドキュメント](../relational-databases/replication/sql-server-replication.md)を参照してください。

SQL Server Management Studio (SSMS) または Transact-SQL ストアド プロシージャを使用して、Linux 上でレプリケーションを構成します。

* SSMS を使用するには、この記事の指示に従ってください。

  Windows オペレーティング システム上で SSMS を使用して SQL Server のインスタンスに接続します。 背景と手順については、[SSMS を使用した SQL Server on Linux の管理](./sql-server-linux-manage-ssms.md)に関する記事を参照してください。
  
* ストアド プロシージャの例については、[Linux での SQL Server レプリケーションの構成](sql-server-linux-replication-tutorial-tsql.md)に関するチュートリアルを参照してください。

## <a name="prerequisites"></a>前提条件

パブリッシャー、ディストリビューター、およびサブスクライバーを構成する前に、SQL Server インスタンスの構成手順をいくつか完了する必要があります。

1. SQL Server エージェントがレプリケーション エージェントを使用できるようにします。 すべての Linux サーバー上で、ターミナルで次のコマンドを実行します。

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. SQL Server インスタンスをレプリケーション用に構成します。 SQL Server インスタンスをレプリケーション用に構成するには、レプリケーションに参加しているすべてのインスタンス上で `sys.sp_MSrepl_createdatatypemappings` を実行します。

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. スナップショット フォルダーを作成します。 SQL Server エージェントには、読み取り/書き込みを行うスナップショット フォルダーが必要です。 ディストリビューターにスナップショット フォルダーを作成します。

  スナップショット フォルダーを作成し、`mssql` ユーザーにアクセス権を付与するには、次のコマンドを実行します。

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を使用してレプリケーションを構成および監視する

### <a name="configure-the-distributor"></a>ディストリビューターの構成
  
ディストリビューターを構成するには: 

1. SSMS 上のオブジェクト エクスプローラーで SQL Server のインスタンスに接続します。

1. **[レプリケーション]** を右クリックし、**[ディストリビューションを構成する]** をクリックします。

1. **ディストリビューションの構成ウィザード**で次の手順を行います。

### <a name="create-publication-and-articles"></a>パブリケーションとアーティクルを作成する

パブリケーションとアーティクルを作成するには:

1. オブジェクト エクスプローラーで、 **[レプリケーション]**  >  **[ローカル パブリケーション]** >  **[新しいパブリケーション]** の順にクリックします。

1. **パブリケーションの新規作成ウィザード**の指示に従って、レプリケーションの種類と、パブリケーションに属するアーティクルを構成します。

### <a name="configure-the-subscription"></a>サブスクリプションを構成する

オブジェクト エクスプローラーでサブスクリプションを構成するには、 **[レプリケーション]**  >  **[ローカル サブスクリプション]** >  **[新しいサブスクリプション]** の順にクリックします。

### <a name="monitor-replication-jobs"></a>レプリケーション ジョブを監視する

レプリケーション モニターを使用して、レプリケーション ジョブを監視します。

オブジェクト エクスプローラーで、**[レプリケーション]** を右クリックし、**[レプリケーション モニターの起動]** をクリックします。

## <a name="next-steps"></a>次のステップ

[概念:Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)

[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
