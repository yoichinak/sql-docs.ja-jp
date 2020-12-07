---
title: '可用性グループ ウィザード: [レプリカの指定] ページ'
description: SQL Server Management Studio (SSMS) の新しい可用性グループ ウィザードに含まれる [レプリカの指定] ページのオプションについて説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.listeners.f1
- sql13.swb.addreplicawizard.specifyreplicas.f1
- sql13.swb.newagwizard.specifyreplicas.f1
ms.assetid: 2d90fc12-a67b-4bd0-b0ab-899b73017196
author: cawrites
ms.author: chadam
ms.openlocfilehash: 404d2afc78765adebb191c49fb58f6d390516a6c
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583891"
---
# <a name="specify-replicas-page-new-availability-group-wizard-add-replica-wizard"></a>[レプリカの指定] ページ (新しい可用性グループ ウィザード:レプリカの追加ウィザード)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 **[レプリカの指定]** ページのオプションについて説明します。 このページの対象は、 **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]** の **[!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]** です。 **[レプリカの指定]** ページを使用して、1 つまたは複数の可用性レプリカを指定および構成して可用性グループを追加します。 このページには、次の表に示す 4 つのタブが含まれます。 この表でタブの名前をクリックすると、このトピックの対応するセクションに移動します。  
  
|タブ|簡単な説明|  
|---------|-----------------------|  
|[レプリカ](#ReplicasTab)|このタブを使用して、セカンダリ レプリカを現在ホストしている、またはホストする予定である [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスを指定します。 現在接続しているサーバー インスタンスでプライマリ レプリカをホストする必要があることに注意してください。<br /><br /> 他のタブに進む前に、 **[レプリカ]** タブですべてのレプリカを指定してください。<br/><br/> クラスター タイプが **NONE** の場合、**自動フェールオーバー** は無効になります。 SQL Server は、可用性グループがクラスターに含まれないときに、手動フェールオーバーのみをサポートします。 <br/><br/> クラスター タイプが EXTERNAL の場合、フェールオーバー モードは **External** です。 <br/><br/> レプリカを追加するときは、新しいレプリカすべてが、既存のレプリカと同じオペレーティング システムの種類でホストされている必要があります。 <br/><br/>レプリカを追加するとき、プライマリ レプリカが WSFC にある場合、セカンダリ レプリカは同じクラスターに含まれていなければなりません。|
|[エンドポイント](#EndpointsTab)|このタブを使用して、既存の任意のデータベース ミラーリング エンドポイントを検証します。また、サービス アカウントが Windows 認証を使用しているサーバー インスタンスでエンドポイントが不足している場合は、エンドポイントを自動的に作成します。|  
|[バックアップの設定](#BackupPreferencesTab)|このタブを使用して、可用性グループ全体についてバックアップの設定を指定し、各可用性レプリカのバックアップ優先順位を指定します。|  
|[リスナー](#Listener)|このタブ (使用可能な場合) を使用して、可用性グループ リスナーを作成します。 既定では、リスナーは作成されません。<br /><br /> このタブは、 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]を実行している場合のみ使用できます。<br/><br/>クラスター タイプが EXTERNAL または NONE のいずれかの場合、DHCP は無効です。 |  
  
##  <a name="replicas-tab"></a><a name="ReplicasTab"></a> [レプリカ] タブ  
 **サーバー インスタンス**  
 可用性レプリカをホストするサーバー インスタンスの名前を表示します。  
  
 セカンダリ レプリカをホストするために使用するサーバー インスタンスが **[可用性レプリカ]** グリッドに表示されていない場合は、 **[レプリカの追加]** をクリックします。 ハイブリッド IT 環境で可用性グループを構成する場合は (「[Azure Virtual Machines での SQL Server の高可用性とディザスター リカバリー](/previous-versions/azure/jj870962(v=azure.100))」を参照)、 **[Azure のレプリカ追加]** ボタンをクリックして、セカンダリ レプリカを備えた仮想マシンを Azure に作成できます。  
  
 **[初期ロール]**  
 新しいレプリカが初期状態で実行するロール(**プライマリ** または **セカンダリ**) を示します。  
  
 **自動フェールオーバー (上限 3)**  
 この可用性レプリカを自動フェールオーバー パートナーにする場合のみ、このチェック ボックスをオンにします。 自動フェールオーバーを構成するには、最初のプライマリ レプリカと 1 つのセカンダリ レプリカに対してこのオプションを選択する必要があります。 どちらのレプリカでも同期コミット可用性モードが使用されます。 3 つのレプリカのみが自動フェールオーバーをサポートできます。  
  
 同期コミット可用性モードの詳細については、「[可用性モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。 自動フェールオーバーの詳細については、「[フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)」を参照してください。  
  
 **[同期コミット (上限 3)]**  
 レプリカに **[自動フェールオーバー (最大 3)]** を選択した場合、 **[同期コミット (最大 3)]** も選択されます。 このチェック ボックスがオフになっている場合は、このレプリカで同期コミット モードを計画的な手動フェールオーバーでのみ使用する場合に限り、オンにしてください。 3 つのレプリカのみが同期コミット モードを使用できます。  
  
 このレプリカで非同期コミット可用性モードを使用する場合、このチェック ボックスはオフのままにします。 レプリカは、強制手動フェールオーバー (データ損失の可能性あり) のみをサポートします。 非同期コミット可用性モードの詳細については、「[可用性モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。 計画的な手動フェールオーバーと強制手動フェールオーバーの詳細については、「[フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)」を参照してください。  
  
 **[読み取り可能セカンダリ ロール]**  
 **[読み取り可能セカンダリ]** ボックスの一覧から値を選択します。値は次のとおりです。  
  
 **いいえ**  
 このレプリカのセカンダリ データベースに対する直接接続は禁止されます。 読み取りアクセスで利用することはできません。 これが既定の設定です。  
  
 **[読み取り目的のみ]**  
 このレプリカのセカンダリ データベースに対する直接接続は、読み取り専用でのみ許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
 **はい**  
 読み取りアクセスに限り、このレプリカのセカンダリ データベースに対するすべての接続が許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
 **[レプリカの追加]**  
 クリックすると、セカンダリ レプリカが可用性グループに追加されます。  
  
 **[Azure のレプリカ追加]**  
 可用性グループのセカンダリ レプリカを実行する Azure 仮想マシンを作成する場合にクリックします。 このオプションは、オンプレミスのレプリカが含まれるハイブリッド IT 環境の可用性グループに対してのみ適用できます。 詳細については、「[Azure Virtual Machines での SQL Server の高可用性とディザスター リカバリー](/previous-versions/azure/jj870962(v=azure.100))」を参照してください。  
  
 **[レプリカの削除]**  
 クリックすると、選択したセカンダリ レプリカが可用性グループから削除されます。  
  
##  <a name="endpoints-tab"></a><a name="EndpointsTab"></a> [エンドポイント] タブ  
 **[エンドポイント]** タブには、可用性レプリカをホストする各サーバー インスタンスについて、既存のデータベース ミラーリング エンドポイント (存在する場合) の実際の値か、Windows 認証を使用する新しいエンドポイント候補の推奨値が表示されます。 既存のエンドポイントと候補となるエンドポイントの両方について、[エンドポイント値] グリッドには次の情報が表示されます。  
  
 **[サーバー名]**  
 可用性レプリカをホストするサーバー インスタンスの名前が表示されます。  
  
 **エンドポイント URL**  
 データベース ミラーリング エンドポイントの実際の URL または提案された URL が表示されます。 提案された新しいエンドポイントに対して、この値を変更することができます。 詳細については、「[可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)」を参照してください。  
  
 **[ポート番号]**  
 エンドポイントの実際のポート番号または提案されたポート番号が表示されます。 提案された新しいエンドポイントに対して、この値を変更することができます。  
  
 **[エンドポイント名]**  
 エンドポイントの実際の名前または提案された名前が表示されます。 提案された新しいエンドポイントに対して、この値を変更することができます。  
  
 **[データの暗号化]**  
 このエンドポイントに送信されるデータが暗号化されているかどうかを示します。 提案された新しいエンドポイントに対して、この設定を変更できます。  
  
 **[SQL Server サービス アカウント]**  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのユーザー名です。  
  
 Windows 認証を使用したエンドポイントをサーバー インスタンスが使用するためには、その [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントがドメイン アカウントである必要があります。  
  
 この要件によって、以降の構成手順が決まります。  
  
-   すべてのサーバー インスタンスがドメイン サービス アカウントで実行されている場合、つまり、すべてのサーバー インスタンスの **[SQL Server サービス アカウント]** 列にドメイン サービス アカウントが表示されている場合は、 **[次へ]** をクリックします。  
  
-   ドメイン サービス アカウントで実行されていないサーバー インスタンスが 1 つでもある場合、ウィザードを続行するには、サーバー インスタンスに手動で変更を加える必要があります。 この場合、 **[次へ]** をクリックすると、警告ダイアログ ボックスが表示されるので、 **[いいえ]** をクリックして、 **[エンドポイント]** タブに戻ってください。 **[レプリカの指定]** ページでウィザードを中断している間、 **[SQL Server サービス アカウント]** 列にドメイン サービス アカウント以外のアカウントが表示されている各サーバー インスタンスに対し、次のいずれかの変更を行います。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントをドメイン アカウントに変更する。 詳細については、「[SQL Server のサービス開始アカウントの変更 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/scm-services-change-the-service-startup-account.md)」を参照してください。  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] または PowerShell を使用して、証明書を使用するデータベース ミラーリング エンドポイントを手動で作成する。 詳細については、「 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md) または [AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)です。  
  
     エンドポイントを構成するときに **[可用性レプリカの指定]** ページを開いたままにしていた場合は、 **[エンドポイント]** タブに戻り、 **[更新]** をクリックして、 **[エンドポイント値]** グリッドを最新の情報に更新します。  
  
##  <a name="backup-preferences-tab"></a><a name="BackupPreferencesTab"></a> [バックアップの設定] タブ  
 どこでバックアップを実行するかを指定するには、次のオプションのいずれかを選択します。  
  
 **[セカンダリを優先]**  
 オンラインのレプリカがプライマリ レプリカのみである場合を除き、セカンダリ レプリカでバックアップを実行することを指定します。 オンラインのレプリカがプライマリ レプリカのみである場合は、プライマリ レプリカでバックアップを実行する必要があります。 既定のオプションです。  
  
 **[セカンダリのみ]**  
 バックアップをプライマリ レプリカでは実行しないことを指定します。 オンラインのレプリカがプライマリ レプリカだけの場合、バックアップは実行されません。  
  
 **プライマリ**  
 バックアップを常にプライマリ レプリカで実行することを指定します。 このオプションは、差分バックアップの作成など、バックアップがセカンダリ レプリカで実行されたときにはサポートされないバックアップ機能が必要な場合に役に立ちます。  
  
 **[任意のレプリカ]**  
 バックアップを実行するレプリカを選択するときにバックアップ ジョブが可用性レプリカのロールを無視するように指定します。 バックアップ ジョブは、動作状態および接続状態と組み合わせて、各可用性レプリカのバックアップ優先順位などの他の要素を評価する場合があります。  
  
> [!IMPORTANT]  
>  バックアップに関するユーザー設定は適用されません。 この優先設定の解釈は、特定の可用性グループのデータベースに対するバックアップ ジョブのスクリプトでのロジックに依存します (ある場合)。 詳細については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
### <a name="replica-backup-priorities-grid"></a>[レプリカのバックアップの優先順位] グリッド  
 **[レプリカのバックアップの優先順位]** グリッドを使用して、可用性グループのレプリカごとに、バックアップの優先順位を指定します。 このグリッドに含まれる列は、次のとおりです。  
  
 **サーバー インスタンス**  
 可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前を表示します。  
  
 **[バックアップ優先度 (最小 = 1、最高 = 100)]**  
 同じ可用性グループ内の他のレプリカと比較して、このレプリカでバックアップを実行する優先順位を割り当てます。 既定値は 50 です。 0 ～ 100 の範囲で、他の任意の整数を選択できます。 1 は最も低い優先順位を示し、100 は最も高い優先順位を示します。 たとえば、 **[バックアップの優先順位]** に 1 を設定した場合、現在使用可能な可用性レプリカにそれより高い優先順位のものがない場合のみ、その可用性レプリカがバックアップの実行に対して選択されます。  
  
 **[レプリカの除外]**  
 バックアップの実行に対してこの可用性レプリカが選択されないようにするには これは、たとえば、バックアップをフェールオーバーすることがないリモート可用性レプリカのような場合に便利です。  
  
##  <a name="listener-tab"></a><a name="Listener"></a> [リスナー] タブ  
 クライアント接続ポイントを提供する[可用性グループ リスナー](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)の設定を指定します。次のいずれかです。  
  
 **[今は可用性グループ リスナーを作成しない]**  
 この手順をスキップします。 リスナーは、後で作成できます。 詳細については、「 [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)が存在する必要があります。  
  
 **[可用性グループ リスナーの作成]**  
 次のように、この可用性グループに対するリスナー優先順位を指定します。  
  
 **[リスナーの DNS 名]**  
 リスナーのネットワーク名を指定します。 この名前は、ドメインで一意である必要があり、英数字、ダッシュ ( **-** )、およびハイフン ( **_** ) のみを任意の順序で含めることができます。 **[リスナー]** タブを使用して指定した場合は、DNS 名の長さは 15 文字までになります。  
  
> [!IMPORTANT]  
>  **[リスナー]** タブで無効な DNS リスナー名 (またはポート番号) を入力した場合は、 **[レプリカの指定]** ページの **[次へ]** ボタンが無効になります。  
  
 **[ポート]**  
 このリスナーで使用される TCP ポートを指定します。  
  
> [!NOTE]  
>  **[リスナー]** タブで無効なポート番号 (または DNS リスナー名) を入力した場合は、 **[レプリカの指定]** ページの **[次へ]** ボタンが無効になります。  
  
 **[ネットワーク モード]**  
 ドロップダウン リストを使用して、このリスナーによって使用されるネットワーク モードを選択します。次のいずれかです。  
  
 **[静的 IP]**  
 複数のサブネット上でリッスンするリスナーを選択する場合は指定します。 静的 IP ネットワーク モードを使用するには、可用性グループ リスナーが、可用性グループの可用性レプリカをホストするすべてのサブネットでリッスンする必要があります。 各サブネットに対して、 **[追加]** をクリックし、サブネット アドレスを選択して、IP アドレスを指定します。  
  
 **[静的 IP]** がネットワーク モードとして選択されている場合は (これは既定の選択)、グリッドに **[サブネット]** 列および **[IP アドレス]** 列が表示され、関連する **[追加]** ボタンおよび **[削除]** ボタンが表示されます。 最初のサブネットを追加するまで、グリッドは空になります。  
  
 **[サブネット]** 列  
 リスナーに対して追加された各サブネットに対して選択したサブネット アドレスが表示されます。  
  
 **[IP アドレス]** 列  
 特定のサブネットに指定した IPv4 または IPv6 のアドレスが表示されます。  
  
 **追加**  
 このリスナーにサブネットを追加する場合にクリックします。 クリックすると、 **[IP アドレスの追加]** ダイアログ ボックスが開きます。 詳細については、「[[IP アドレスの追加] ダイアログ ボックス &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/add-ip-address-dialog-box-sql-server-management-studio.md)」ヘルプ トピックを参照してください。  
  
 **Remove**  
 グリッド内で現在選択されているサブネットを削除する場合にクリックします。  
  
 **[DHCP]**  
 リスナーで単一のサブネットをリッスンし、動的ホスト構成プロトコル (DHCP) を実行しているサーバーによって割り当てられる動的 IPv4 アドレスを使用する場合に選択します。 DHCP は、可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスに共通の単一サブネットに限定されます。 DHCP は、クラスター タイプ external または none では使用できません。  
  
> [!IMPORTANT]  
>  運用環境での DHCP の使用はお勧めしません。 ダウンタイムが発生して DHCP IP のリース期限が切れると、リスナーの DNS 名に関連付けられている新しい DHCP のネットワーク IP アドレスの登録に余分な時間がかかり、クライアント接続に影響が及びます。 ただし、開発環境とテスト環境を設定して可用性グループの基本機能を確認する場合や、アプリケーションとの統合の場合には DHCP が適しています。  
  
 **[DHCP]** が選択されている場合は、 **[サブネット]** フィールドが表示されます。  
  
 **サブネット**  
 ネットワーク モードとして **[DHCP]** を選択している場合は、 **[サブネット]** ボックスの一覧を使用して、可用性グループの可用性レプリカがホストされているサブネットのアドレスを選択します。  
  
> [!IMPORTANT]
>  可用性グループ リスナーを定義した後は、次のことを行うことを強くお勧めします。  
> 
>  -   リスナーの IP アドレスが排他的に使用されるように確保することを、ネットワーク管理者に依頼します。 この可用性グループへのクライアント接続を要求するときの接続文字列で使用できるよう、リスナーの DNS ホスト名をアプリケーション開発者に通知します。  
> -   この可用性グループへのクライアント接続を要求するときの接続文字列で使用できるよう、リスナーの DNS ホスト名をアプリケーション開発者に通知します。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
-   [AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
