---
title: ログ配布を可用性グループに変換する前提条件
description: ログ配布を Always On 可用性グループに変換するために必要な前提条件の説明。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: cawrites
ms.author: chadam
ms.openlocfilehash: 90ede0e93644a87d11ef25ec1c2113076ff0bba2
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584068"
---
# <a name="prerequisites-to-convert-log-shipping-to-always-on-availability-groups"></a>ログ配布を Always On 可用性グループに変換する前提条件
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  このトピックでは、ログ配布プライマリ データベースと 1 つまたは複数のセカンダリ データベースを、AlwaysOn プライマリ データベースとセカンダリ データベースに変換するための前提条件について説明します。  
  
> [!NOTE]  
>  可用性グループのプライマリまたはセカンダリ データベース (場合によっては読み取り可能) は、ログ配布プライマリ データベースとして構成できます。  
  
  
##  <a name="availability-group-prerequisites"></a><a name="AGPrereqsRealAddress"></a> 可用性グループの前提条件  
 バックアップ ジョブを可用性グループのプライマリ レプリカ上で実行できるようにするには、AlwaysOn 可用性グループの次のバックアップ設定を使用します。  
  
|プロパティ|設定|  
|--------------|-------------|  
|可用性グループの自動バックアップ設定|[プライマリ レプリカ上のみ]|  
|プライマリ レプリカのバックアップの優先順位。|>0|  
  
 **詳細:**  
  
 [可用性グループのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
 [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="log-shipping-prerequisites"></a><a name="LogShipPrereqs"></a> ログ配布の前提条件  
  
-   ログ配布プライマリ データベースは、可用性グループの初期/現在のプライマリ レプリカをホストしている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに存在している必要があります。  
  
-   AlwaysOn セカンダリ データベースに変換するには、ログ配布セカンダリ データベースは次の条件を満たしている必要があります。  
  
    -   プライマリ データベースと同じ名前を使用している。  
  
    -   可用性グループのセカンダリ レプリカをホストしているサーバー インスタンスに存在している。  
  
 バックアップ ジョブをプライマリ データベース上で実行した後は、バックアップ ジョブを無効にし、復元ジョブを特定のセカンダリ データベース上で実行した後は、復元ジョブを無効にします。  
  
 可用性グループのすべてのセカンダリ データベースを作成した後、セカンダリ レプリカにバックアップを実行する場合は、可用性グループの自動バックアップ設定を再構成する必要があります。  
  
 **詳細:**  
  
 [可用性グループへのログ配布構成の変換](/archive/blogs/sqlalwayson/converting-a-logshipping-configuration-to-availability-group) (SQL Server ブログ)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **ログ配布**  
  
-   [SQL Server 2016 へのログ配布のアップグレード &#40;Transact-SQL&#41;](../../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [ログ配布の削除 &#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
 **Always On 可用性グループ**  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [可用性グループへのログ配布構成の変換](/archive/blogs/sqlalwayson/converting-a-logshipping-configuration-to-availability-group)  
  
     [Add a Log Shipping Primary Database and Secondary Database(s) to an Existing Availability Group](/archive/blogs/sqlalwayson/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group)  
  
     [SQL Server Always On チームのブログ: SQL Server Always On チームのオフィシャル ブログ](/archive/blogs/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](/archive/blogs/psssql/)  
  
-   **ホワイト ペーパー:**  
  
     [移行ガイド: 以前の配置の結合データベース ミラーリングとログ配布から AlwaysOn 可用性グループに移行する](/previous-versions/sql/sql-server-2012/jj635217(v=msdn.10))  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://social.technet.microsoft.com/wiki/contents/articles/13146.white-paper-gallery-for-sql-server.aspx#[Category]SQLServer2012)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
