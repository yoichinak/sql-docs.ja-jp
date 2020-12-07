---
description: ウィザードを使用したモデルの配置パッケージの作成
title: ウィザードを使用してモデルの配置パッケージを作成する
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], creating
- models [Master Data Services], creating a deployment package
- creating packages [Master Data Services]
ms.assetid: b24ec4c2-1378-4c72-ac69-4ec2647030f0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7c776d67ebf49e39ae3593d9ac570fe251abb728
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477080"
---
# <a name="create-a-model-deployment-package-by-using-the-wizard"></a>ウィザードを使用したモデルの配置パッケージの作成

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  モデル オブジェクトのみのパッケージを作成するには、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のモデル配置ウィザードを使用します。 パッケージにデータを含める必要がある場合は、「 [MDSModelDeploy を使用したモデルの配置パッケージの作成](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)」を参照してください。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションで、 **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   モデルのパッケージを作成するには、そのモデルが存在する必要があります。 詳細については、「[モデルを作成する (マスター データ サービス)](../master-data-services/create-a-model-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-model-deployment-package"></a>モデルの配置パッケージを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデル ビュー]** ページのメニュー バーから **[システム]** をポイントして **[配置]** をクリックします。  
  
3.  **[モデル配置ウィザード]** で **[作成]** をクリックします。  
  
4.  **[パッケージの作成]** ページで **[モデル]** ボックスの一覧からモデルを選択します。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[Download]** をクリックします。  
  
7.  ファイルを保存します。  
  
8.  **[閉じる]** をクリックしてウィザードを閉じます。  
  
## <a name="next-steps"></a>次の手順  
  
-   [ウィザードを使用したモデルの配置パッケージの展開](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
## <a name="see-also"></a>参照  
 [モデルの配置 (マスター データ サービス)](../master-data-services/deploying-models-master-data-services.md)  
  
  
