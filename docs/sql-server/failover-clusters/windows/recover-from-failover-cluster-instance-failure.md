---
title: フェールオーバー クラスター インスタンス障害からの復旧
description: SQL Server でフェールオーバーが発生した後にフェールオーバー クラスター マネージャー スナップインを使用して、フェールオーバー クラスター インスタンスのフェールオーバーから復旧する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- clusters [SQL Server], recovery from failure
- failover clustering [SQL Server], recovery from failure
- hardware failures [SQL Server]
- recovering failover cluster failures [SQL Server]
ms.assetid: 3d151d0c-e841-4325-8606-c094de37d7d1
author: cawrites
ms.author: chadam
ms.openlocfilehash: 7d747370e5daf2b26d9508e0ca681eae77523e6e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127597"
---
# <a name="recover-from-failover-cluster-instance-failure"></a>フェールオーバー クラスター インスタンス障害からの復旧
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]でフェールオーバーが発生した後にフェールオーバー クラスター マネージャー スナップインを使用してクラスター障害から復旧する方法について説明します。 フェールオーバー クラスター マネージャー スナップインは、Windows Server フェールオーバー クラスタリング (WSFC) サービスのクラスター管理アプリケーションです。  
  
-   [修復不可能な障害からの復旧](#Scenario1)  
  
-   [ソフトウェア障害からの復旧](#Scenario2)  
  
##  <a name="recover-from-an-irreparable-failure"></a><a name="Scenario1"></a> 修復不可能な障害からの復旧  
 修復不可能な障害から復旧するには、次の手順に従います。 この障害の原因としては、ディスク コントローラーやオペレーティング システムの異常などが考えられます。 この例では、2 ノード クラスターのノード 1 でハードウェア障害が発生したものとします。  
  
1.  ノード 1 で障害が発生した後、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI がノード 2 にフェールオーバーされます。  
  
2.  FCI からノード 1 を削除します。 そのためには、ノード 2 でフェールオーバー クラスター マネージャー スナップインを開きます。ノード 1 を右クリックし、 **[移動アクション]** をクリックし、 **[ノードの削除]** をクリックします。  
  
3.  ノード 1 がクラスターの定義から削除されたことを確認します。  
  
4.  新しいハードウェアをインストールし、ノード 1 で故障したハードウェアと交換します。  
  
5.  フェールオーバー クラスター マネージャー スナップインを使用して、ノード 1 を既存のクラスターに追加します。 詳細については、「 [フェールオーバー クラスタリングをインストールする前に](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)」を参照してください。  
  
6.  管理者アカウントは、すべてのクラスター ノードで同じになるようにします。  
  
7.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行してノード 1 を FCI に追加します。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
##  <a name="recover-from-a-reparable-failure"></a><a name="Scenario2"></a> 修復可能な障害からの復旧  
 修復可能な障害から復旧するには、次の手順に従います。 このケースでは、障害の原因はダウンまたはオフラインになっているノード 1 です。ただし、復旧できないほどの損傷ではありません。 この障害の原因としては、オペレーティング システム、ハードウェア、または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス自体の障害が考えられます。  
  
1.  ノード 1 で障害が発生した後、FCI がノード 2 にフェールオーバーされます。  
  
2.  ノード 1 の問題を解決します。  
  
3.  すべてのノードがオンライン状態であり、WSFC サービスが動作していることを確認します。  
  
4.  復旧したノードに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をフェールオーバーします。  
  
  
