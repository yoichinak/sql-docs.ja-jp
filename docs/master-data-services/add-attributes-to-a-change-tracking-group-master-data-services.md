---
description: 変更の追跡グループに属性を追加する (マスター データ サービス)
title: Change Tracking グループへの属性の追加
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 154dc5a555e97d4de56f3a40981aad71e64fe22c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491501"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>変更の追跡グループに属性を追加する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で属性の値に対する変更を追跡する場合、変更の追跡グループに属性を追加します。  
  
> [!NOTE]  
>  変更の追跡グループに属性を追加した後に属性の値が変更されると、属性は [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで変更済みとしてフラグが付けられます。 変更に基づいてアクションを実行するビジネス ルールを作成します。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   変更の追跡グループに追加する属性が存在する必要があります。 詳細については、「 [テキスト属性を作成する (マスター データ サービス)](../master-data-services/create-a-text-attribute-master-data-services.md)」を参照してください。  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>属性を変更の追跡グループに追加するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [ **モデルの管理** ] ページで、グリッドからモデルを選択し、[ **エンティティ**] をクリックします。  
  
3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。  
  
4.  **[属性]** をクリックします。  
  
5.  **[属性の管理]** ページで、次のいずれかの操作を行います。  
  
    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。  
  
    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。  
  
    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。  
  
6.  編集する属性の行を選択し、 **[編集]** をクリックします。  
  
7.  **[変更の追跡の有効化]** チェック ボックスをオンにします。  
  
8.  **[変更の追跡グループ]** ボックスにグループの番号を入力します。  
  
9. **[属性の保存]** をクリックします。  
  
     編集済みの属性では、グリッドの **[Enable Change Tracking Group (変更の追跡グループを有効にする)]** 列が **[はい]\(グループ: 入力したグループ番号)** に変更されます。  
  
10. グループに含めるすべての属性に対して、この手順を繰り返します。 グループ内の各属性に対して同じ変更の追跡グループの番号を使用します。  
  
## <a name="next-steps"></a>次の手順  
  
-   [属性値の変更に基づいてアクションを開始する (マスター データ サービス)](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [テキスト属性 &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
