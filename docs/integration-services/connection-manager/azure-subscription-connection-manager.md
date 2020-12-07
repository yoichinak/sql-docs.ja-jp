---
description: Azure サブスクリプション接続マネージャー
title: Azure サブスクリプション接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 277e92a906acb89960e16c941fbd71df023ddb23
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678990"
---
# <a name="azure-subscription-connection-manager"></a>Azure サブスクリプション接続マネージャー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Azure サブスクリプション接続マネージャー** を使用すると、Azure サブスクリプション ID と管理証明書のプロパティに指定した値を使用して、SSIS パッケージを Azure サブスクリプションに接続できます。  
  
 **Azure サブスクリプション接続マネージャー** は、 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。
  
1.  上記の **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで **[Azure サブスクリプション]** を選択し、 **[追加]** をクリックします。  次の **[Azure Subscription Connection Manager Editor]** (Azure サブスクリプション接続マネージャー エディター) ダイアログ ボックスが表示されます。  
  
    ![[Azure Subscription Connection Manager Editor]\(Azure サブスクリプション接続マネージャー エディター\) ダイアログ ボックスを示すスクリーンショット。](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  **[Azure サブスクリプション ID]** には、Azure サブスクリプションを一意に識別する Azure サブスクリプション ID を入力します。  この値は、 [Azure 管理ポータル](https://manage.windowsazure.com) の **[設定]** ページで確認できます。  
  
    ![[設定] ページの [サブスクリプション] タブが表示されている Azure 管理ポータルのスクリーンショット。](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  ドロップダウン リストから **[Management certificate store location (管理証明書ストアの場所)]** と **[Management certificate store name (管理証明書ストアの名前)]** を選択します。  
  
4.  **管理証明書の拇印** を入力するか、 **[参照]** をクリックして、選択したストアから証明書を選択します。 証明書は、サブスクリプションの管理証明書としてアップロードする必要があります。 これを行うには、Azure Portal の次のページで **[アップロード]** をクリックします (詳細については、こちらの [MSDN の投稿](/previous-versions/azure/gg551722(v=azure.100))を参照)。  
  
     ![[設定] ページの [管理証明書] タブが表示されている Azure 管理ポータルのスクリーンショット。](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  **[接続テスト]** をクリックして接続をテストします。  
  
6.  **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
