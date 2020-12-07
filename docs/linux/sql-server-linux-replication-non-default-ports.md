---
title: レプリケーション スナップショット フォルダーを構成する (既定以外のポート)
titleSuffix: SQL Server on Linux
description: Linux 上の SQL Server レプリケーションに対して、既定以外のポートでスナップショット フォルダーの共有を構成する方法について説明します。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a945b716b6de0d4fcb61ccbfd296eded645243d4
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785029"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>既定以外のポートを使用してレプリケーションを構成する (SQL Server Linux)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Linux インスタンス上で、network.tcpport mssql-conf 設定を使用して構成された任意のポートをリッスンする SQL Server とのレプリケーションを構成できます。 次の条件に該当する場合は、構成時にポートをサーバー名に追加する必要があります。

1. レプリケーションのセットアップに、SQL Server on Linux のインスタンスが含まれる
2. すべてのインスタンス (Windows または Linux) が既定以外のポートをリッスンしている。 

インスタンスのサーバー名は、インスタンス上で @@servername を実行することで見つけることができます。 サーバー名の代わりに IP アドレスを使用しないでください。 パブリッシャー、ディストリビューター、またはサブスクライバーの IP アドレスを使用すると、エラーが発生する可能性があります。

> [!NOTE]
> Linux 上で既定以外のポートを使用して SQL Server レプリケーションを作成することは、SQL Server 2019 以降でのみ機能します。

## <a name="examples"></a>例

'Server1' は、Linux 上でポート 1500 をリッスンします。 ディストリビューション用に 'Server1' を構成するには、`@distributor` を使用して `sp_adddistributor` を実行します。 次に例を示します。 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' は、Linux 上でポート 1500 をリッスンします。 ディストリビューターのパブリッシャーを構成するには、`@publisher` を使用して `sp_adddistpublisher` を実行します。 次に例を示します。

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' は、Linux 上でポート 6549 をリッスンします。 'Server2' をサブスクライバーとして構成するには、`@subscriber` を使用して `sp_addsubscription` を実行します。 次に例を示します。

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' は、Windows 上で、サーバー名 Server3、インスタンス名 MSSQL2017 を使用してポート 6549 をリッスンします。 'Server3' をサブスクライバーとして構成するには、`@subscriber` を使用して `sp_addsubscription` を実行します。 次に例を示します。

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>次のステップ

[概念:Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)

[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

