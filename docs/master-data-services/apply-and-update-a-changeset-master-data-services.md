---
description: 変更セットの適用および更新 (マスター データ サービス)
title: 変更セットの適用および更新
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3a6a3cf2-1e77-43d3-a64a-855ae51258e7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 06373651ed453c412360e2cf6201c61752e637be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456837"
---
# <a name="apply-and-update-a-changeset-master-data-services"></a>変更セットの適用および更新 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  変更セットは、マスター データに対する保留中の変更のコレクションです。 変更セットをビューにローカルに適用したり、変更セット内の保留中の変更を追加、更新、削除したりできます。  
  
## <a name="prerequisites"></a>[前提条件]  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「 [機能領域のアクセス許可 &#40;マスターデータサービス&#41;](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   少なくとも、エンティティまたはその属性のいずれかに対する更新アクセス権が必要です。  
  
-   エンティティ管理者は、自分で所有する変更セットまたは承認のために送信された変更セットのみを表示できます。  
  
-   変更セットの状態がオープン状態または拒否状態のときは、自分で所有する変更セットのみを変更できます。  
  
## <a name="to-apply-and-update-a-changeset"></a>変更セットを適用および更新するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[変更セット]** を選択し、表示および変更する変更セットをダブルクリックします。  
  
4.  **[適用]** をクリックします。  
  
     保留中の変更がグリッド内のエンティティ メンバーに適用されます。 保留中の変更が強調表示されます。  
  
     メンバーを作成、削除、更新すると、変更セットが変更されます。  
  
5.  保留中の変更に戻すには、 **[変更セット]** ウィンドウのグリッド内で右クリックし、 **[戻す]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 [変更セットのコミットまたは送信 (マスター データ サービス)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [変更セット &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
