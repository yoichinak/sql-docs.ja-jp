---
title: レポートとサブスクリプションの処理を無効化または一時停止する | Microsoft Docs
description: サブスクリプションの管理、共有スケジュールの一時停止、共有データ ソースの無効化、レポートへのアクセスのブロック、サブスクリプションのアクセス許可の管理、配信拡張機能の削除を行います。
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ea16180c9a4e67f40302de7d70ae357b8393010
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986628"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>レポートとサブスクリプションの処理を無効化または一時停止する  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のレポートやサブスクリプションの処理を無効化または一時停止するには、複数の方法があります。 この記事では、サブスクリプションの無効化からデータ ソース接続の中断までの方法を扱います。 すべての方法をどちらの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバー モードでも使用できるわけではありません。 次の表では、方法とサポートされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバー モードについて概要を示します。  
  
##  <a name="in-this-article"></a><a name="bkmk_top"></a> この記事の内容  
  
|アプローチ|サポートされるサーバー モード|  
|-|---------------------------|  
|[サブスクリプションを有効または無効にする](#bkmk_disable_subscription)|ネイティブ モード|  
|[共有スケジュールを一時停止する](#bkmk_pause_schedule)|ネイティブ モードと SharePoint モード|  
|[共有データ ソースを無効にする](#bkmk_disable_shared_datasource)|ネイティブ モードと SharePoint モード|  
|[レポートへのアクセスを禁止するためのロールの割り当てを変更する (ネイティブ モード)](#bkmk_modify_role_assignment)|ネイティブ モード|  
|[ロールからサブスクリプション管理アクセス許可を削除する (ネイティブ モード)](#bkmk_remove_manage_subscriptions_permission)|ネイティブ モード|  
|[配信拡張機能を無効にする](#bkmk_disable_extensions)|ネイティブ モードと SharePoint モード|  
  
##  <a name="enable-and-disable-subscriptions"></a><a name="bkmk_disable_subscription"></a>サブスクリプションを有効または無効にする  
  
>[!TIP]  
>SQL 2016 Reporting Services の新機能では、"*サブスクリプションを有効または無効*" にします。 新しいユーザー インターフェイス オプションを使用して、サブスクリプションを簡単に有効または無効にできます。 サブスクリプションを無効にしても、スケジュールなどの他の構成プロパティは維持され、簡単に再び有効にすることができます。 また、プログラムを使用してサブスクリプションを有効または無効にしたり、無効にされたサブスクリプションを監査したりすることもできます。  
  
  ![[サブスクリプション] ページの [有効] ボタンと [無効] ボタン ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
Web ポータルで、 **[個人用サブスクリプション]** ページまたは個別のサブスクリプションの **[サブスクリプション]** ページからサブスクリプションに移動します。 1 つまたは複数のサブスクリプションを選択した後、リボン上の無効ボタンまたは有効ボタンをクリックします (上の図を参照)。 [状態] 列が、それぞれ "無効" または "有効" に変更されます。  
  
 サブスクリプションが有効または無効になると、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ログに行を書き込みます。 次はレポート サーバーのログ ファイルの例です。  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 このファイルに次のような行が書き込まれます。  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![PowerShell 関連コンテンツ](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ"):**Windows PowerShell を使用して、単一のサブスクリプションを無効にする:** 次の PowerShell スクリプトを使用して、特定のサブスクリプションを無効にします。 スクリプト内のサーバー名とサブスクリプション ID は更新してください。  
  
```PS  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 次のスクリプトを使用すると、すべてのサブスクリプションとその ID を一覧表示できます。 サーバー名を更新します。  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell 関連コンテンツ](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ") **Windows PowerShell を使用して、無効になっているすべてのサブスクリプションを一覧表示する:** 次の PowerShell スクリプトを使用して、現在のネイティブ モード レポート サーバーで無効になっているすべてのサブスクリプションを一覧表示します。 サーバー名を更新します。  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell 関連コンテンツ](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ") **Windows PowerShell を使用して、無効になっているすべてのサブスクリプションを有効にする:** 次の PowerShell スクリプトを使用して、現在無効になっているすべてのサブスクリプションを有効にします。 サーバー名を更新します。  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell 関連コンテンツ](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ") **Windows PowerShell を使用して、すべてのサブスクリプションを無効にする:** 次の PowerShell スクリプトを使用して、**すべて**のサブスクリプションを無効にします。  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="pause-a-shared-schedule"></a><a name="bkmk_pause_schedule"></a> 共有スケジュールを一時停止する  
 レポートまたはサブスクリプションが共有スケジュールから実行される場合、スケジュールを一時停止して処理を中止できます。 一時停止したスケジュールで実行されるすべてのレポートおよびサブスクリプションの処理は、スケジュールが再開されるまで延期されます。  
  
-   **SharePoint モード:** ![SharePoint 設定](/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint の設定") **[サイトの設定]** で、 **[共有スケジュールの管理]** を選択します。 スケジュールを選択し、 **[選択したスケジュールの一時停止]** をクリックします。  
  
-   **ネイティブ モード:** Web ポータルで、Web ポータル画面の上部にあるメニュー バーの **[設定]** ボタン ![[設定] ボタン](media/ssrs-portal-settings-gear.png) を選択し、ドロップダウン メニューから **[サイトの設定]** を選択します。 **[スケジュール]** タブを選択して、[スケジュール] ページを表示します。 有効または無効にするスケジュールの横にあるチェックボックスをオンにしてから、 **[有効]** または **[無効]** ボタンを選択して、目的の操作を実行します。 それに応じて、[状態] 列が "無効" または "有効" に更新されます。  
  
##  <a name="disable-a-shared-data-source"></a><a name="bkmk_disable_shared_datasource"></a> 共有データ ソースを無効にする  
 共有データ ソースを使用する利点の 1 つは、共有データ ソースを無効にして、レポートまたはデータ ドリブン サブスクリプションの実行を中止できることです。 共有データ ソースを無効にすると、レポートは外部ソースから切断されます。 共有データ ソースが無効な間は、すべてのレポートと共有データ ソースを使用するサブスクリプションで共有データ ソースを使用できません。  
  
 データ ソースが使用できない場合でも、レポートは読み込まれることに注意してください。 レポートにはデータは含まれていませんが、適切な権限を持ったユーザーは、レポートに関連付けられたプロパティ ページ、セキュリティ設定、レポート履歴、およびサブスクリプション情報にアクセスできます。  
  
-   **SharePoint モード:** SharePoint モードのレポート サーバーで共有データ ソースを無効にするには、データ ソースを含むドキュメント ライブラリに移動します。 ![共有データ ソースのアイコン](../../reporting-services/report-data/media/hlp-16datasource.png "共有データ ソースのアイコン") データ ソースをクリックして、 **[このデータ ソースを有効にする]** チェック ボックスをオフにします。  
  
-   **ネイティブ モード:** ネイティブ モードのレポート サーバーで共有データ ソースを無効にするには、Web ポータルでデータ ソースを開き、 **[このデータ ソースを有効にする]** チェック ボックスをオフにします。  
  
##  <a name="modify-role-assignments-to-prevent-access-to-a-report-native-mode"></a><a name="bkmk_modify_role_assignment"></a> ロールの割り当てを変更してレポートへのアクセスを禁止する (ネイティブ モード)  
レポートを使用できないようにする方法の 1 つは、レポートにアクセスするためのロールの割り当てを一時的に削除することです。 この方法は、データ ソースへの接続方法に関係なくすべてのレポートに使用できます。 この方法は、ロールの割り当てを一時的に削除したレポートのみに有効で、他のレポートやアイテムの操作には影響しません。  
  
 ロールの割り当てを削除するには、Web ポータルでレポートの **[セキュリティ]** ページを開きます。 そのレポートが親レポートからセキュリティを継承している場合は、 **[セキュリティをカスタマイズする]** を選択した後、 **[アイテム セキュリティ]** ダイアログ ボックスの **[確認]** を選択して、広範囲なアクセスを提供するロールの割り当てを省略する、制限付きのセキュリティ ポリシーを作成できます (たとえば、Everyone にアクセスを提供するロールの割り当てを削除し、Administrators などの小規模なユーザー グループにアクセスを提供するロールの割り当てを保持できます)。  
  
##  <a name="remove-manage-subscription-permissions-from-role-native-mode"></a><a name="bkmk_remove_manage_subscriptions_permission"></a> ロールからサブスクリプション管理アクセス許可を削除する (ネイティブ モード)  
 ユーザーがサブスクリプションを作成できないようにするには、ロールから **[個別のサブスクリプションを管理]** タスクをオフにします。 このタスクを削除すると、[サブスクリプション] ページは使用できなくなります。 Web ポータルの [個人用サブスクリプション] ページには、既にサブスクリプションが含まれていても、何も表示されません (これは削除できません)。 サブスクリプション関連タスクを削除すると、ユーザーはサブスクリプションを作成および変更できなくなりますが、既存のサブスクリプションは削除されません。 既存のサブスクリプションは、削除しない限り引き続き実行されます。 アクセス許可を削除するには:  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。 
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーに接続します。  
  
3.  **[セキュリティ]** ノードを展開します。  
  
4.  **[ロール]** ノードを展開し、目的のロールを選択します。  
  
5.  ロールを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[個々のサブスクリプションを管理]** タスクと **[すべてのサブスクリプションを管理]** タスクをオフにします。  
  
7.  **[OK]** を選択して、変更内容を適用します。

  
##  <a name="disable-delivery-extensions"></a><a name="bkmk_disable_extensions"></a> 配信拡張機能を無効にする  
 レポート サーバーにインストールされたすべての配信拡張機能は、特定のレポートのサブスクリプションを作成する権限を持つユーザーが使用できます。 使用できる配信拡張機能は次のとおりです。自動的に構成されます。  
  
-   Windows ファイル共有  
  
-   SharePoint ライブラリ (SharePoint 統合モードのレポート サーバーと統合された SharePoint サイトからのみ利用可能)  
  
 電子メール配信は使用前に構成する必要があります。 構成が済んでいない場合、使用できません。 詳細については、「[電子メールの設定 - Reporting Services のネイティブ モード (構成マネージャー)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」を参照してください。  
  
 特定の拡張機能を無効にするには、 **RSReportServer.config** ファイルから拡張機能のエントリを削除します。 詳細については、「[Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)」と「[電子メールの設定 - Reporting Services のネイティブ モード (構成マネージャー)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」を参照してください。  
  
 配信拡張機能を削除すると、これは Web ポータルまたは SharePoint サイトで使用できなくなります。 配信拡張機能を削除すると、サブスクリプションが無効になることがあります。 配信拡張機能を削除する前に、このようなサブスクリプションを削除するか、または別の配信拡張機能を使用するように構成する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [サブスクリプションと配信 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Web ポータルの構成](../../reporting-services/report-server/configure-web-portal.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [セキュリティ保護可能なアイテム](../../reporting-services/security/securable-items.md) 
