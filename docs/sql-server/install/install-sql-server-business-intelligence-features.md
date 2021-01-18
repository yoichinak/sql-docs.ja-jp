---
title: ビジネス インテリジェンス機能のインストール
description: この記事では、Microsoft ビジネス インテリジェンス プラットフォームに含まれる SQL Server の機能をインストールするための情報へのリンクを提供します。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 67399b24-e48a-49f3-9dd4-32d78c6a2ece
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e901d6dd36709994c056eaa5ef159303d49c00f1
ms.sourcegitcommit: 3ec49252e82590de0fe559a8574606ae213f6f3b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "97975513"
---
# <a name="install-sql-server-business-intelligence-features"></a>SQL Server のビジネス インテリジェンス機能のインストール

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Microsoft Business Intelligence プラットフォームに含まれる SQL Server 機能には、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および分析データの作成または操作に使用されるいくつかのクライアント アプリケーションがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップのドキュメントのこのセクションでは、これらの機能のインストール方法について説明します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、スタンドアロン サーバーとして、スケールアウト構成で、または SharePoint ファームの共有サービス アプリケーションとしてインストールできます。 サービスをファームにインストールすると、SharePoint のみで使用できる BI 機能が有効になります。これらの機能には、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint と、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の表形式モデルのデータベースで実行される [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] を対話形式でアドホック実行したレポート デザイナーの [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] が含まれます。  
  
## <a name="sql-server-bi-features"></a>SQL Server BI 機能  
 BI コンポーネントを含むすべての SQL Server 機能は、SQL Server セットアップでインストールされます。 次のリンクは、各 BI 機能に固有の補足情報を提供します。  
  
-   [Analysis Services のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)  
  
-   [Power Pivot モードでの Analysis Services のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)  
  
-   [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)  
  
-   [Integration Services のインストール](../../integration-services/install-windows/install-integration-services.md)  
  
-   [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)  
  
-   [Reporting Services のインストール](../../reporting-services/install-windows/install-reporting-services.md)  
  
-   [Reporting Services SharePoint モードのインストール](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

> [!NOTE]
> SQL Server Data Tools (SSDT) は、SQL Server 2016 に含まれていません。 [SQL Server Data Tools のダウンロード](https://go.microsoft.com/fwlink/?LinkID=616714)。
  
## <a name="see-also"></a>参照  
 [Reporting Services &#40;SSRS&#41; の新機能](https://msdn.microsoft.com/bc909063-6b84-4b3a-80d2-e93fc04b4b9d)   
 [Analysis Services の新機能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)   
 [Integration Services の新機能](../../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)   
 [マスター データ サービス &#40;MDS&#41; の新機能](../../master-data-services/what-s-new-in-master-data-services-mds.md)   
 [SQL Server のインストール](../../database-engine/install-windows/install-sql-server.md)   
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
