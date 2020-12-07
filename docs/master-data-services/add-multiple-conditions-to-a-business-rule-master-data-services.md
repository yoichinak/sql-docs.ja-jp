---
description: ビジネス ルールに複数の条件を追加する (マスター データ サービス)
title: ビジネスルールに条件を追加する
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a3ecfda6bd7b2bbd885cc8cc4b12917289dd3142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495076"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>ビジネス ルールに複数の条件を追加する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]ではより複雑なルールが必要な場合に、複数の **AND** 条件または **OR** 条件をビジネス ルールに追加します。  
  
> [!NOTE]  
>  **OR** 演算子を使用するビジネス ルールを作成する場合は、個別に評価できる条件ステートメントごとに個別のルールを作成することを検討してください。 そうすることによって、必要に応じてルールを除外できるので、柔軟性が向上し、トラブルシューティングも容易になります。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   ビジネス ルールが存在する必要があります。 詳細については、「[ビジネス ルールを作成しパブリッシュする (マスター データ サービス)](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)」を参照してください。  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>ビジネス ルールに複数の条件を追加するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  [ **ビジネスルール/** ページ] の [ **モデル** ] ドロップダウンリストから、モデルを選択します。  
  
4.  **[エンティティ]** ドロップダウン リストから、エンティティを選択します。  
  
5.  **[メンバーの種類]** ドロップ ダウン リストから、メンバーの種類を選択します。  
  
6.  編集するビジネス ルールの行をクリックします。  
  
7.  **[編集]** をクリックします。  
  
8.  **If** ブロックの下で、左側にある論理演算子のドロップダウン リストから、 **AND/OR/ NOT**を選択します。  
  
9. **[追加]** をクリックします。 パネルが表示されます。  
  
10. **[属性]** ボックスの一覧から、属性を選択します。  
  
11. **[演算子]** ドロップダウン リストから、条件を選択します。  
  
12. すべての必須フィールドに入力します。  
  
13. **[保存]** をクリックします。 新しい行が **If** グリッドに追加されます。  
  
14. 他の条件も追加する場合は、手順 8 ～ 13 を繰り返します。  
  
    > [!TIP]  
    >  条件を削除するには、条件を選択して右クリックし、 **[削除]** をクリックします。  
  
    > [!TIP]  
    >  複数の条件を選択して右クリックすると、論理演算子内で条件をグループ化したり、特定の論理演算子内の条件のグループ化を解除したりできます。  
  
## <a name="see-also"></a>参照  
 [ビジネスルール &#40;マスターデータサービス&#41;](../master-data-services/business-rules-master-data-services.md)   
 [ビジネスルールの名前を変更する &#40;マスターデータサービス&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [通知を送信するようにビジネス ルールを構成する (マスター データ サービス)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
