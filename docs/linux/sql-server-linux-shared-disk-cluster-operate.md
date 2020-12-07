---
title: FCI の手動フェールオーバー - SQL Server on Linux
description: SQL Server on Linux (具体的には、Red Hat Linux Enterprise、Ubuntu、Suse Linux Enterprise Server) 上のフェールオーバー クラスター インスタンス (FCI) を手動でフェールオーバーする方法について説明します。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: c37157d47e2eddaaf47f787de364603cbaaa250a
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785096"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>フェールオーバー クラスター インスタンスの操作 - SQL Server on Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、Linux で SQL Server フェールオーバー クラスター インスタンス (FCI) を操作する方法について説明します。 Linux に SQL Server FCI を作成していない場合は、「[フェールオーバー クラスター インスタンスの構成 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)」をご覧ください。 

## <a name="failover"></a>[フェールオーバー]

FCI のフェールオーバーは、Windows Server フェールオーバー クラスター (WSFC) に似ています。 FCI がホストされているクラスター ノードで何らかの障害が発生した場合、FCI を自動的に別のノードにフェールオーバーする必要があります。 WSFC とは異なり、優先所有者を設定する方法がないため、Pacemaker によって FCI の新しいホストとなるノードが選択されます。

FCI を別のノードに手動でフェールオーバーすることが必要になる場合があります。 そのプロセスは、WSFC 上の FCI と同じではありません。 WSFC では、ロール レベルでリソースをフェールオーバーします。 Pacemaker では、ユーザーが移動するリソースを選択し、すべての制約が正しいと仮定すると、他のすべてのものも同様に移動されます。 

フェールオーバーの方法は、Linux のディストリビューションによって異なります。 お使いの Linux ディストリビューションの指示に従ってください。

- [RHEL または Ubuntu](#manual-failover-rhel-or-ubuntu)
- [SLES](#manual-failover-sles)

## <a name="manual-failover-rhel-or-ubuntu"></a>手動フェールオーバー (RHEL または Ubuntu)

Red Hat Enterprise Linux (RHEL) サーバーまたは Ubuntu サーバーで手動フェールオーバーを実行するには、次の手順を実行します。
1.  次のコマンドを実行します。 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName> は、SQL Server FCI の Pacemaker リソース名です。

   \<NewHostNode> は、FCI をホストするクラスター ノードの名前です。 

   受信確認は受け取りません。

2.  手動フェールオーバーの間に、Pacemaker によって、手動で移動するように選択したリソースに対して場所の制約が作成されます。 この制約を見るには、`sudo pcs constraint` を実行します。

3.  フェールオーバーが完了した後、`sudo pcs resource clear <FCIResourceName>` を発行して制約を削除します。 

\<FCIResourceName> は、FCI の Pacemaker リソース名です。 

## <a name="manual-failover-sles"></a>手動フェールオーバー (SLES)


Suse Linux Enterprise Server (SLES) では、SQL Server FCI を手動でフェールオーバーするには、`migrate` コマンドを使います。 次に例を示します。

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName> は、フェールオーバー クラスター インスタンスのリソース名です。 

\<NewHostNode> は、新しいフェールオーバー先ホストの名前です。 


<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

--->

## <a name="next-steps"></a>次の手順

- [フェールオーバー クラスター インスタンスの構成 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
