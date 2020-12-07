---
description: 階層メンバーの権限を割り当てる (マスター データ サービス)
title: 階層メンバーの権限を割り当てる
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], assigning member permissions
- members [Master Data Services], assigning permissions
ms.assetid: e1b8b46a-7cd1-4a7d-9345-dd7df081e145
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6201fa319ef3f0ae35f1fecd0643954ab814b085
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456781"
---
# <a name="assign-hierarchy-member-permissions-master-data-services"></a>階層メンバーの権限を割り当てる (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  階層メンバーに権限を割り当てて、 **の** [エクスプローラー] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]機能領域にあるデータを表示するためのアクセス権をユーザーまたはグループに付与します。  
  
 階層メンバーの権限はオプションです。 階層メンバーの権限は、必須であるモデル オブジェクトの権限に粒度を追加します。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-assign-hierarchy-member-permissions"></a>階層メンバーの権限を割り当てるには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  **[ユーザー]** または **[グループ]** ページで、編集するユーザーまたはグループの行を選択します。  
  
3.  **[選択したユーザーの編集]** をクリックします。  
  
4.  **[階層メンバー]** タブをクリックします。  
  
5.  **[モデル]** ボックスの一覧からモデルを選択します。  
  
6.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
7.  **[階層]** ボックスの一覧から階層を選択します。  
  
8.  **[編集]** をクリックします。  
  
9. ツリーを展開して、権限を割り当てる階層ノードをクリックします。  
  
10. メニューから、 **作成**、 **読み取り、更新** 、および **削除** 権限の組み合わせ、または **拒否** 権限を選択します。  
  
11. **[保存]** をクリックします。  
  
    > [!NOTE]  
    >  階層メンバーの権限は、すぐには有効になりません。 詳細については、「[メンバー権限を直ちに適用する (マスター データ サービス)](../master-data-services/immediately-apply-member-permissions-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスターデータサービス &#40;階層メンバーの権限を削除&#41;](../master-data-services/delete-hierarchy-member-permissions-master-data-services.md)   
 [モデルオブジェクト権限の割り当て &#40;マスターデータサービス&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [階層メンバーの権限 (マスター データ サービス)](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
