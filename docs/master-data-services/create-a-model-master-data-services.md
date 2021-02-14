---
title: モデルの作成
description: モデルオブジェクトを格納するためにマスターデータサービスでモデルを作成する方法について説明します。 [システム管理] 領域のアクセス許可が必要です。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f153a6b7bf2f4ceef65b06d02a825620ea7b3fb2
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100272623"
---
# <a name="create-a-model-master-data-services"></a>モデルを作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でモデルを作成してモデル オブジェクトを含めます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-model"></a>モデルを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデル ビュー]** ページのメニュー バーから **[管理]** をポイントして **[モデル]** をクリックします。  
  
3.  **[モデルの管理]** ページで **[追加]** をクリックします。 右側にパネルが表示されます。  
  
4.  **[名前]** ボックスに、モデルの名前を入力します。  
  
5.  (必要に応じて) **[説明]** フィールドに、モデルの説明を入力します。  
  
6.  **[Log Retention Days]** (ログの保持日数) フィールドで、ログ データを保持するためのオプションのいずれかを選択します。 既定値は **[システム設定]** です。これは、値が [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]のシステム設定から継承されることを示します。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
     システム設定をオーバーライドし、トランザクション ログ データを削除しない場合は、**[いいえ]** を選択します。 今日のログデータのみを保持し、過去のすべての日のログデータを切り捨てるには、[ **はい]** を選択し、[ **日** ] フィールドを0に設定します。 指定した日数のログ データを保持するには、 **[はい]** を選択し、 **[日間]** フィールドに目的の日数を設定します。  
  
7.  (オプション) **[モデルと同じ名前のエンティティを作成する]** をクリックして、モデルと同じ名前のエンティティを作成します。  
  
8.  **[モデルの保存]** をクリックします。  
  
 作成されたモデルごとに、8 列の行がグリッドに追加されます。 8 つの列は次のとおりです。  
  
-   **[状態]**: モデルの状態。 [ **モデルの保存** ] ボタンをクリックすると、 ![更新](../master-data-services/media/mds-model-status-updating.png "Updating") 中のイメージが表示されます。これは、モデルが更新中であることを示します。 モデルの作成時または編集時にエラーが発生した場合は、 ![エラー](../master-data-services/media/mds-model-status-error.png "誤り") イメージが表示されます。 それ以外の場合、状態は [OK] になり、 ![[Ok]](../master-data-services/media/mds-model-status-ok.png "OK") のイメージが表示されます。  
  
-   **[名前]**: モデル名。  
  
-   **[説明]**: モデルの説明。  
  
-   **[Log Retention Days]**(ログの保持日数): モデルのログを保持する日数。  
  
-   **[作成者]**: モデルを作成したユーザーのユーザー名。  
  
-   **[Created Date and Time]**(作成日時): モデルが作成された日時。  
  
-   **[Updated By]**(更新者): モデルを最後に更新したユーザーのユーザー名。  
  
-   **[Updated Date and Time]**(更新日時): モデルが最後に更新された日時。  
  
## <a name="next-steps"></a>次の手順  
  
-   [エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [モデル &#40;マスターデータサービス&#41;](../master-data-services/models-master-data-services.md)   
 [エンティティ &#40;マスターデータサービス&#41;](../master-data-services/entities-master-data-services.md)   
 [モデル &#40;マスターデータサービスの削除&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [モデルの編集 &#40;マスターデータサービス&#41;](../master-data-services/edit-model-master-data-services.md)   
 [トランザクション (マスター データ サービス)](../master-data-services/transactions-master-data-services.md)  
  
  
