---
title: 可用性グループ機能を有効または無効にする
description: Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio を使用して Always On 可用性グループを有効または無効にする手順。
ms.custom: seodec18
ms.date: 08/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 33172488fd20ed4ef2fc555026931ae8b9a10f9c
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584322"
---
# <a name="enable-or-disable-always-on-availability-group-feature"></a>Always On 可用性グループ機能を有効または無効にする
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  サーバー インスタンスで可用性グループを使用するには、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を有効にする必要があります。 可用性グループを作成したり構成したりするためには、少なくとも 1 つの可用性グループの可用性レプリカがホストされる [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の各インスタンスで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能が有効になっている必要があります。  
  
> [!IMPORTANT]  
>  WSFC クラスターを削除してから再作成した場合は、元の WSFC クラスター上の可用性レプリカをホストしていた [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の各インスタンスについて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能を無効にしてから再度有効にする必要があります。  
  
  
##  <a name="prerequisites-for-enabling-always-on-availability-groups"></a><a name="Prerequisites"></a> AlwaysOn 可用性グループを有効にするための前提条件  
  
-   このサーバー インスタンスは、Windows Server フェールオーバー クラスタリング (WSFC) ノードに存在している必要があります。  
  
-   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]をサポートする SQL Server エディションが実行されている必要があります。 詳細については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
-   一度に 1 つのサーバー インスタンスでのみ AlwaysOn 可用性グループを有効にします。 AlwaysOn 可用性グループを有効にした後は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが再起動するまで待ってから、次のサーバー インスタンスを有効にしてください。  
  
 可用性グループの作成と構成に関するその他の前提条件については、「[AlwaysOn 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
## <a name="permissions"></a><a name="Permissions"></a> Permissions  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス上で AlwaysOn 可用性グループが有効になっている限り、そのサーバー インスタンスには、WSFC クラスターに対するフル コントロール権限があります。  

 ローカル コンピューターの **Administrator** グループのメンバーシップおよび WSFC クラスターに対するフル コントロール権限が必要です。 PowerShell を使用して AlwaysOn を有効にする場合は、 **[管理者として実行]** オプションを使用してコマンド プロンプト ウィンドウを開いてください。  
  
 Active Directory の Create Objects 権限と Manage Objects 権限が必要です。  
  
##  <a name="determine-whether-always-on-availability-groups-is-enabled"></a><a name="IsEnabled"></a> AlwaysOn 可用性グループが有効になっているかどうかを確認する  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMS1Procedure"></a> SQL Server Management Studio の使用  
 **AlwaysOn 可用性グループが有効になっているかどうかを調べるには**  
  
1.  オブジェクト エクスプローラーでサーバー インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[サーバーのプロパティ]** ダイアログ ボックスの **[全般]** ページをクリックします。 **[HADR が有効]** プロパティに、次のいずれかの値が表示されます。  
  
    -   **True**(AlwaysOn 可用性グループが有効である場合)  
  
    -   **False**(AlwaysOn 可用性グループが無効である場合)  
  
###  <a name="using-transact-sql"></a><a name="Tsql1Procedure"></a> Transact-SQL の使用  
 **AlwaysOn 可用性グループが有効になっているかどうかを調べるには**  
  
1.  次の [SERVERPROPERTY](../../../t-sql/functions/serverproperty-transact-sql.md) ステートメントを使用します。  
  
    ```  
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     **IsHadrEnabled** サーバー プロパティの設定は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに対して AlwaysOn 可用性グループが有効であるかどうかを示します。  
  
    -   **IsHadrEnabled** = 1 の場合: AlwaysOn 可用性グループが有効  
  
    -   **IsHadrEnabled** = 0 の場合: AlwaysOn 可用性グループが無効  
  
    > [!NOTE]  
    >  **IsHadrEnabled** サーバー プロパティの詳細については、「[SERVERPROPERTY &#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)」を参照してください。  
  
###  <a name="using-powershell"></a><a name="PowerShell1Procedure"></a> PowerShell の使用  
 **AlwaysOn 可用性グループが有効になっているかどうかを調べるには**  
  
1.  **が有効であるかどうかを確認するサーバー インスタンスを既定の操作対象に設定 (** cd [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ) します。  
  
2.  PowerShell コマンド **Get-Item** を入力します。  
  
    ```  
    PS SQLSERVER:\SQL\NODE1\DEFAULT> get-item . | select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="enable-always-on-availability-groups"></a><a name="EnableAOAG"></a> AlwaysOn 可用性グループを有効にする  
 **AlwaysOn を有効にする場合に使用するツール:**  
  
-   [SQL Server 構成マネージャー](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="using-sql-server-configuration-manager"></a><a name="SQLCM2Procedure"></a> SQL Server 構成マネージャーの使用  
 **Always On 可用性グループを有効にするには**  
  
1.  対象の (AlwaysOn 可用性グループを有効にする) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスがホストされている Windows Server フェールオーバー クラスター (WSFC) ノードに接続します。  
  
2.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
3.  **SQL Server 構成マネージャー** で、 **[SQL Server のサービス]** をクリックし、[SQL Server ( **\<**_instance name_**>)** ] を右クリックして、 **[プロパティ]** をクリックします。 **\<**_instance name_**>** は、Always On 可用性グループを有効にするローカル サーバー インスタンスの名前です。  
  
4.  **[AlwaysOn 高可用性]** タブを選択します。  
  
5.  **[Windows フェールオーバー クラスター名]** フィールドに、ローカル フェールオーバー クラスターの名前が表示されていることを確認します。 このフィールドが空白の場合、このサーバー インスタンスは現在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]をサポートしていません。 ローカル コンピューターがクラスター ノードではないか、WSFC クラスターがシャットダウンされています。または、このエディションの [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] では [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]がサポートされません。  
  
6.  **[AlwaysOn 可用性グループを有効にする]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーによって変更内容が保存されます。 その後、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを手動で再起動する必要があります。 業務上の要件に合った時間帯を選んで再起動することができます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが再起動されると、AlwaysOn が有効になり、 **IsHadrEnabled** サーバー プロパティが 1 に設定されます。  
  
###  <a name="using-sql-server-powershell"></a><a name="PScmd2Procedure"></a> SQL Server PowerShell の使用  
 **AlwaysOn を有効にするには**  
  
1.  ディレクトリ変更コマンド (**cd**) を使用して、AlwaysOn 可用性グループを有効にするサーバー インスタンスに移動します。  
  
2.  AlwaysOn 可用性グループを有効にするには、**Enable-SqlAlwaysOn** コマンドレットを使用します。  
  
     コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
    > [!NOTE]  
    >  **Enable-SqlAlwaysOn** コマンドレットを実行したときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを再起動するかどうかを制御する方法については、このトピックの「[SQL Server サービスがコマンドレットによって再起動される条件](#WhenCmdletRestartsSQL)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="example-enable-sqlalwayson"></a><a name="ExmplEnable-SqlHadrServic"></a> 例: Enable-SqlAlwaysOn  
 次の PowerShell コマンドは、SQL Server のインスタンス ( [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Computer *Instance*\\ *) の* を有効にします。  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="disable-always-on-availability-groups"></a><a name="DisableAOAG"></a> AlwaysOn 可用性グループを無効にする  
  
-   **AlwaysOn を無効にする前に:**  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
-   **AlwaysOn を無効にする場合に使用するツール:**  
  
    -   [SQL Server 構成マネージャー](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **補足情報:** [Always On を無効にした後](#FollowUp)  
  
> [!IMPORTANT]  
>  AlwaysOn を無効にできるサーバー インスタンスは一度に 1 つだけです。 AlwaysOn 可用性グループを無効にした後は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが再起動するまで待ってから、次のサーバー インスタンスを有効にしてください。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
 サーバー インスタンスで AlwaysOn を無効にする前に、次の操作を行うことをお勧めします。  
  
1.  保持する可用性グループのプライマリ レプリカをサーバー インスタンスがホスト中の場合は、同期されたセカンダリ レプリカに可用性グループを手動でフェールオーバーすることをお勧めします (可能な場合)。 詳細については、「[可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)」を参照してください。  
  
2.  ローカル セカンダリ レプリカをすべて削除します。 詳細については、「[可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)」を参照してください。  
  
###  <a name="using-sql-server-configuration-manager"></a><a name="SQLCM3Procedure"></a> SQL Server 構成マネージャーの使用  
 **AlwaysOn を無効にするには**  
  
1.  対象の (AlwaysOn 可用性グループを無効にする) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスがホストされている Windows Server フェールオーバー クラスター (WSFC) ノードに接続します。  
  
2.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
3.  **SQL Server 構成マネージャー** で、 **[SQL Server のサービス]** をクリックし、[SQL Server ( **\<**_instance name_**>)** ] を右クリックして、 **[プロパティ]** をクリックします。 **\<**_instance name_**>** は、Always On 可用性グループを無効にするローカル サーバー インスタンスの名前です。  
  
4.  **[Always On 高可用性]** タブで、 **[Always On 可用性グループを有効にする]** チェック ボックスをオフにし、 **[OK]** をクリックします。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーによって変更内容が保存され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが再起動されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスが再起動すると、AlwaysOn が無効になり、 **IsHadrEnabled** サーバー プロパティは、AlwaysOn 可用性グループが無効であることを示す 0 に設定されます。  
  
5.  このトピックの「 [補足情報: Always On を無効にした後](#FollowUp)」を読むことをお勧めします。  
  
###  <a name="using-sql-server-powershell"></a><a name="PScmd3Procedure"></a> SQL Server PowerShell の使用  
 **AlwaysOn を無効にするには**  
  
1.  ディレクトリ変更コマンド (**cd**) を使用して、AlwaysOn 可用性グループを無効にするサーバー インスタンスに移動します。  
  
2.  AlwaysOn 可用性グループを無効にするには、**Disable-SqlAlwaysOn** コマンドレットを使用します。  
  
     たとえば、次のコマンドは、SQL Server インスタンス (*Computer*\\*Instance*) の AlwaysOn 可用性グループを無効にします。  このコマンドの場合、インスタンスを再起動する必要があり、再起動するかどうかを確認するメッセージが表示されます。  
  
    ```  
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  **Disable-SqlAlwaysOn** コマンドレットを実行したときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを再起動するかどうかを制御する方法については、このトピックの「[SQL Server サービスがコマンドレットによって再起動される条件](#WhenCmdletRestartsSQL)」を参照してください。  
  
     コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="follow-up-after-disabling-always-on"></a><a name="FollowUp"></a>補足情報: Always On を無効にした後  
 AlwaysOn 可用性グループを無効にした後、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを無効にする必要があります。 サーバー インスタンスは、SQL 構成マネージャーによって自動的に再起動されます。 ただし、**Disable-SqlAlwaysOn** コマンドレットを使用した場合は、サーバー インスタンスを手動で再起動する必要があります。 詳細については、「 [sqlservr Application](../../../tools/sqlservr-application.md)」を参照してください。  
  
 再起動後のサーバー インスタンスに該当する状況を以下に示します。  
  
-   SQL Server の起動時に可用性データベースは開始されず、アクセス不能となります。  
  
-   サポートされる AlwaysOn [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md)のみとなります。 CREATE AVAILABILITY GROUP と ALTER AVAILABILITY GROUP、および ALTER DATABASE の SET HADR オプションはサポートされません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 可用性グループを無効にしても、WSFC 内の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の構成データと  のメタデータにその影響が及ぶことはありません。  
  
 1 つまたは複数の可用性グループの可用性レプリカをホストするすべてのサーバー インスタンスで AlwaysOn 可用性グループを永続的に無効にする場合は、次の手順を完了することをお勧めします。  
  
1.  AlwaysOn を無効にする前にローカル可用性レプリカを削除しなかった場合は、サーバー インスタンスが可用性レプリカをホストしている可用性グループを削除します。 可用性グループの削除については、「[可用性グループの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)」を参照してください。  
  
2.  残されたメタデータを除去するには、元の WSFC の一部であるサーバー インスタンスから影響を受ける可用性グループをそれぞれ削除します。  
  
3.  プライマリ データベースには引き続きすべての接続からアクセスできますが、プライマリ データベースとセカンダリ データベース間のデータの同期は中止されます。  
  
4.  セカンダリ データベースは、RESTORING 状態に入ります。 これらは削除するか、RESTORE WITH RECOVERY を使用して復元できます。 ただし、復元されたデータベースは、それ以降、可用性グループのデータの同期対象とはなりません。  
  
##  <a name="when-does-a-cmdlet-restart-the-sql-server-service"></a><a name="WhenCmdletRestartsSQL"></a> SQL Server サービスがコマンドレットによって再起動される条件  
 現在実行中のサーバー インスタンスで、**Enable-SqlAlwaysOn** または **Disable-SqlAlwaysOn** を使用して現在の AlwaysOn 設定を変更すると、SQL Server サービスが再起動されます。 再起動の動作は次の条件によって異なります。  
  
|-NoServiceRestart パラメーターの指定|-Force パラメーターの指定|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスの再起動|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|いいえ|いいえ|既定では再起動されます。 ただし、次のプロンプトが表示されます。<br /><br /> **このアクションを完了するには、サーバー インスタンス '<instance_name>' の SQL Server サービスを再起動する必要があります。続行しますか?**<br /><br /> **[Y] はい  [N] いいえ  [S] 中断  [?] ヘルプ (既定値は "Y"):**<br /><br /> **N** または **S** を指定した場合、サービスは再起動されません。|  
|いいえ|はい|サービスは再起動されます。|  
|はい|いいえ|サービスは再起動されません。|  
|はい|はい|サービスは再起動されません。|  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)  
  
