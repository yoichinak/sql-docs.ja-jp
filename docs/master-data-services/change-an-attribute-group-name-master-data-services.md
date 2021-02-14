---
description: 属性グループ名を変更する (マスター データ サービス)
title: 属性グループ名を変更する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], changing name
ms.assetid: 79510fcf-4c83-4426-bdd4-15b4170ecfbd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1ef8ddfdf5444683ebef8ffd82042cd6e83951cf
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100272863"
---
# <a name="change-an-attribute-group-name-master-data-services"></a>属性グループ名を変更する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、属性グループ名を変更できます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-change-an-attribute-group-name"></a>属性グループ名を変更するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [ **モデルの管理** ] ページで、グリッドからモデルを選択し、[ **エンティティ**] をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、属性グループを編集するエンティティの行をグリッドから選択します。  
  
4.  **[属性グループ]** をクリックします。  
  
5.  **[属性グループの管理]** ページで、 **[メンバーの種類]** ドロップダウン リストからメンバーの種類を選択し、更新するグループの種類に応じて **[リーフ]**、 **[統合]**、 **[コレクション]** を展開します。  
  
6.  更新する属性グループの名前をクリックし、 **[編集]** をクリックします。  
  
7.  **[名前]** ボックスに新しい名前を入力します。  
  
8.  **[グループの保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [属性グループ &#40;マスターデータサービス&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [属性グループ &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)   
 [属性グループを削除する &#40;マスター データ サービス&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)  
  
  
