---
title: 可用性グループの可用性モード
description: Always On 可用性グループの 3 つの異なる可用性モード (非同期コミットモード、同期コミットモード、構成のみモード) について学習します。
ms.custom: seo-lt-2019
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], asynchronous commit
- synchronous-commit availability mode
- Availability Groups [SQL Server], synchronous commit
- asynchronous-commit availability mode
- Availability Groups [SQL Server], availability modes
ms.assetid: 10e7bac7-4121-48c2-be01-10083a8c65af
author: cawrites
ms.author: chadam
ms.openlocfilehash: bb9a9743f6a23d75d7819fb4e48e4233ed2104fd
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584650"
---
# <a name="differences-between-availability-modes-for-an-always-on-availability-group"></a>Always On 可用性グループの可用性モードの違い
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の *可用性モード* は、可用性レプリカが同期コミット モードで動作できるかどうかを指定するレプリカのプロパティです。 可用性レプリカごとに、可用性モードを同期コミット モード、非同期コミット モード、または構成のみモードとして構成する必要があります。  プライマリ レプリカが *非同期コミット モード* で構成されている場合、プライマリ レプリカはセカンダリ レプリカによる受信トランザクション ログ レコードのディスクへの書き込みを ( *ログ書き込み*) 待機しません。 特定のセカンダリ レプリカが非同期コミット モードで構成されている場合、プライマリ レプリカはそのセカンダリ レプリカによるログ書き込みを待機しません。 プライマリ レプリカとセカンダリ レプリカの両方が *同期コミット モード* で構成されている場合、プライマリ レプリカはログが書き込まれたことをセカンダリ レプリカが確認するまで待機します (プライマリの *セッション タイムアウト期間* 内に、セカンダリ レプリカがプライマリ レプリカに対する ping に失敗した場合を除きます)。 
  

> [!NOTE]  
>  セカンダリ レプリカがプライマリのセッション タイムアウト期間を超えた場合、プライマリ レプリカはそのセカンダリ レプリカに対して一時的に非同期コミット モードに移行します。 セカンダリ レプリカがプライマリ レプリカと再接続すると、同期コミット モードが再開されます。  
  
##  <a name="supported-availability-modes"></a><a name="SupportedAvModes"></a> サポートされる可用性モード  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、次のように、非同期コミット モード、同期コミット モード、および構成のみモードの 3 種類の可用性モードをサポートします。  
  
-   *非同期コミット モード* は、可用性レプリカが離れた距離に分散されている場合に正常に利用できる災害復旧ソリューションです。 すべてのセカンダリ レプリカが非同期コミット モードで実行されている場合、プライマリ レプリカは、いずれかのセカンダリ レプリカによりログが書き込まれるまで待機しません。 ログ レコードがローカル ログ ファイルに書き込まれるとすぐに、プライマリ レプリカはクライアントにトランザクションの確認を送信します。 プライマリ レプリカは、非同期コミット モードが構成されているセカンダリ レプリカに対して、トランザクションの遅延を最小限に抑えて実行されます。  現在のプライマリに非同期コミット可用性モードが構成されている場合、このプライマリは、セカンダリの個々の可用性モードの設定に関係なく、すべてのセカンダリ レプリカに対してトランザクションを非同期にコミットします。  
  
     詳細については、このトピックの「 [非同期コミット可用性モード](#AsyncCommitAvMode)」を参照してください。  
  
-   *同期コミット モード* は、パフォーマンスよりも高可用性が重視され、トランザクションの遅延が増加するのが欠点です。 同期コミット モードでは、セカンダリ レプリカでログがディスクに書き込まれるまで、トランザクションの確認はクライアントに送信されません。 セカンダリ データベースでデータの同期が開始されると、セカンダリ レプリカで、対応するプライマリ データベースから受信したログ レコードの適用が開始されます。 すべてのログ レコードが書き込まれるとすぐに、セカンダリ データベースが SYNCHRONIZED 状態になります。 その後、すべての新しいトランザクションがセカンダリ レプリカによって書き込まれてから、ログ レコードがローカル ログ ファイルに書き込まれます。 特定のセカンダリ レプリカのすべてのセカンダリ データベースが同期されると、同期コミット モードでは、手動でのフェールオーバーがサポートされます (オプションで自動フェールオーバーがサポートされます)。  
  
     詳細については、このトピックの「 [同期コミット可用性モード](#SyncCommitAvMode)」を参照してください。  

-   "*構成のみモード*" は、Windows Server フェールオーバー クラスター上にない可用性グループに適用されます。 構成のみモードのレプリカには、ユーザー データは含まれません。 構成のみモードでは、レプリカの master データベースに可用性グループの構成メタデータが格納されます。 詳しくは、[構成のみのレプリカでの可用性グループ](../../../linux/sql-server-linux-availability-group-ha.md)に関するページをご覧ください。
  
 次の図には、5 つの可用性レプリカがある可用性グループを示しています。 プライマリ レプリカおよびセカンダリ レプリカの 1 つには、自動フェールオーバーが指定された同期コミット モードが構成されています。 もう 1 つのセカンダリ レプリカは、計画的な手動フェールオーバーのみが指定された同期コミット モードで構成されています。残りの 2 つのセカンダリ レプリカは、強制手動フェールオーバー (通常は *強制フェールオーバー* と呼ばれます) のみをサポートする非同期コミット モードで構成されています。  
  
 ![レプリカの可用性モードとフェールオーバー モード](../../../database-engine/availability-groups/windows/media/aoag-availabilityandfailovermodes.gif "レプリカの可用性モードとフェールオーバー モード")  
  
 2 つの可用性レプリカ間の同期およびフェールオーバー動作は、両方のレプリカの可用性モードに依存します。 たとえば、同期コミットを発生させるには、現在のプライマリ レプリカとセカンダリ レプリカの両方で同期コミットが構成されている必要があります。 同様に、自動フェールオーバーを発生させるには、両方のレプリカで自動フェールオーバーが構成されている必要があります。 上の配置シナリオについて、それぞれのプライマリ レプリカでの動作を次の表に示します。  
  
|現在のプライマリ レプリカ|自動フェールオーバー ターゲット|同期コミット モードの動作の対象|非同期コミット モードの動作の対象|自動フェールオーバー|  
|-----------------------------|--------------------------------|--------------------------------------------|---------------------------------------------|---------------------------------|  
|01|02|02 と 03|04|はい|  
|02|01|01 と 03|04|はい|  
|03||01 と 02|04|いいえ|  
|04|||01、02、03|いいえ|  
  
 通常、非同期コミット レプリカとしてのノード 04 が災害復旧サイトに配置されます。 ノード 04 にフェールオーバーした後もノード 01、02、03 は非同期コミット モードにとどまるため、2 つのサイト間の長いネットワーク待機時間が原因で可用性グループに生じるパフォーマンスの低下を回避できます。  
  
##  <a name="asynchronous-commit-availability-mode"></a><a name="AsyncCommitAvMode"></a> Asynchronous-Commit Availability Mode  
 *非同期コミット モード* では、セカンダリ レプリカがプライマリ レプリカと同期されることはありません。 特定のセカンダリ データベースが対応するプライマリ データベースからの遅れを取り戻す場合もありますが、セカンダリ データベースはどの時点でも遅延する可能性があります。 非同期コミット モードは、プライマリ レプリカから非常に離れた場所にセカンダリ レプリカがあり、軽度のエラーによるプライマリ レプリカへの影響でも不都合が生じる災害復旧シナリオ、または同期によるデータ保護よりもパフォーマンスの方が重要な場合に役立ちます。 また、プライマリ レプリカはセカンダリ レプリカから送信される確認を待機しないため、セカンダリ レプリカの問題がプライマリ レプリカに影響することはありません。  
  
 非同期コミット セカンダリ レプリカは、プライマリ レプリカから受信するログ レコードとの時間差を埋めようとします。 ただし、非同期コミット セカンダリ データベースは常に同期されていない状態であり、対応するプライマリ データベースよりも若干遅れる可能性があります。 通常、非同期コミット セカンダリ データベースと対応するプライマリ データベース間の時間差はわずかですが、 セカンダリ レプリカをホストするサーバーに負荷がかかり過ぎている場合やネットワークが低速の場合は、この時間差が大きくなります。  
  
 非同期コミット モードでサポートされるフェールオーバーは、強制フェールオーバーのみです (データ損失の可能性あり)。 フェールオーバーの強制は、現在のプライマリ レプリカが長期間使用できない状態のままであり、データを失うリスクよりもプライマリ データベースがすぐに使用できるようになることの方が重要である場合にのみ、最後の手段として使用します。フェールオーバー ターゲットとなるレプリカは、ロールが SECONDARY 状態または RESOLVING 状態であることが必要です。 フェールオーバー ターゲットはプライマリ ロールに移行し、データベースのコピーがプライマリ データベースになります。 元のプライマリ データベースが使用できるようになると、残りのセカンダリ データベースと元のプライマリ データベースは手動で個別に再開されるまで中断されます。 非同期コミット モードでは、元のプライマリ レプリカから元のセカンダリ レプリカにまだ送信されていなかったトランザクション ログはすべて失われます。 つまり、一部またはすべての新しいプライマリ データベースで、最近コミットされたトランザクションが欠落している可能性があります。 強制フェールオーバーのしくみと、強制フェールオーバーを使用する際のベスト プラクティスの詳細については、「 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)」を参照してください。  
  
##  <a name="synchronous-commit-availability-mode"></a><a name="SyncCommitAvMode"></a> Synchronous-Commit Availability Mode  
 同期コミット可用性モード (*同期コミット モード*) では、セカンダリ データベースは可用性グループに参加すると、対応するプライマリ データベースからの遅れを取り戻し、SYNCHRONIZED 状態になります。 データの同期が継続されている間は、セカンダリ データベースは SYNCHRONIZED のままです。 これにより、特定のプライマリ データベースでコミットされたすべてのトランザクションが、対応するセカンダリ データベースでもコミットされていることが保証されます。 特定のセカンダリ レプリカのすべてのセカンダリ データベースが同期されると、セカンダリ レプリカ全体の同期状態が HEALTHY になります。  
  
 **このセクションの内容**  
  
-   [データの同期が中断する要因](#DisruptSync)  
  
-   [セカンダリ レプリカでの同期のしくみ](#HowSyncWorks)  
  
-   [手動フェールオーバーのみを指定した同期コミット モード](#SyncCommitWithManual)  
  
-   [自動フェールオーバーを指定した同期コミット モード](#SyncCommitWithAuto)  
  
###  <a name="factors-that-disrupt-data-synchronization"></a><a name="DisruptSync"></a> データの同期が中断する要因  
 すべてのデータベースが同期されると、セカンダリ レプリカは HEALTHY 状態になります。 次のいずれかの状況にならない限り、同期されたセカンダリ レプリカは HEALTHY のままです。  
  
-   ネットワークやコンピューターの遅延または不具合が原因で、セカンダリ レプリカとプライマリ レプリカ間のセッションがタイムアウトになった。  
  
    > [!NOTE]  
    >  可用性レプリカのセッション時間プロパティの詳細については、「 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
-   セカンダリ レプリカ上のセカンダリ データベースを中断した。 セカンダリ レプリカの同期が行われなくなり、同期状態が NOT_HEALTHY としてマークされます。 中断されたセカンダリ データベースが再開されて再同期されるか、可用性グループから削除されるまで、セカンダリ レプリカを HEALTHY にすることはできません。  
  
-   プライマリ データベースを可用性グループに追加した。 以前に同期されたセカンダリ レプリカは NOT_HEALTHY 同期状態になります。 この状態は、少なくとも 1 つのデータベースが NOT SYNCHRONIZING 同期状態であることを示しています。 対応するセカンダリ データベースがレプリカ上で準備され、可用性グループに参加し、新しいプライマリ データベースと同期されるまで、特定のセカンダリ レプリカを HEALTHY にすることはできません。  
  
-   プライマリ レプリカまたはセカンダリ レプリカを非同期コミット可用性モードに変更した。 非同期コミット モードに変更すると、データの同期が継続されている間は、セカンダリ レプリカは HEALTHY 同期状態のままになります。 ただし、プライマリ レプリカのみを非同期コミット モードに変更すると、同期コミット セカンダリ レプリカは PARTIALLY_HEALTHY 同期状態になります。 この状態は、少なくとも 1 つのデータベースが SYNCHRONIZING 同期状態であり、NOT SYNCHRONIZING 状態のデータベースが 1 つもないことを示しています。  
  
-   セカンダリ レプリカを同期コミット可用性モードに変更した。 これにより、すべてのデータベースが SYNCHRONIZED 同期状態になるまで、 セカンダリ レプリカは PARTIALLY_HEALTHY 同期状態としてマークされます。  
  
> [!TIP]  
>  可用性グループ、可用性レプリカ、または可用性データベースの同期状態を確認するには、 **sys.dm_hadr_availability_group_states** 、 **sys.dm_hadr_availability_replica_states** 、または [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)それぞれの [synchronization_health](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)列または [synchronization_health_desc](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)列に対してクエリを実行します。  
  
###  <a name="how-synchronization-works-on-a-secondary-replica"></a><a name="HowSyncWorks"></a> セカンダリ レプリカでの同期のしくみ  
 同期コミット モードでは、セカンダリ レプリカは可用性グループに参加してプライマリ レプリカとのセッションを確立した後、受信したログ レコードをディスクに書き込み (*ログ書き込み*)、プライマリ レプリカに確認メッセージを送信します。 セカンダリ データベースの書き込まれたログがプライマリ データベースのログの末尾に追い付くと、セカンダリ データベースの状態は SYNCHRONIZED に設定されます。 同期に必要な時間は、主にセッションの開始時にセカンダリ データベースがプライマリ データベースからどれだけ遅れたか (プライマリ レプリカから最初に受信したログ レコード数によって測定)、プライマリ データベースのワークロード、およびセカンダリ レプリカをホストするサーバー インスタンスのコンピューター速度に依存します。  
  
 同期操作は次のように行われます。  
  
1.  プライマリ レプリカは、クライアントからトランザクションを受け取ると、そのトランザクションのログをトランザクション ログに書き込み、同時にログ レコードをセカンダリ レプリカに送信します。  
  
2.  ログ レコードがプライマリ データベースのトランザクション ログに書き込まれた後にトランザクションを元に戻すには、ログを受け取っていないセカンダリへのフェールオーバーがこの時点で存在している必要があります。 プライマリ レプリカは、同期コミット セカンダリ レプリカから送信される確認を待機します。  
  
3.  セカンダリ レプリカはログを書き込み、確認をプライマリ レプリカに返します。  
  
4.  プライマリ レプリカは、セカンダリ レプリカから確認を受け取ると、コミット処理を終了させ、確認メッセージをクライアントに送信します。  
  
    > [!NOTE]  
    >  同期コミット セカンダリ レプリカによってログが書き込まれたことを確認する前にタイムアウトになった場合、プライマリはそのセカンダリ レプリカを失敗としてマークします。 セカンダリ レプリカの接続状態は DISCONNECTED に変更され、プライマリ レプリカはセカンダリ レプリカから送信される確認の待機を停止します。 この動作により、失敗した同期コミット セカンダリ レプリカによってプライマリ レプリカのトランザクション ログの書き込みが実行できなくなることを回避します。  
  
 同期コミット モードでは、2 か所間のデータの同期を要求することによってデータを保護しますが、トランザクションの遅延が多少大きくなるというデメリットもあります。  
  
### <a name="synchronous-commit-mode-with-only-manual-failover"></a><a name="SyncCommitWithManual"></a> 手動フェールオーバーのみを指定した同期コミット モード  
 これらのレプリカが接続され、データベースが同期されている場合、手動フェールオーバーがサポートされます。 セカンダリ レプリカがダウンしても、プライマリ レプリカは影響を受けません。 SYNCHRONIZED 状態のレプリカが存在しない場合、プライマリ レプリカは公開された状態で (つまり、データをセカンダリ レプリカに送信せずに) 実行されます。 プライマリ レプリカが利用できなくなると、セカンダリ レプリカが RESOLVING 状態になりますが、データベース所有者はセカンダリ レプリカへの強制フェールオーバーを実行できます (データを損失する可能性もあります)。 詳細については、「 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
###  <a name="synchronous-commit-mode-with-automatic-failover"></a><a name="SyncCommitWithAuto"></a> 自動フェールオーバーを指定した同期コミット モード  
 自動フェールオーバーは、プライマリ レプリカが機能しなくなった後もデータベースをすぐに再度使用できるようにすることで、高可用性を実現します。 可用性グループを自動フェールオーバー用に構成するには、現在のプライマリ レプリカと少なくとも 1 つのセカンダリ レプリカの両方を、自動フェールオーバーを指定した同期コミット モードに設定する必要があります。 最大 3 つの自動フェールオーバー レプリカを所有することができます。  
  
 さらに、特定の時点で自動フェールオーバーを実行するには、このセカンダリ レプリカがプライマリ レプリカと同期されている (つまり、すべてのセカンダリ レプリカが同期されている) 必要があるだけでなく、Windows Server フェールオーバー クラスタリング (WSFC) クラスターがクォーラムを持っている必要もあります。 プライマリ レプリカが使用できなくなると、これらの条件で自動フェールオーバーが発生します。 セカンダリ レプリカはプライマリ ロールに切り替わり、そのデータベースをプライマリ データベースとして提供します。 詳細については、「[フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)」トピックの「自動フェールオーバー」セクションを参照してください。  
  
> [!NOTE]  
>  WSFC クォーラムと [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] については、「[WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)」を参照してください。  

### <a name="data-latency-on-secondary-replica"></a>セカンダリ レプリカでのデータ待機時間
セカンダリ レプリカへの読み取り専用アクセスの実装が役立つのは、読み取り専用ワークロードである程度のデータ待機時間を許容できる場合です。 データ待機時間が許容できない場合は、読み取り専用ワークロードをプライマリ レプリカに対して実行することを検討してください。

プライマリ レプリカは、プライマリ データベースでの変更のログ レコードをセカンダリ レプリカに送信します。 それぞれのセカンダリ データベースで、専用の再実行スレッドがログ レコードに適用されます。 読み取りアクセス セカンダリ データベースでは、その変更を含むログ レコードがセカンダリ データベースに適用され、トランザクションがプライマリ データベース上でコミットされない限り、特定のデータの変更はクエリ結果に反映されません。+

つまり、プライマリ レプリカとセカンダリ レプリカの間には待機時間 (通常は数秒程度) が発生します。 ただし、ネットワークの問題のためにスループットが低下するなどの特殊なケースでは、待機時間が長くなることがあります。 I/O ボトルネックが生じた場合やデータの移動が中断された場合は、待機時間が増加します。 データ移動の中断を監視する場合、[Always On ダッシュボード](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)または [sys.dm_hadr_database_replica_states 動的管理ビュー](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)を使用できます。

セカンダリ レプリカでの再実行待機時間の調査方法について詳しくは、[プライマリの変更がセカンダリ レプリカで反映されない場合のトラブルシューティング](../../../database-engine/availability-groups/windows/troubleshoot-primary-changes-not-reflected-on-secondary.md)に関するページを参照してください。
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **可用性モードとフェールオーバー モードを変更するには**  
  
-   [可用性レプリカの可用性モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカのフェールオーバー モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
 **クォーラム投票を調整するには:**  
  
-   [クラスター クォーラムの NodeWeight 設定を表示](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)  
  
-   [クラスター クォーラムの NodeWeight の設定の構成](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)  
  
-   [クォーラムを使用せずに WSFC クラスターを強制的に起動する](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
 **手動フェールオーバーを実行するには**  
  
-   [可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [可用性グループのフェールオーバー ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
 **可用性グループ、可用性レプリカ、およびデータベースの状態を確認するには**  
  
-   [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 関連コンテンツ  
  
-   [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
-   [SQL Server AlwaysOn チームのブログ: SQL Server AlwaysOn チームのオフィシャル ブログ](/archive/blogs/sqlalwayson/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
