---
description: モデルの配置パッケージの編集
title: モデルの配置パッケージの編集
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6b0fdb7d-83dd-4392-9011-4ae642c471f1
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 81c8c6445041321adca7cfbc0761f0c396edb891
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88389568"
---
# <a name="edit-a-model-deployment-package"></a>モデルの配置パッケージの編集

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  このトピックでは、モデル全体ではなく、モデルの選択した部分を MDS に配置する方法について説明します。 これを行うには、モデル パッケージ エディターを使用して MDS モデル パッケージを編集します。  
  
 モデル パッケージ エディター ウィザードを使用すると、MDS パッケージに含めるモデル内の特定のエンティティ、派生階層、サブスクリプション ビュー、およびビジネス ルールを選択して、後で配置することができます。 配置しないモデルの部分は除外できます。 エンティティを選択すると、そのエンティティの依存オブジェクトもすべて自動的に選択されます。  
  
 モデル パッケージ エディターを使用して、MDSModelDeploy ツール (オブジェクトとデータを含むパッケージ ファイルを作成します) またはモデル配置ウィザード (モデル構造のみを含むファイルを作成します) で作成したパッケージ ファイル内のモデルの部分を選択します。 パッケージ内のモデルを編集したら、MDSModelDeploy ツールを使用してオブジェクトとデータを配置するか、モデル配置ウィザードを使用してモデル構造のみを配置します。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   モデル パッケージを編集するには、そのモデル パッケージが存在する必要があります。 詳細については、「[モデルの配置 (マスター データ サービス)](../master-data-services/deploying-models-master-data-services.md)」と「[ウィザードを使用したモデルの配置パッケージの作成](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)」、または「[MDSModelDeploy を使用したモデルの配置パッケージの作成](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)」を参照してください。  
  
### <a name="to-edit-a-model-deployment-package"></a>モデルの配置パッケージを編集するには  
  
1.  MDS サーバーの Windows エクスプ ローラーで、&lt; *ドライブ*&gt;:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration に移動します。  
  
2.  ModelPackageEditor.exe を実行します。  
  
3.  モデル パッケージ エディター ウィザードで、 **[参照]** をクリックしてパッケージが格納されているフォルダーに移動し、パッケージを選択して **[開く]** をクリックします。 **[次へ]** をクリックします。  
  
4.  配置するエンティティ、派生階層、サブスクリプション ビュー、またはビジネス ルールを選択します。 配置しない項目は選択を解除します。 **[次へ]** をクリックします。  
  
5.  配置する選択項目の一覧を確認します。 変更するには、 **[戻る]** をクリックして手順 4 を繰り返します。  
  
6.  **[参照]** をクリックし、部分的なパッケージを保存するフォルダーに移動して、部分的なパッケージのファイル名を入力します (.pkg 拡張子を付けます)。 **[保存]** をクリックします。  
  
7.  **[完了]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   [ウィザードを使用したモデルの配置パッケージの展開](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
-   [MDSModelDeploy を使用したモデルの配置パッケージの配置](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
