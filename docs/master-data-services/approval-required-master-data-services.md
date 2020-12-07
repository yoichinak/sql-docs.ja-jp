---
description: 承認が必要 (マスター データ サービス)
title: 承認が必要
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f93514c1efd561aa989c03373f91edc2d552eba9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456822"
---
# <a name="approval-required-master-data-services"></a>承認が必要 (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、管理者はエンティティを「承認が必要」に設定できます。 このエンティティに対するすべての変更には、エンティティ管理者の確認と承認が必要になります。  
  
> [!NOTE]  
>  リーフ メンバーに加えられた変更には、承認が必要です。 非推奨の明示的階層とコレクションに加えられた変更は、承認がバイパスされます。  
>   
>  ステージング テーブルの処理によって行われた変更は、承認がバイパスされます。  
>   
>  ビジネス ルールによって行われた変更は、承認がバイパスされます。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [システム管理] 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[管理者 (マスター データ サービス)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   エンティティが存在する必要があります。 詳細については、「 [Create a Entity &#40;マスターデータサービス](../master-data-services/create-an-entity-master-data-services.md)」を参照してください&#41;  
  
## <a name="to-enable-approval-required-for-an-entity"></a>エンティティに対して「承認が必要」を有効にするには  
  
1.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページでグリッドからモデルを選択し、 **[エンティティ]** をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、  **[承認が必要]** を有効にするエンティティの行をグリッドから選択します。  
  
4.  **[編集]** をクリックし、 **[承認が必要]** を選択して **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [変更セット (マスター データ サービス)](../master-data-services/changesets-master-data-services.md)  
  
  
