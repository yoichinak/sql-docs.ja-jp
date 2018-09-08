---
title: フェールオーバー クラスタリングと Always On 可用性グループ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
caps.latest.revision: 48
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e75e0f70138c2ef6d783e72e80cfd0544f1bfa5e
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2018
ms.locfileid: "40406048"
---
# <a name="failover-clustering-and-always-on-availability-groups-sql-server"></a>フェールオーバー クラスタリングと Always On 可用性グループ (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

   [!INCLUDE[sssql11](../../../includes/sssql11-md.md)] で導入された [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] (High Availability and Disaster Recovery) ソリューションには、Windows Server フェールオーバー クラスタリング (WSFC) が必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] はフェールオーバー クラスタリングには依存しませんが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、フェールオーバー クラスタリング インスタンス (FCI) を使用して、可用性グループの可用性レプリカをホストすることもできます。 実際に [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 環境を設計する際は、それぞれのクラスタリング テクノロジの役割を知り、注意点を把握しておくことが大切です。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の概念については、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   [Windows Server フェールオーバー クラスタリング](#WSFC)  
  
-   [SQL Server フェールオーバー クラスタリング](#SQLServerFC)  
  
-   [WSFC フェールオーバー クラスター マネージャーを使用した可用性グループの操作に関する制限事項](#FCMrestrictions)  
  
##  <a name="WSFC"></a> Windows Server フェールオーバー クラスタリングと可用性グループ  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を配置するには、Windows Server フェールオーバー クラスタリング (WSFC) クラスターが必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが WSFC ノード上に存在し、WSFC クラスターとノードがオンライン状態である必要があります。 さらに、特定の可用性グループの各可用性レプリカが、同じ WSFC クラスターの異なるノード上に存在する必要があります。 唯一の例外は、別の WSFC クラスターに移行するときに、可用性グループは一時的に 2 つのクラスターにまたがることができるという点です。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] では、特定の可用性グループに属している可用性レプリカの現在のロールを監視、管理したり、フェールオーバー イベントが可用性レプリカに及ぼす影響を判断したりするために、 Windows Server フェールオーバー クラスタリング (WSFC) クラスターが使用されます。 WSFC リソース グループは、作成されたすべての可用性グループに対して作成されます。 WSFC クラスターは、このリソース グループを監視して、プライマリ レプリカの正常性を評価します。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のクォーラムは、クラスター ノードが可用性レプリカをホストしているかどうかに関係なく、WSFC クラスター内のすべてのノードに基づきます。 データベース ミラーリングとは異なり、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]には監視ロールはありません。  
  
 WSFC クラスターの全体的な正常性は、クラスター内のノードのクォーラムの投票によって決定されます。 災害や永続的なハードウェア障害または通信障害が原因で WSFC クラスターがオフラインになった場合は、管理操作を手動で行う必要があります。 Windows Server または WSFC クラスターの管理者は、クォーラムを強制し、稼動しているクラスター ノードをフォールト トレラントではない構成でオンラインに戻す必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] レジストリ キーは WSFC クラスターのサブキーです。 WSFC クラスターを削除してから再作成した場合は、元の WSFC クラスター上の可用性レプリカをホストしていた [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の各インスタンスについて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能を無効にしてから再度有効にする必要があります。  
  
 Windows Server フェールオーバー クラスタリング (WSFC) ノードでの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の実行および WSFC クォーラムについては、「[Windows Server フェールオーバー クラスタリング &#40;WSFC&#41;  と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)」を参照してください。  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) と可用性グループ  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングを WSFC クラスターと共に実装することにより、サーバー インスタンス レベルで第 2 のフェールオーバー レイヤーをセットアップできます。 可用性レプリカは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスまたは FCI インスタンスでホストできます。 特定の可用性グループのレプリカをホストできる FCI パートナーは 1 つに限られます。 可用性レプリカが FCI で実行されている場合、可用性グループの有効な所有者の一覧には、アクティブな FCI ノードだけが含まれます。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、共有ストレージの形態には依存しません。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) を使用して 1 つまたは複数の可用性レプリカをホストする場合、各 FCI では標準の SQL Server フェールオーバー クラスター インスタンスのインストールと同様、共有ストレージが必要になります。  
  
 追加の前提条件の詳細については、「[Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」の「SQL Server のフェールオーバー クラスター インスタンス (FCI) を使用して可用性レプリカをホストするための前提条件と制限」を参照してください。  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>フェールオーバー クラスター インスタンスと可用性グループの比較  
 FCI のノードの数に関係なく、FCI 全体は可用性グループ内の 1 つのレプリカをホストします。 次の表に、FCI 内のノードと可用性グループ内のレプリカの概念の違いについて説明します。  
  
||FCI 内のノード|可用性グループ内のレプリカ|  
|-|-------------------------|-------------------------------------------|  
|**WSFC クラスターを使用する**|はい|はい|  
|**保護レベル**|インスタンス|データベース|  
|**ストレージの種類**|共有|非共有<br /><br /> 可用性グループ内のレプリカがストレージを共有しない一方、FCI によってホストされるレプリカは、FCI によって必要とされたときに共有ストレージ ソリューションを使用します。 ストレージ ソリューションは、可用性グループのレプリカ間ではなく、FCI 内のノードでのみ共有されます。|  
|**ストレージ ソリューション**|直接接続、SAN、マウント ポイント、SMB|ノードの種類によって異なる|  
|**読み取り可能なセカンダリ**|いいえ*|はい|  
|**該当するフェールオーバー ポリシー設定**|WSFC クォーラム<br /><br /> FCI 固有<br /><br /> 可用性グループ設定**|WSFC クォーラム<br /><br /> 可用性グループ設定|  
|**フェールオーバー リソース**|サーバー、インスタンス、およびデータベース|データベースのみ|  
  
 *可用性グループ内の同期セカンダリ レプリカは、常に対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上で実行されていますが、FCI 内のセカンダリ ノードは、実際には対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを起動していないため、読み取り不可能です。 FCI 内のセカンダリ ノードは、FCI フェールオーバー中にリソース グループの所有権が転送されたときにのみ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを起動します。 ただし、アクティブな FCI ノードにおいて、FCI によってホストされるデータベースが可用性グループに属している場合にローカルな可用性グループが読み取り可能なセカンダリ レプリカとして実行されていると、データベースは読み取り可能です。  
  
 **可用性グループのフェールオーバー ポリシー設定は、スタンドアロン インスタンスと FCI インスタンスのどちらでホストされているかに関係なく、すべてのレプリカに適用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の各エディションにおけるフェールオーバー クラスタリング内の**ノード数**および **Always On 可用性グループ**の詳細については、「[SQL Server 2012 の各エディションがサポートする機能](http://go.microsoft.com/fwlink/?linkid=232473)」(http://go.microsoft.com/fwlink/?linkid=232473) を参照してください。  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>FCI で可用性レプリカをホストする場合の考慮事項  
  
> [!IMPORTANT]  
>  SQL Server フェールオーバー クラスター インスタンス (FCI) で可用性レプリカをホストすることを計画している場合は、Windows Server 2008 ホスト ノードが Always On の前提条件およびフェールオーバー クラスター インスタンス (FCI) の制限を満たしていることを確認してください。 詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
 場合により、すべてのノードで使用できない共有ディスクを含めるように Windows Server フェールオーバー クラスタリング (WSFC) クラスターを構成する必要があります。 たとえば、3 つのノードを持つ 2 つのデータ センター間の WSFC クラスターを検討します。 ノードのうちの 2 つは、プライマリ データ センター内の SQL Server フェールオーバー クラスタリング インスタンス (FCI) をホストし、同じ共有ディスクにアクセスできます。 3 つ目のノードは、別のデータ センター内の SQL Server のスタンドアロン インスタンスをホストし、プライマリ データ センターの共有ディスクにはアクセスできません。 この WSFC クラスター構成では、FCI でプライマリ レプリカがホストされ、スタンドアロン インスタンスでセカンダリ レプリカがホストされる場合に可用性グループの配置がサポートされます。  
  
 特定の可用性グループの可用性レプリカをホストするために FCI を選択する場合は、FCI フェールオーバーによって 1 つの WSFC ノードで同じ可用性グループの 2 つの可用性レプリカをホストする操作が試行されないように注意してください。  
  
 この構成によってどのような問題が起きるかを次のサンプル シナリオに示します。  
  
 Marcel は、 `NODE01` と `NODE02`の 2 つのノードから成る WSFC クラスターを構成しています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス `fciInstance1`は、 `NODE01` と `NODE02` の両方にインストールされています。 `NODE01` の現在の所有者は `fciInstance1`です。  
 Marcel は、 `NODE02`に、別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス `Instance3`をインストールすることにしました。Instance3 はスタンドアロン インスタンスです。  
 Marcel は、 `NODE01`で、fciInstance1 に対する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にしました。 `NODE02`では、 `Instance3` に対する [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を有効にしました。 さらに、可用性グループをセットアップしました。この可用性グループは、 `fciInstance1` がプライマリ レプリカをホストするためだけでなく、 `Instance3` がセカンダリ レプリカをホストするためにも使用されます。  
 あるとき、 `fciInstance1` 上の `NODE01`が利用できなくなり、WSFC クラスターによって、 `fciInstance1` が `NODE02`にフェールオーバーされたとします。 フェールオーバー後の `fciInstance1` は、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]上でプライマリ ロールとして動作する `NODE02`対応のインスタンスです。 しかし、この時点で `Instance3` は、 `fciInstance1`と同じ WSFC ノードに存在します。 これは [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の制約に違反します。  
 このシナリオで起きる問題を回避するには、スタンドアロン インスタンス ( `Instance3`) が、 `NODE01` や `NODE02`と同じ WSFC クラスター内の別のノードに存在している必要があります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスタリングの詳細については、「[Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
##  <a name="FCMrestrictions"></a> WSFC フェールオーバー クラスター マネージャーを使用した可用性グループの操作に関する制限事項  
 フェールオーバー クラスター マネージャーを使用して可用性グループを操作しないでください。次に例を示します。  
  
-   可用性グループのクラスター化されたサービス (リソース グループ) のリソースの追加や削除を行わないでください。  
  
-   可用性グループのプロパティ (たとえば、有効な所有者、優先所有者) を変更しないでください。 これらのプロパティは、可用性グループによって自動的に設定されます。  
  
-   フェールオーバー クラスター マネージャーを使用して可用性グループを他のノードに移動したり可用性グループをフェールオーバーしたりしないでください。 フェールオーバー クラスターは可用性レプリカの同期状態を認識しないため、そのような操作を行うとダウンタイムが長くなることがあります。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用する必要があります。  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [制限付きセキュリティを使用した SQL Server 用 Windows フェールオーバー クラスタリング (可用性グループまたは FCI) の構成](https://blogs.msdn.microsoft.com/sqlalwayson/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security/)  
  
     [SQL Server Always On チームのブログ: SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](http://blogs.msdn.com/b/psssql/)  
  
-   **ホワイトペーパー:**  
  
     [Always On アーキテクチャ ガイド: フェールオーバー クラスター インスタンスと可用性グループの使用による高可用性および障害復旧ソリューションの構築](http://msdn.microsoft.com/library/jj215886.aspx)  
  
     [高可用性と障害復旧のための Microsoft SQL Server Always On ソリューション ガイド](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](http://sqlcat.com/)  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
