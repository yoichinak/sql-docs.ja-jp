---
description: 明示的階層を作成する (マスター データ サービス)
title: 明示的階層を作成する
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8512e53686d747fedb8ac5158a388e48b38469e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461814"
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>明示的階層を作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で任意のレベルでメンバーが存在できる不規則階層が必要な場合、明示的階層を作成します。 明示的階層には、1 つのエンティティのメンバーが含まれています。  
  
 明示的階層を作成したら、 **[エクスプローラー]** 機能領域で明示的階層にメンバーを追加できます。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   [ **システム管理** ] 機能領域にアクセスするためのアクセス許可が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスターデータサービス&#41;](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   エンティティは、明示的階層およびコレクションに対して有効化されている必要があります。  
  
### <a name="to-create-an-explicit-hierarchy"></a>明示的階層を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  [ **モデルの管理** ] ページで、グリッドからモデルを選択し、[ **エンティティ**] をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、明示的階層を作成するエンティティの行をグリッドから選択します。  
  
4.  [ **明示的階層**] をクリックします。  
  
5.  **[Manage Explicit Hierarchy]** (明示的階層の管理) ページで、 **[追加]** をクリックします。  
  
6.  **[名前]** ボックスに階層の名前を入力します。  
  
7.  必要に応じて、 **[必須階層]** チェック ボックスをオフにして、任意の階層として明示的階層を作成します。 階層の種類の詳細については、「 [明示的階層 (マスター データ サービス)](../master-data-services/explicit-hierarchies-master-data-services.md)」を参照してください。  
  
8.  **[保存]** をクリックします。  
  
## <a name="grid-columns"></a>グリッド列  
 作成する各明示的階層で、グリッドに 7 列の行が追加されます。 次に、各列について説明します。  
  
|名前|説明|  
|----------|-----------------|  
|Status|エンティティの状態。 **[保存]** をクリックすると、エンティティが更新中であることを示す次のイメージが表示されます。<br /><br /> ![状態を更新するためのアイコン](../master-data-services/media/mds-statusicon-updating.png "状態を更新するためのアイコン")<br /><br /> エンティティの作成または編集中にエラーが発生すると、次のイメージが表示されます。<br /><br /> ![エラー状態のアイコン](../master-data-services/media/mds-statusicon-error.png "エラー状態のアイコン")<br /><br /> 適切な状態の場合は、次のイメージが表示されます。<br /><br /> ![OK 状態のアイコン](../master-data-services/media/mds-statusicon-ok.png "OK 状態のアイコン")|  
|名前|明示的階層の名前。|  
|必須|明示的階層が必須かどうかを指定します。|  
|作成者|明示的階層を作成したユーザーの名前。|  
|作成日時|明示的階層が作成された日時。|  
|更新者|明示的階層を更新したユーザーの名前。|  
|更新日|明示的階層が最後に更新された日時。|  
  
## <a name="next-steps"></a>次の手順  
  
-   [統合メンバーを作成する (マスター データ サービス)](../master-data-services/create-a-consolidated-member-master-data-services.md)  
  
  
  
## <a name="see-also"></a>参照  
 [明示的階層 &#40;マスターデータサービス&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [明示的なキャップを持つ派生階層 &#40;マスターデータサービス&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [明示的階層名を変更する (マスター データ サービス)](../master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  

