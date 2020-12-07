---
description: ファイルのみのインストール (Reporting Services)
title: ファイルのみのインストール (Reporting Services) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5480e7b56f1ebaae56d30be0b0027a989d6ff816
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933496"
---
# <a name="files-only-installation-reporting-services"></a>ファイルのみのインストール (Reporting Services)
  *ファイルのみのインストール* とは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストール形態の 1 つです。このインストールでは、セットアップで、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] プログラム ファイルのフォルダー構造の作成、ディスクへのファイルのコピー、ローカル コンピューターへのレポート サーバー サービスの登録、サービス アカウントの構成、サービス アカウントへのファイル権限の付与、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI プロバイダーの登録を行います。  
  
 ファイルのみのインストールに含まれる [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能は、レポート サーバー サービス (レポート サーバー Web サービスおよびバックグラウンド処理アプリケーションをホストします)、レポート ビルダー、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツール、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コマンド ライン ユーティリティ (rsconfig.exe、rskeymgmt.exe、および rs.exe) です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] や [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] などの共有機能は含まれません。これらの機能をインストールする場合は、別のアイテムとして指定する必要があります。  
  
 他のインストール モードとは異なり、ファイルのみのモードでインストールされたレポート サーバーは、セットアップの終了時点ではまだ使用できません。 [レポート サーバー構成マネージャー (ネイティブ モード)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md) を使用してレポート サーバーをオンラインにするには、追加の構成が必要です。  
  
## <a name="when-to-select-files-only-installation-mode"></a>ファイルのみのインストール モードを選択する場合  
 次のような場合、ファイルのみのインストールを実行する必要があります。  
  
-   リモートのレポート サーバー データベースにレポート サーバーを接続する場合。  
  
-   レポート サーバーを名前付きインスタンスとしてインストールする場合。  
  
-   カスタムの設定や機能の使用が配置要件に含まれており、サーバー構成のタイミングと方法を完全に制御する必要がある場合。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を含む [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]フェールオーバー クラスターをインストールする場合。  
  
## <a name="how-to-perform-a-files-only-installation"></a>ファイルのみのインストールを実行する方法  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、ファイルのみのインストールが既定値です。  
  
 ファイルのみのインストールを、コマンド ラインまたはインストール ウィザードで指定できます。 手順については次のトピックを参照してください。  
  
-   [SQL Server をインストール ウィザードからインストールする &#40;セットアップ&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
#### <a name="example-command-line-script"></a>コマンド ライン スクリプトの例  
 わかりやすくするため、この例では /RSINSTALLMODE ="FilesOnlyMode" を指定しています。 実際には、ファイルのみのモードが既定値であるため、これを省略してもファイルのみのモードでインストールされます。  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>インストール ウィザード  
 [機能の選択] ページで [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] を選択すると、[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成] ページでインストール モードを指定できるようになります。 ファイルのみのインストールを指定するには、 **[構成] ページで** [レポート サーバーを構成せずにインストールする] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をクリックします。  
  
## <a name="see-also"></a>参照  
 [Reporting Services のインストール状態の検証](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [レポート サーバー サービス アカウントの構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー URL の構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [レポート サーバー データベース接続の構成 (レポート サーバー構成マネージャー)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 [Reporting Services SharePoint モードのインストール](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   

::: moniker-end

 [Reporting Services ネイティブ モードのレポート サーバーのインストール](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)  
  
  

