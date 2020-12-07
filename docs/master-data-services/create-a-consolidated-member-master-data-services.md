---
description: 統合メンバーを作成する (マスター データ サービス)
title: 統合メンバーを作成する
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4465fa105492cd691f474664748a4b3aca0a4f3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461906"
---
# <a name="create-a-consolidated-member-master-data-services"></a>統合メンバーを作成する (マスター データ サービス)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で明示的階層の親ノードが必要な場合、統合メンバーを作成します。 データを一括で追加する場合は、ステージング テーブルを使用します。 詳細については、「[テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/import-data-from-tables-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>[前提条件]  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   メンバーを追加するエンティティの統合モデル オブジェクトに対する **更新** 権限が最低限必要です。さらに、エンティティ下の統合型に対する **作成権限** も必要です。  
  
### <a name="to-create-a-consolidated-member"></a>統合メンバーを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  メニュー バーの **[階層]** をポイントして、統合メンバーを追加する階層の名前をクリックします。  
  
5.  グリッドの上にある **[統合メンバー]** または **[階層内のすべての統合メンバー]** をクリックします。  
  
6.  左側のウィンドウで、統合メンバーの作成先として、ルート ノードまたは統合メンバーのいずれかを選択します。  
  
7.  **[追加]** をクリックします。  
  
8.  右側のペインのフィールドに入力します。  
  
9. 任意。 **[注釈]** ボックスに、メンバーを追加した理由についてのコメントを入力します。 そのメンバーにアクセスできるすべてのユーザーが、その注釈を表示できます。  
  
10. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [明示的階層 &#40;マスターデータサービスを作成し&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [リーフメンバー &#40;マスターデータサービスを作成&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)   
 [メンバー &#40;マスターデータサービス&#41;](../master-data-services/members-master-data-services.md)   
 [明示的階層 (マスター データ サービス)](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
