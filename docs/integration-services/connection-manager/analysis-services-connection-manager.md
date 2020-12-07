---
description: Analysis Services 接続マネージャー
title: Analysis Services 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 633dd8288a9168422d0e5187caa1265615911a8a
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130613"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services 接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用すると、パッケージは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを実行するサーバー、またはキューブとディメンション データへのアクセスを提供する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに接続できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でのパッケージ開発中に接続できるのは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]プロジェクトのみです。 実行時には、パッケージは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを配置したサーバーおよびデータベースに接続します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 実行タスクや [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクなどのタスクと、データ マイニング モデル トレーニング変換先などの変換先は、どちらも [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データべースの詳細については、「[多次元モデル データベース &#40;SSAS&#41;](/analysis-services/multidimensional-models/multidimensional-model-databases-ssas)」を参照してください。  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Analysis Services 接続マネージャーの構成  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーをパッケージに追加すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、実行時に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続として解決される接続マネージャーが作成され、接続マネージャーのプロパティが設定され、接続マネージャーがパッケージの **Connections** コレクションに追加されます。 接続マネージャーの **ConnectionManagerType** プロパティは、 **MSOLAP100** に設定されます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーは、次の方法で構成できます。  
  
-   Microsoft OLE Provider for Analysis Services プロバイダーの要件を満たすように構成された、接続文字列を指定します。  
  
-   接続する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを指定します。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続する場合、認証モードを指定します。  

> [!NOTE]    
>  Azure Data Factory (ADF) で SSIS を使用していて、Azure Analysis Services (AAS) インスタンスに接続する場合は、Multi-Factor Authentication (MFA) が有効になっているアカウントを使用することはできません。代わりに、対話機能/MFA を必要としないアカウント、またはサービス プリンシパルを使用する必要があります。 サービス プリンシパルを使用するには、[ここ](/azure/analysis-services/analysis-services-service-principal)を参照してサービス プリンシパルを作成し、サーバー管理者ロールを割り当てます。その後、**[特定のユーザー名とパスワードを使用する]** を選択して、接続マネージャーでサーバーにログオンし、最後に「`User name: app:YourApplicationID`」と「`Password: YourAuthorizationKey`」を入力します。
  
-   接続マネージャーから作成される接続を、実行時に保持するかどうかを指定します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
