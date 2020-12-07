---
description: モデル オブジェクト権限を割り当てる (Master Data Services)
title: モデル オブジェクト権限を割り当てる
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9b79a9428df0dc528190281070ea33b3a2c21b25
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456747"
---
# <a name="assign-model-object-permissions-master-data-services"></a>モデル オブジェクト権限を割り当てる (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、 **の** [エクスプローラー] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]機能領域内のデータにユーザーまたはグループがアクセスできるようにする必要があるとき、またはユーザーまたはグループを管理者にする必要があるときは、モデル オブジェクトに権限を割り当てます。  
  
> [!NOTE]  
>  モデルに権限を割り当てると、その他のすべてのモデルへの権限は暗黙的に拒否されます。 モデル オブジェクト権限を割り当てない場合、ユーザーまたはグループは **[エクスプローラー]** のデータにアクセスできません。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-assign-model-object-permissions"></a>モデル オブジェクト権限を割り当てるには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  **[ユーザー]** または **[グループ]** ページで、編集するユーザーまたはグループの行を選択します。  
  
3.  **[選択したユーザーの編集]** をクリックします。  
  
4.  **[モデル]** タブをクリックします。  
  
5.  **[モデル]** ボックスの一覧からモデルを選択します (オプション)。  
  
6.  **[編集]** をクリックします。  
  
7.  ツリーを展開して、権限を割り当てるモデル オブジェクトをクリックします。  
  
8.  メニューから、[読み取り]、[作成]、[更新]、[削除]、または [拒否] の組み合わせを選択します。  
  
9. ユーザー モデル管理者を作成する必要がある場合、最上位のモデルで **[管理]** を選択します。  
  
10. **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   (省略可能) [階層メンバーの権限を割り当てる (マスター データ サービス)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [マスターデータサービス&#41;&#40;モデルオブジェクト権限の削除 ](../master-data-services/delete-model-object-permissions-master-data-services.md)   
 [モデルオブジェクト権限 &#40;マスターデータサービス&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [モデル管理者を作成する (マスター データ サービス)](../master-data-services/create-a-model-administrator-master-data-services.md)  
  
  
