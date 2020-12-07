---
description: 共有データ ソースと埋め込みデータ ソースの比較 - レポート ビルダーと Reporting Services (SSRS)
title: 共有データ ソースと埋め込みデータ ソースの比較 - レポート ビルダーと Reporting Services |Microsoft Docs
ms.date: 11/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25721242123d34c1cb4b826cd937df2decf02523
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484995"
---
# <a name="compare-shared-and-embedded-data-sources---report-builder--reporting-services-ssrs"></a>共有データ ソースと埋め込みデータ ソースの比較 - レポート ビルダーと Reporting Services (SSRS)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]
 
共有または埋め込みのいずれかのデータソースを使用してデータに接続できます。 "*共有データ ソース*" は、レポートとは無関係に定義されます。 これは、レポート サーバーまたは SharePoint サイト上の複数のレポートで使用できます。 "*埋め込みデータ ソース*" は、レポート内で定義されます。 これはそのレポート内でのみ使用できます。 

 共有データ ソースは、よく使用するデータ ソースがある場合に役立ちます。 可能な限り共有データ ソースを作成して使用することをお勧めします。 レポートやレポートへのアクセスが管理しやすくなり、レポートやレポートからアクセスするデータ ソースの安全性を高めることができます。 共有データ ソースが必要な場合、システム管理者にその作成を依頼する必要が生じることがあります。  
  
 埋め込みデータ ソースは、"*レポート固有のデータ ソース*" とも呼ばれ、レポート定義に保存されるデータ接続です。 埋め込まれたデータ ソースの接続情報は、それが埋め込まれたレポートでのみ使用できます。 埋め込みデータ ソースを定義および管理するには、 **[データ ソースのプロパティ]** ダイアログ ボックスを使用します。  
  
 埋め込みデータ ソースと共有データ ソースとでは、作成、格納、および管理の方法が異なります。  
  
-   レポート デザイナーで、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] プロジェクトの一部として、埋め込みデータ ソースまたは共有データ ソースを作成します。 プレビュー用にローカルで使用するか、プロジェクトの一部としてレポート サーバーまたは SharePoint サイトに配置するかを制御することができます。 自分のコンピューターおよびレポート サーバー、さらにレポートの配置先の SharePoint サイトにインストールされているカスタム データ拡張機能を使用できます。  
  
     システム管理者は、別のデータ処理拡張機能および .NET Framework データ プロバイダーをインストールおよび設定できます。 詳細については、「[データ処理拡張機能と .NET Framework データ プロバイダー (SSRS)](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)」を参照してください。  
  
     <xref:Microsoft.ReportingServices.DataProcessing> API を使ってデータ処理拡張機能を作成すると、その他の種類のデータ ソースもサポートできます。  
  
-   [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]で、レポート サーバーまたは SharePoint サイト上の保存先を参照して共有データ ソースを選択するか、または、レポートに埋め込みデータ ソースを作成します。 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] で共有データ ソースを作成することはできません。 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] でカスタム データ拡張機能を使用することはできません。  

## <a name="summary-of-differences"></a>相違点のまとめ
  
 次の表は、埋め込みデータ ソースと共有データ ソースの違いをまとめたものです。  
  
|説明|埋め込み<br /><br /> Data Source|共有<br /><br /> Data Source|  
|-----------------|------------------------------|----------------------------|  
|データ接続がレポート定義に埋め込まれる|![利用可能](../../reporting-services/report-data/media/greencheck.gif "利用可能")||  
|レポート サーバー上のデータ接続へのポインターがレポート定義に埋め込まれる||![利用可能](../../reporting-services/report-data/media/greencheck.gif "利用可能")|  
|レポート サーバー上で管理|![利用可能](../../reporting-services/report-data/media/greencheck.gif "利用可能")|![利用可能](../../reporting-services/report-data/media/greencheck.gif "利用可能")|  
|共有データセットに必要||![利用可能](../../reporting-services/report-data/media/greencheck.gif "利用可能")|  
|コンポーネントに必要||![利用可能](../../reporting-services/report-data/media/greencheck.gif "利用可能")|  

## <a name="next-steps"></a>次のステップ

[共有データ ソースを作成および管理する](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[埋め込みデータ ソースを作成および変更する](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[配置プロパティを設定する](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
