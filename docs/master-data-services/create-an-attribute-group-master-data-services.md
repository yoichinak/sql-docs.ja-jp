---
description: 属性グループを作成する (マスター データ サービス)
title: 属性グループを作成する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ffe84797d519961ab26e6d43fb48a5c4c2dd3e13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461839"
---
# <a name="create-an-attribute-group-master-data-services"></a>属性グループを作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、 **[エクスプローラー]** グリッドの個々のタブに属性を表示する場合、属性グループを作成します。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   少なくとも 1 つの属性が必要です。 詳細については、「 [テキスト属性を作成する (マスター データ サービス)](../master-data-services/create-a-text-attribute-master-data-services.md)」を参照してください。  
  
### <a name="to-create-an-attribute-group"></a>属性グループを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [ **モデルの管理** ] ページで、グリッドからモデルを選択し、[ **エンティティ**] をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、属性グループを作成するエンティティの行をグリッドから選択します。  
  
4.  **[属性グループ]** をクリックします。  
  
5.  [属性グループの管理] ページで、次のいずれかの操作を行い、 **[追加]** をクリックします。  
  
     対象の属性グループがリーフ メンバーの属性グループの場合は、ページの上部にある **[メンバーの種類]** ドロップダウン リストの **[リーフ]** を選択します。  
  
     対象の属性グループが統合メンバーの属性グループの場合は、 **[メンバーの種類]** ドロップダウン リストの **[統合]** を選択します。  
  
     対象の属性グループがコレクションの属性グループの場合は、 **[メンバーの種類]** ドロップダウン リストの **[コレクション]** を選択します。  
  
6.  **[リーフ グループ]**、 **[統合グループ]**、または **[コレクション グループ]** をクリックして、リーフ メンバー、統合メンバー、またはコレクションの属性グループを作成します。  
  
7.  **[名前]** ボックスに属性グループの名前を入力します。 この名前が **エクスプローラー**のタブに表示されます。  
  
8.  属性を追加するには、 **[使用できる属性]** ボックスの属性をクリックし、 **[追加]** 矢印をクリックします。 すべての属性を追加するには、 **[すべて追加]** 矢印をクリックします。  
  
9. **上** および **下** 向きの矢印をクリックして、属性の順序 (左から右) を変更します。  
  
10. **[使用できるユーザー]** ボックスのユーザーをクリックし、 **[追加]** 矢印をクリックします。 すべてのユーザーを追加するには、 **[すべて追加]** 矢印をクリックします。  
  
11. **[使用できるグループ]** ボックスのグループをクリックし、 **[追加]** 矢印をクリックします。 すべてのグループを追加するには、 **[すべて追加]** 矢印をクリックします。  
  
12. **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   [属性グループのユーザーへの表示 (マスター データ サービス)](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [属性グループ &#40;マスターデータサービス&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [属性 &#40;マスターデータサービス&#41;](../master-data-services/attributes-master-data-services.md)   
 [属性グループ名を変更する &#40;マスターデータサービス&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [属性グループ &#40;マスターデータサービスの削除&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)   
 [リーフ権限 (マスター データ サービス)](../master-data-services/leaf-permissions-master-data-services.md)   
   
  
  
