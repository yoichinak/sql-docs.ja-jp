---
description: 変更セットのコミットまたは送信 (マスター データ サービス)
title: 変更セットのコミットまたは送信
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 47675ce7f7ac4704db9578564020c67fdc3b30b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430104"
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>変更セットのコミットまたは送信 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  変更セットは、マスター データに対する保留中の変更のコレクションです。 エンティティの変更が管理者の承認を必要としない場合は、変更セットをコミットできます。 エンティティの変更が管理者の承認を必要とする場合は、承認を受けるために変更セットを送信できます。  
  
## <a name="prerequisites"></a>[前提条件]  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   エンティティの変更が管理者の承認を必要としない場合は、変更セットを自分が所有し、変更セットの状態がオープンである場合のみ、変更セットをコミットできます。  
  
-   エンティティの変更が管理者の承認を必要とする場合は、変更セットを自分が所有し、変更セットの状態がオープンまたは拒否である場合のみ、承認を受けるために変更セットを送信できます。  
  
## <a name="to-commit-a-local-changeset"></a>ローカルの変更セットをコミットするには  
 コミット オプションは、エンティティ管理者が承認の必要性を有効にしていないエンティティでローカルの変更セットにのみ使用できます。  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[変更セット]** を選択し、コミットする変更セットをダブルクリックします。  
  
4.  **[コミット]** をクリックします。  
  
## <a name="to-submit-a-changeset"></a>変更セットを送信するには  
 送信オプションは、エンティティ管理者が承認の必要性を有効にしているエンティティの変更セットでのみ使用できます。  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[変更セット]** を選択し、送信する変更セットをダブルクリックします。  
  
4.  **[送信]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [変更セット &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの適用および更新 &#40;マスターデータサービス&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
