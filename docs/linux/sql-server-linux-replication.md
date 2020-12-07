---
title: Linux 上の SQL Server レプリケーション
description: SQL Server 2017 (14.x) (CU18) 以降では、SQL Server on Linux のインスタンス用の SQL Server レプリケーションがサポートされています。
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 7faa2b0101ee1f54484fce2a0756812a4ad611e1
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785012"
---
# <a name="sql-server-replication-on-linux"></a>Linux 上の SQL Server レプリケーション

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) 以降では、SQL Server on Linux のインスタンス用の SQL Server レプリケーションがサポートされています。

SQL Server Management Studio (SSMS) の[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)を使用して、Linux 上でレプリケーションを構成します。

SQL Server インスタンスは、任意のレプリケーション ロールに参加できます。

* Publisher
* ディストリビューター
* サブスクライバー (Subscriber)

レプリケーション スキーマでは、オペレーティング システムのプラットフォームを混在させて一致させることができます。 たとえば、レプリケーション スキーマにパブリッシャーとディストリビューターの SQL Server on Linux インスタンスを含めることができ、サブスクライバーに Windows 上と Linux 上の SQL Server インスタンスを含めることができます。

Linux 上の SQL Server インスタンスは、任意の種類のレプリケーションに参加できます。

* トランザクション
* スナップショット

レプリケーションの詳細については、[SQL Server レプリケーションのドキュメント](../relational-databases/replication/sql-server-replication.md)を参照してください。

## <a name="supported-features"></a>サポートされている機能

次のレプリケーション機能がサポートされています。

* スナップショット レプリケーション
* トランザクション レプリケーション
* 既定以外のポートを使用するレプリケーション <!--Add link to explanation-->
* AD 認証を使用するレプリケーション
* Windows と Linux 間でのレプリケーションの構成
* トランザクション レプリケーションの即時更新

## <a name="limitations"></a>制限事項

次の機能はサポートされていません。

* マージ レプリケーション
* ピア ツー ピア レプリケーション
* Oracle パブリッシュ

## <a name="next-steps"></a>次のステップ

[Linux 上で SQL Server レプリケーションを構成する](sql-server-linux-replication-tutorial-tsql.md)

[サンプル:Linux 上で SQL Server レプリケーションを構成する](sql-server-linux-replication-configure.md)
