---
title: レポート サーバー アクセスに対するファイアウォールの構成 | Microsoft Docs
description: URL 経由でアクセスされるレポート サーバー アプリケーションとパブリッシュされたレポートへのアクセスを許可するよう、Windows ファイアウォールを構成する方法について説明します。
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [Reporting Services]
- configuring servers [Reporting Services]
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 89ad4ef0d7537f1b5e8cad9349eb7aeacf0872c6
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934607"
---
# <a name="configure-a-firewall-for-report-server-access"></a>レポート サーバー アクセスに対するファイアウォールの構成
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバー アプリケーションとパブリッシュされたレポートには、IP アドレス、ポート、および仮想ディレクトリを指定した URL を通じてアクセスします。 Windows ファイアウォールが有効になっている場合、レポート サーバーで使用するように構成されているポートは閉じられる可能性が高くなります。 ポートが閉じていると、リモートのクライアント コンピューターから Web ポータルを開こうとしたときに空白のページが表示されたり、レポートの要求後に空白の Web ページが表示されたりします。  
  
 ポートを開くには、レポート サーバー コンピューターで Windows ファイアウォール ユーティリティを使用する必要があります。 ポートは Reporting Services によって自動的に開かれないので、この手順を手動で実行する必要があります。  
  
 既定では、レポート サーバーはポート 80 で HTTP 要求をリッスンします。 このため、以下に示す手順ではそのポートを指定しています。 別のポートを使用するようにレポート サーバーの URL を構成している場合は、以下に示す手順を実行するときにそのポート番号を指定する必要があります。  
  
 外部コンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベースにアクセスする場合、またはレポート サーバー データベースが外部の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに置かれている場合は、外部コンピューターのポート 1433 および 1434 を開く必要があります。 詳しくは、「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)」をご覧ください。 Windows ファイアウォールの既定の設定に関する詳細と、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
## <a name="prerequisites"></a>前提条件  
 次の手順では、既にサービス アカウントを構成し、レポート サーバー データベースを作成し、レポート サーバー Web サービスと Web ポータルの URL を構成していることを前提としています。 詳細については、「 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)」を参照してください。  
  
 また、ローカル レポート サーバー インスタンスへのローカル Web ブラウザー接続を通じてレポート サーバーにアクセスできることを確認しておく必要があります。 この手順によって、作業環境が整っているかどうかを検証できます。 ポートを開く前に、環境が正しく構成されているかどうかを確認する必要があります。 Windows Server でこの手順を完了するには、レポート サーバー サイトを [信頼済みサイト] に追加しておくことも必要です。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。  
  
## <a name="opening-ports-in-windows-firewall"></a>Windows ファイアウォールでポートを開く  
  
#### <a name="to-open-port-80"></a>ポート 80 を開くには  
  
1.  **[スタート]** メニューの **[コントロール パネル]** をクリックし、 **[システムとセキュリティ]** 、 **[Windows ファイアウォール]** の順にクリックします。 コントロール パネルの表示方法が [カテゴリ] 以外の場合は、単に **[Windows ファイアウォール]** を選択するだけでかまいません。  
  
2.  **[詳細設定]** をクリックします。  
  
3.  **[受信の規則]** をクリックします。  
  
4.  **[操作]** ウィンドウで **[新しい規則]** をクリックします。  
  
5.  **[ポート]** の **[規則の種類]** をクリックします。  
  
6.  **[次へ]** をクリックします。  
  
7.  **[プロトコルおよびポート]** ページで、 **[TCP]** をクリックします。  
  
8.  **[特定のローカル ポート]** を選択し、「 **80**」という値を入力します。  
  
9. **[次へ]** をクリックします。  
  
10. **[操作]** ページで、 **[接続を許可する]** をクリックします。  
  
11. **[次へ]** をクリックします。  
  
12. **[プロファイル]** ページで、実際の環境に合った適切なオプションをクリックします。  
  
13. **[次へ]** をクリックします。  
  
14. **[名前]** ページで、「**ReportServer (TCP on port 80)** 」という名前を入力します。  
  
15. **[完了]** をクリックします。  
  
16. コンピューターを再起動します。  
  
## <a name="next-steps"></a>次のステップ  
 ポートを開いた後、リモート ユーザーがそのポートでレポート サーバーにアクセスできるかどうかを確認する前に、ホームに対するロールとサイト レベルのロールの割り当てを行って、レポート サーバーへのアクセスをユーザーに許可する必要があります。 ユーザーに十分な権限がない場合は、ポートを正しく開くことができてもレポート サーバーへの接続に失敗します。 詳細については、「[レポート サーバーへのユーザー アクセスを許可する](../../reporting-services/security/grant-user-access-to-a-report-server.md)」を参照してください。  
  
 別のコンピューター上で Web ポータルを起動することによって、ポートが正しく開かれているかどうかを確認することもできます。 詳細については、[レポート サーバーの Web ポータル](../../reporting-services/web-portal-ssrs-native-mode.md)に関するページをご覧ください。
  
## <a name="see-also"></a>関連項目  
 [レポート サーバー サービス アカウントの構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー URL の構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [レポート サーバー データベースの作成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [レポート サーバー サービス アカウントの構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
