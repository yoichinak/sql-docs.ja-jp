---
title: SQL Server インスタンスの可用性グループ機能を有効にする
description: SQL Server インスタンスの Always On 可用性グループ機能を有効にする方法について説明します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: cawrites
ms.author: chadam
ms.openlocfilehash: f45626f82de0e1754ed34a515f9daeb68c54fbb8
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584540"
---
# <a name="enable-the-always-on-availability-group-feature-for-a-sql-server-instance"></a>SQL Server インスタンスの Always On 可用性グループ機能を有効にする
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] でサポートするために [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] のインスタンスを構成する際の要件について説明します。  
  
> [!IMPORTANT]  
>  Windows Server フェールオーバー クラスタリング (WSFC) ノードおよび [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の前提条件と制限に関する基本情報については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
   
##  <a name="terms-and-definitions"></a><a name="TermsAndDefinitions"></a> 用語と定義  
 [Always On 可用性グループ](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューション。 *可用性グループ* は、 *可用性データベース* として知られる、ひとまとまりでフェールオーバーされる個別のユーザー データベースのセットのためのフェールオーバー環境をサポートします。  
  
 可用性レプリカ  
 可用性グループのインスタンス化。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスによってホストされ、可用性グループに属する各可用性データベースのローカル コピーを保持します。 可用性グループには、2 種類の可用性レプリカ ( *プライマリ レプリカ* と 1 ～ 4 つの *セカンダリ レプリカ*) があります。 可用性グループの可用性レプリカをホストするサーバー インスタンスは、同じ Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の別のノードにある必要があります。  
  
 [データベース ミラーリング エンドポイント](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 エンドポイントとは、SQL Server でネットワーク経由の通信を行うことができるようにする SQL Server オブジェクトです。 データベース ミラーリングおよび [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に参加する場合、サーバー インスタンスには特別な専用のエンドポイントが必要です。 サーバー インスタンスのすべてのミラーリングと可用性グループの接続は、同じデータベース ミラーリング エンドポイントを使用します。 このエンドポイントの用途は特殊で、他のサーバー インスタンスからこれらの接続を受信するためにのみ使用されます。  
  
##  <a name="to-configure-a-server-instance-to-support-always-on-availability-groups"></a><a name="ConfigSI"></a> Always On 可用性グループをサポートするようにサーバー インスタンスを構成するには  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]をサポートする場合、サーバー インスタンスは、可用性グループをホストする WSFC フェールオーバー クラスター内のノードにあり、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] が有効になっていて、データベース ミラーリング エンドポイントを持っている必要があります。  
  
1.  可用性グループに追加するすべてのサーバー インスタンスの Always On 可用性グループ機能を有効にします。 特定の可用性グループの特定のサーバー インスタンスがホストできる可用性レプリカは 1 つだけです。  
  
2.  サーバー インスタンスに、データベース ミラーリング エンドポイントが存在することを確認します。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **Always On 可用性グループを有効にするには**  
  
-   [AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **データベース ミラーリング エンドポイントが存在するかどうかを確認するには**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
 **データベース ミラーリング エンドポイントを作成するには**  
  
-   [AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [AlwaysOn - HADRON 学習シリーズ: HADRON 対応データベースのワーカー プールの使用](/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)  
  
     [SQL Server Always On チームのブログ: SQL Server Always On チームのオフィシャル ブログ](/archive/blogs/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](/archive/blogs/psssql/)  
  
-   **ビデオ:**  
  
     [Microsoft SQL Server コード ネーム "Denali" Always On シリーズ パート 1: 次世代の高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" AlwaysOn シリーズ パート 2: AlwaysOn を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ホワイト ペーパー:**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://social.technet.microsoft.com/wiki/contents/articles/13146.white-paper-gallery-for-sql-server.aspx#[Category]SQLServer2012)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Always On 可用性グループ: 相互運用性 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [フェールオーバー クラスタリングと Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
