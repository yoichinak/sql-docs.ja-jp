---
description: モデルを編集する (マスター データ サービス)
title: モデルを編集する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6d409886b398aaace940cca8f21ee17682bfe2ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88389538"
---
# <a name="edit-model-master-data-services"></a>モデルを編集する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、モデルの名前と説明を変更し、トランザクション ログを保持する日数を指定できます。  
  
 詳細については、「[トランザクション (マスター データ サービス)](../master-data-services/transactions-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-change-a-model"></a>モデルを変更するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデル ビュー]** ページのメニュー バーから **[管理]** をポイントして **[モデル]** をクリックします。  
  
3.  **[モデルの管理]** ページで、グリッドから、モデルの名前または説明を変更する行を選択します。  
  
4.  **[編集]** をクリックします。  
  
5.  **[名前]** ボックスに、モデルの新しい名前を入力します。  
  
6.  **[説明]** フィールドに、モデルの新しい説明を入力します。  
  
7.  **[Log Retention Days]** (ログの保持日数) フィールドで、ログ データを保持するためのオプションのいずれかを選択します。 既定値は **[システム設定]** です。これは、値が [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]のシステム設定から継承されることを示します。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
     システム設定をオーバーライドし、トランザクション ログ データを削除しない場合は、**[いいえ]** を選択します。 今日のログデータのみを保持し、過去のすべての日のログデータを切り捨てるには、[ **はい]** を選択し、[ **日** ] フィールドを0に設定します。 指定した日数のログ データを保持するには、 **[はい]** を選択し、 **[日間]** フィールドに目的の日数を設定します。  
  
8.  **[モデルの保存]** をクリックします。  
  
 グリッドの **[状態]** 列には、モデルに対する操作の状態が示されます。 [ **モデルの保存** ] ボタンをクリックすると、 ![更新](../master-data-services/media/mds-model-status-updating.png "更新中") 中のイメージが表示されます。これは、モデルが更新中であることを示します。 モデルの作成時または編集時にエラーが発生した場合は、 ![エラー](../master-data-services/media/mds-model-status-error.png "エラー") イメージが表示されます。 それ以外の場合、状態は [OK] になり、 ![[Ok]](../master-data-services/media/mds-model-status-ok.png "[OK]") のイメージが表示されます。  
  
## <a name="see-also"></a>参照  
 [モデル &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [モデル &#40;マスターデータサービスの削除&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [モデル (マスター データ サービス)](../master-data-services/models-master-data-services.md)  
  
  
