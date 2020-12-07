---
description: インデックスを作成する (マスター データ サービス)
title: インデックスを作成する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 48d78cffb116996848035e3675e707994226f080
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461830"
---
# <a name="create-an-index-master-data-services"></a>インデックスを作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  頻繁にクエリを実行する属性の一覧にカスタム インデックスを作成して、クエリのパフォーマンスを高めます。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [システム管理] 機能領域にアクセスする権限が必要です。 詳細については、「 [機能領域のアクセス許可 &#40;マスターデータサービス&#41;](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
 **インデックスを作成するには**  
  
1.  マスター データ マネージャーで、 **[システム管理]** をクリックします。  
  
2.  **[Manage Model]** (モデルの管理) ページでグリッドからモデルを選択し、 **[エンティティ]** をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、インデックスを作成するエンティティの行を **グリッド** から選択します。  
  
4.  **[インデックス]** をクリックします。  
  
5.  **[名前]** ボックスに、このインデックスの名前を入力します。  
  
6.  一意なインデックスを作成する場合は、 **[Is Unique]** (一意) を選択します。 インデックスの種類の詳細については、「 [カスタム インデックス (マスター データ サービス)](../master-data-services/custom-index-master-data-services.md)」を参照してください。  
  
7.  **[使用できる属性]** ボックスの属性をクリックし、 **[追加]** 矢印をクリックします。 すべての属性を追加するには、 **[すべて追加]** 矢印をクリックします。  
  
8.  **[保存]** をクリックします。  
  
 作成されたインデックスごとに、4 列の行がグリッドに追加されます。 次の表で各列について説明します。  
  
|列名|説明|  
|-----------------|-----------------|  
|Status|インデックスの状態。<br /><br /> [ **保存**] をクリックすると、 ![更新中の状態の](../master-data-services/media/mds-statusicon-updating.png "状態を更新するためのアイコン") 画像を示すアイコンが表示され、インデックスが更新中であることを示します。<br /><br /> インデックスの作成中または編集中にエラーが発生した場合は、 ![エラー状態の画像のアイコン](../master-data-services/media/mds-statusicon-error.png "エラー状態のアイコン") が表示されます。<br /><br /> それ以外の場合、状態は [OK] になり、 ![[OK] ステータスイメージのアイコン](../master-data-services/media/mds-statusicon-ok.png "OK 状態のアイコン") が表示されます。|  
|名前|インデックス名。|  
|[Is Unique]|インデックスが一意かどうかを示します。|  
|[On Attributes] (属性)|インデックスが定義されている属性の表示名を示します。|  
  
 インデックスをクリックすると、次の情報が表示されます。  
  
-   **作成者**: インデックスを作成したユーザーの名前。  
  
-   **作成日時**: インデックスが作成された日時。  
  
-   **更新者**: インデックスを最後に更新したユーザーの名前。  
  
-   **更新日時**: インデックスが最後に更新された日時。  
  
## <a name="next-steps"></a>次の手順  
 [インデックスの編集と削除 (マスター データ サービス)](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [カスタム インデックス (マスター データ サービス)](../master-data-services/custom-index-master-data-services.md)  
  
  
