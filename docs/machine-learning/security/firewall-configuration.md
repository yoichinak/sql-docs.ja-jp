---
title: ファイアウォールの構成
description: SQL Server Machine Learning Services からの発信接続のためのファイアウォールを構成する方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/17/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f8cf14b294c85f90b0e44375f751a84a50b30e04
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180419"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services のファイアウォール構成
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

この記事では、Machine Learning Services を使用する場合に管理者またはアーキテクトが念頭に置く必要がある、ファイアウォールの構成に関する考慮事項を示します。

## <a name="default-firewall-rules"></a>既定のファイアウォール規則

既定では、SQL Server Setup はファイアウォール規則を作成することにより、送信接続を無効にします。

SQL Server 2016 および2017 では、これらの規則はローカル ユーザー アカウントに基づいており、そこではセットアップが **SQLRUserGroup** のためにアウトバウンド規則を作成し、メンバーへのネットワーク アクセスを拒否しています (各ワーカー アカウントは、規則に従いローカル原則として一覧表示されていました)。 SQLRUserGroup の詳細については、「[SQL Server Machine Learning Services の機能拡張フレームワークのセキュリティの概要](../../machine-learning/concepts/security.md#sqlrusergroup)」に関するページを参照してください。

SQL Server 2019 では、AppContainers への移行の一環として、AppContainer SID に基づく新しいファイアウォール規則があります。これは、SQL Server セットアップで作成された 20 の AppContainers のそれぞれに 1 つずつあります。 ファイアウォール規則名の名前付け規則は、**Block network access for AppContainer-00 in SQL Server instance MSSQLSERVER** です。ここで、00 は AppContainer の番号 (既定では 00-20) で、MSSQLSERVER は SQL Server インスタンスの名前です。

> [!Note]
> ネットワーク呼び出しが必要な場合は、Windows ファイアウォールでアウトバウンド規則を無効にすることができます。

## <a name="restrict-network-access"></a>ネットワーク アクセスを制限する

既定のインストールでは、外部ランタイム プロセスからのすべての送信ネットワーク アクセスをブロックするために Windows ファイアウォール規則が使用されます。 外部ランタイム プロセスが、パッケージのダウンロードやその他の悪意のある可能性があるネットワーク呼び出しを行うことを防ぐために、ファイアウォール規則を作成する必要があります。

別のファイアウォール プログラムを使用している場合にも、ローカル ユーザー アカウント用、またはユーザー アカウント プールに代表されるグループ用の規則を設定することで、外部ランタイムの送信ネットワーク接続をブロックするための規則を作成できます。

R または Python ランタイムによる無制限のネットワーク アクセスを制限するには、Windows ファイアウォール (または別のファイアウォール) を有効にすることを強くお勧めします。

## <a name="next-steps"></a>次のステップ

[受信接続用に Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)