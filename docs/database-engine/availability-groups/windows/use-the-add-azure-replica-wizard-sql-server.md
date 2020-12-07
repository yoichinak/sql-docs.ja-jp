---
title: 可用性グループでセカンダリ レプリカとして Azure VM を構成する
description: Azure のレプリカ追加ウィザードを使用して、ハイブリッド IT 環境に Azure VM を作成し、新規または既存の Always On 可用性グループのセカンダリ レプリカとしてこれを構成します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: cawrites
ms.author: chadam
ms.openlocfilehash: 9ff107b2f3e132015e294ef7ba8174ade5a0c575
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583693"
---
# <a name="configure-azure-vm-as-a-secondary-replica-in-an-availability-group"></a>可用性グループでセカンダリ レプリカとして Azure VM を構成する
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Azure のレプリカ追加ウィザードを使用して、ハイブリッド IT 環境に新しい Azure VM を作成し、新規または既存の Always On 可用性グループのセカンダリ レプリカとしてこれを構成することができます。  

>  [!IMPORTANT]  
>  Azure には、リソースの作成と操作に関して 2 種類のデプロイメント モデルがあります。リソース マネージャー デプロイメント モデルとクラシック デプロイメント モデルです。 この記事では、クラシック デプロイ モデルの使用方法について説明します。 最新のデプロイメントでは、リソース マネージャー モデルを使用することをお勧めします。 この記事の手順は、Resource Manager モデルを使用して Azure 仮想マシンをデプロイしている場合には適用されません。   

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
 これまでに可用性グループに可用性レプリカを追加したことがない場合は、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」の、「サーバー インスタンス」と「可用性グループとレプリカ」のセクションを参照してください。  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   現在のプライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   オンプレミスのサブネットに Azure とのサイト間 VPN があるハイブリッド IT 環境が必要です。 詳細については、「 [管理ポータルでのサイト間 VPN の構成](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal)」を参照してください。  
  
-   可用性グループに、内部設置型可用性レプリカが含まれている必要があります。  
  
-   可用性グループ リスナーに対するクライアントで、可用性グループが Azure レプリカにフェールオーバーした場合にリスナーとの接続を維持するには、インターネット接続が必要です。  
  
-   **初期データの完全同期を使用するための前提条件** ウィザードでのバックアップの作成およびバックアップへのアクセスには、ネットワーク共有を指定する必要があります。 プライマリ レプリカでは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の起動に使用するアカウントにネットワーク共有での読み取り/書き込みファイルシステム権限が必要です。 セカンダリ レプリカでは、アカウントは、ネットワーク共有に対する読み取り権限を持つ必要があります。  
  
     ウィザードを使用して初期データの完全同期を実行できない場合は、セカンダリ データベースを手動で準備する必要があります。 これは、ウィザードの実行前でも実行後でもかまいません。 詳細については、「 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
 また、可用性グループへのレプリカ追加ウィザードでデータベース ミラーリング エンドポイントを管理できるようにする場合は、CONTROL ON ENDPOINT 権限も必要です。  
  
##  <a name="using-the-add-azure-replica-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Azure のレプリカ追加ウィザードの使用 (SQL Server Management Studio)  

>  [!IMPORTANT]  
>  Azure レプリカの追加ウィザードでサポートされるのは、クラシック デプロイ モデルで作成された仮想マシンのみです。 新しい仮想マシンのデプロイでは、新しい Resource Manager モデルを使用する必要があります。 Resource Manager で仮想マシンを使用する場合は、Transact-SQL コマンド (ここには示されていません) を使用して、セカンダリ Azure レプリカを手動で追加する必要があります。 このウィザードは、Resource Manager のシナリオでは機能しません。 
>
>  Azure レプリカの追加ウィザードは、SQL Server Management Studio の最新リリース (バージョン 18.x および 17.x) では使用できません。
        
 Azure のレプリカ追加ウィザードは、 [[レプリカの指定] ページ](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)から起動できます。 このページを開くには、次の 2 つの方法があります。  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Azure のレプリカ追加ウィザードを起動したら、次の手順を行います。  
  
1.  まず、Azure サブスクリプションの管理証明書をダウンロードします。 **[ダウンロード]** をクリックして、サインイン ページを開きます。  
  
2.  Microsoft アカウントまたは組織アカウントを使用して Microsoft Azure にサインインします。 Microsoft アカウントまたは組織アカウントは、HYPERLINK "mailto:patc@contoso.com" patc@contoso.com などの電子メール アドレスの形式になっています。 Azure の資格情報の詳細については、「 [Microsoft Account for Organizations FAQ (組織向け Microsoft アカウントに関する FAQ)](/previous-versions/jj592903(v=msdn.10)) 」および [Troubleshooting sign-in problems with your organizational account (組織アカウントのサインインに関する問題のトラブルシューティング)](https://support.microsoft.com/kb/2756852)に関するページを参照してください。  
  
3.  次に、 **[接続]** をクリックしてサブスクリプションに接続します。 接続すると、 **[仮想ネットワーク]** や **[仮想ネットワーク サブネット]** などの Azure のパラメーターがドロップダウン リストに設定されます。  
  
4.  新しいセカンダリ レプリカをホストする Azure VM の設定を指定します。  
  
     Image  
     Azure VM に使用する SQL Server イメージの名前  
  
     [VM サイズ]  
     Azure VM のサイズ  
  
     VM 名  
     Azure VM の DNS 名  
  
     [VM ユーザー名]  
     Azure VM の既定の管理者のユーザー名  
  
     [VM 管理者パスワード] (および [パスワードの確認入力])  
     Azure VM の既定の管理者のパスワード  
  
     Virtual Network  
     Azure VM を配置する仮想ネットワーク  
  
     [仮想ネットワーク サブネット]  
     Azure VM を配置する仮想ネットワーク サブネット  
  
     Domain  
     Azure VM を参加させる Active Directory (AD) ドメイン  
  
     ドメイン ユーザー名  
     Azure VM をドメインに参加させるために使用される AD ユーザー名  
  
     Password  
     Azure VM をドメインに参加させるために使用されるパスワード  
  
5.  **[OK]** をクリックして設定をコミットし、Azure のレプリカ追加ウィザードを終了します。  
  
6.  新しいレプリカの場合と同じように、 [[レプリカの指定] ページ](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) で残りの構成手順を行います。  
  
     可用性グループ ウィザードまたは可用性グループへのレプリカ追加ウィザードを完了すると、構成プロセスにより、Azure での操作 (新しい VM の作成、AD ドメインへの参加、Windows クラスターへの追加、Always On 高可用性の有効化、可用性グループへの新しいレプリカの追加) がすべて行われます。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
