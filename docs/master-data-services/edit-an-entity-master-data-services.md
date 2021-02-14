---
description: エンティティを編集する (マスター データ サービス)
title: エンティティを編集する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], changing name
ms.assetid: 6a5b9f14-6dfc-49d7-a771-e96461d4feae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 55cc510ecfb781d1d4366d9df928223139116fde
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341743"
---
# <a name="edit-an-entity-master-data-services"></a>エンティティを編集する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、エンティティを編集することができます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-edit-an-entity"></a>エンティティを編集するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [ **モデルの管理** ] ページで、グリッドからモデルを選択し、[ **エンティティ**] をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、変更するエンティティの行をグリッドから選択し、 **[編集]** をクリックします。  
  
4.  **[名前]** ボックスに、エンティティの新しい名前を入力します。  
  
5.  **[説明]** フィールドに、エンティティの新しい説明を入力します。  
  
6.  **[ステージング テーブルの名前]** フィールドに、ステージング テーブルの新しい名前を入力します。  
  
7.  **[トランザクション ログの種類]** フィールドで、ドロップダウン リストから新しいトランザクション ログの種類を選択します。  
  
     詳細については、「[エンティティのトランザクション ログの種類の変更 (マスター データ サービス )](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)」を参照してください。  
  
8.  **[コードの値を自動的に作成]** チェックボックスをオンまたはオフにします。  
  
     詳細については、「[コードの自動作成 (マスター データ サービス)](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。  
  
9. **[データ圧縮を有効にする]** チェックボックスをオンまたはオフにします。 既定では、行の圧縮は有効になっています。  
  
     詳細については、「[データ圧縮](../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
## <a name="status"></a>Status  
 グリッドの状態列には、エンティティに対する操作の状態が示されます。 **[エンティティの保存]** をクリックすると、エンティティが更新中であることを示す次の画像が表示されます。  
  
 ![状態を更新するためのアイコン](../master-data-services/media/mds-statusicon-updating.png "状態を更新するためのアイコン")  
  
 エンティティの作成または編集中にエラーが発生すると、次の画像が表示されます。  
  
 ![エラー状態のアイコン](../master-data-services/media/mds-statusicon-error.png "エラー状態のアイコン")  
  
 適切な状態のときは、次の画像が表示されます。  
  
 ![OK 状態のアイコン](../master-data-services/media/mds-statusicon-ok.png "OK 状態のアイコン")  
  
## <a name="see-also"></a>参照  
 [明示的階層 &#40;マスターデータサービス&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [エンティティ &#40;マスターデータサービスの削除&#41;](../master-data-services/delete-an-entity-master-data-services.md)   
 [エンティティ (マスター データ サービス)](../master-data-services/entities-master-data-services.md)  
  
  
