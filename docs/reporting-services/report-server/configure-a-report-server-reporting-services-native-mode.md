---
title: レポート サーバーの構成 (Reporting Services ネイティブ モード) | Microsoft Docs
description: インストール中に選択したオプションによって異なる、SQL Server Report Server の追加構成について説明します。
ms.date: 06/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf028fa4de6457b5ddfe520bae1d2348c52362bf
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935016"
---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>レポート サーバーの構成 (Reporting Services ネイティブ モード)
  インストール中に選択したオプションによっては、レポート サーバーを使用する前に追加の構成が必要になる場合があります。 少なくともレポート サーバーの構成には以下が必要です。  
  
-   レポート サーバー サービス アカウント (インストール中に設定される)  
  
-   レポート サーバーへのアクセスを提供する Web サービス URL  
  
-   アプリケーション データ、レポート、およびその他のアイテムを格納するレポート サーバー データベース  
  
 ネイティブ モードの既定の構成または SharePoint 統合モードの既定の構成のいずれかのインストール オプションを選択した場合は、セットアップによって最小の設定が構成されます。 レポート サーバーをファイルのみのモードでインストールした場合 (インストール ウィザードで **[サーバーを構成せずにインストールする]** オプションを選択した場合) は、サービス アカウントのみ構成されます。 Web サービス URL とレポート サーバー データベースは、セットアップの完了後に構成する必要があります。  
  
レポート サーバーへのアクセスをユーザーに付与し、レポート サーバーのコンテンツを管理できるように Web ポータルを構成することをお勧めします。 SharePoint 統合モードでレポート サーバーを配置した場合、SharePoint サーバーの Web フロントエンドを使用してアクセス権を付与します。  
  
 レポート サーバーの電子メールや自動実行アカウントなどの追加の機能は、必要に応じて構成できます。 詳細については、「 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)」を参照してください。  
  
 レポート サーバーを構成するには、Reporting Services 構成ツールを使用します。  
  
## <a name="to-minimally-configure-a-report-server-installation"></a>レポート サーバー インストールの最小構成を行うには  
  
1.  Reporting Services 構成ツールを起動して、レポート サーバー インスタンスに接続します。 手順については、「[レポート サーバーの構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
2.  **[Web サービス URL]** をクリックして、レポート サーバーの URL を構成するページを開きます。 URL を定義する方法の手順については、「[URL の構成 &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)」を参照してください。  
  
3.  **[データベース]** をクリックして、レポート サーバー データベースを作成します。 手順については、「[ネイティブ モードのレポート サーバー データベースを作成する &#40;レポート サーバーの構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)」を参照してください。  
  
4.  **[Web サービス URL]** ページに戻り、URL をクリックして機能するかどうかを検証します。  
  
5.  「次の手順」の指示に従って配置を完了します。  
  
## <a name="next-steps"></a>次の手順  
 配置を完了するには、Web ポータルまたは SharePoint 統合を構成する必要があります。 詳細については、「[Web ポータルの構成](../../reporting-services/report-server/configure-web-portal.md)」をご覧ください。  
  
 Windows ファイアウォールが有効になっている場合、レポート サーバーで使用するように構成されているポートは閉じられる可能性が高くなります。 ポートが閉じられている場合は、たとえばリモート クライアント コンピューターから Web ポータルを開こうとすると、空のページが返されます。 ファイアウォールの構成の詳細については、「 [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)」を参照してください。  
  
 Windows Vista または Windows Server 2008 を使用している場合は、Web ポータルをローカルで開く前に追加の手順が必要になります。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。  
  
 フォルダーを作成し、アイテムをアップロードし、レポートを実行してインストール状況を確認します。 インストール状況を確認するには、「 [Reporting Services のインストール状態の検証](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) 」の手順に従います。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [リモート管理用のレポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)   
 [レポート サーバーの構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
