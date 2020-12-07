---
description: ネイティブ モードから SharePoint モードへの移行 (SSRS)
title: ネイティブから SharePoint への移行 | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: c5b15bec-6fde-4174-bcde-d043307244dd
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ba6eef61dd79dbbbe97326c888698b69152065ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454545"
---
# <a name="native-to-sharepoint-migration-ssrs"></a>ネイティブ モードから SharePoint モードへの移行 (SSRS)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサーバー モードを別のモードにアップグレードまたは変換することはできません。 たとえば、ネイティブ モードのレポート サーバーを SharePoint モードにアップグレードまたは変換することはできません。 モードが異なると使用されるデータベース スキーマも異なるため、モード間でレポート サーバー データベースをコピーすることはできません。 コンテンツはレポート サーバー間で移行できます。 使用するツールは、移行元サーバーと移行先サーバーに対して構成されたレポート サーバー モードの種類によって異なります。  
  
##  <a name="reporting-services-migration-tool"></a><a name="bkmk_native_to_sharepoint"></a> Reporting Services 移行ツール  
 このツールでは、ネイティブ モードの配置から SharePoint モードの配置へのコンテンツの移行がサポートされます。 SharePoint モードから SharePoint モードまたは SharePoint モードからネイティブ モードへの移行はサポートされません。  
  
 詳細については、「[Reporting Services 移行ツール](https://www.microsoft.com/download/details.aspx?id=29560)」(https://www.microsoft.com/download/details.aspx?id=29560) を参照してください。  
  
## <a name="use-script-to-migrate-content"></a>スクリプトを使用したコンテンツの移行  
 移行ツールが目的に合わない場合は、レポート サーバー データを手動で移行できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 間でのレポート アイテムの移行を完了するための手順の概要を次に示します。 この方法では、移行元サーバーまたは移行先サーバーとしてネイティブ モードまたは SharePoint モードをサポートしています。  
  
1.  暗号化キーをバックアップおよび復元します。 これは、データの暗号化に使用されるキーです。 暗号化キーは、パスワード (データ ソース接続用に保存されているパスワードなど) を暗号化するためにも使用されます。 ただし、パスワードを移行することはできないため、移行先の環境で再度入力する必要があります。  
  
2.  **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS スクリプト:** レポート サーバー Web サービスの SOAP メソッドを呼び出してデータベース間でデータをコピーする Visual Basic スクリプトを作成します。 スクリプトを実行するには、 **RS.exe** ユーティリティを使用します。 RS.exe は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]と共にインストールされます。  
  
    -   [レポート サーバー間でコンテンツをコピーするサンプル Reporting Services rs.exe スクリプト](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。 このトピックでは、CodePlex からダウンロードできるサンプル スクリプトの使用方法について説明します。  
  
    -   CodePlex にあるサンプル RSS スクリプト ( [レポート サーバー間でコンテンツを移行する Reporting Services RS.exe スクリプト](https://azuresql.codeplex.com/releases/view/115207))。  
  
    -   [Reporting Services を使ったスクリプトの作成と PowerShell](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)  
  
 次の表は、スクリプトを使用して移行できる [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] オブジェクトをまとめたものです。  
  
|オブジェクト|スクリプト化の可否|コメント|  
|------------|---------------------|--------------|  
|Reports|はい|移行後にデータソースのパスワードを再入力します。|  
|データソース|はい|移行後にレポートとデータソースとの間のリンクを再設定します。|  
|モデル|はい||  
|データセット|はい||  
|レポート パーツ||移行後にレポート パーツへのパスを確認または更新します。|  
|スケジュール|はい|ListSchedules メソッドに関する説明 (「 [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)」) を参照してください。|  
|サブスクリプション|はい|ListSubscriptions メソッドに関する説明 (「 [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md) 」) および <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A> に関する説明を参照してください。|  
|スナップショット|||

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
