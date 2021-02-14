---
description: 変更セットの承認または拒否 (マスター データ サービス)
title: 変更セットの承認または拒否
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 47ea1da154b6e27be84888361867e370945e7438
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100339559"
---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>変更セットの承認または拒否 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  変更セットは、マスター データに対する保留中の変更のコレクションです。 エンティティを変更する場合に管理者による承認を必要とする場合、変更セットが承認のために送信されます。管理者は、変更セットを確認したうえで、承認または拒否します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「 [機能領域のアクセス許可 &#40;マスターデータサービス&#41;](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   エンティティに対する管理者権限が必要です。  
  
-   エンティティの変更は、管理者による承認を必要とする必要があります。  
  
-   変更セットの状態が保留中の場合は、管理者が変更セットを確認したうえで、変更セットを承認または拒否できます。  
  
-   ユーザーは、自分自身が加えた変更を承認することはできません。 エンティティ管理者は、自分自身が加えた変更セットを承認するために 2 人目の管理者を割り当てる必要があります。  
  
## <a name="to-approve-or-reject-a-changeset"></a>変更セットを承認または拒否するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[Changesets]** (変更セット) を選択し、承認または拒否する変更セットをダブルクリックします。  
  
4.  **[適用]** をクリックして変更セットを適用し、保留中の変更を確認します。  
  
5.  変更セットを拒否して所有者に差し戻すには、 **[拒否]** をクリックします。  
  
6.  変更セットを承認するには、 **[承認]** をクリックします。 変更セットが自動的にコミットされます。  
  
## <a name="see-also"></a>参照  
 [変更セット &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの適用および更新 &#40;マスターデータサービス&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [変更セットのコミットまたは送信 (マスター データ サービス)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
