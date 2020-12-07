---
description: ソリューションのアイテムの移動
title: ソリューションのアイテムの移動
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 871f86e949eb8c4567b6998f5f664de554e4f466
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497301"
---
# <a name="move-items-in-a-solution"></a>ソリューションのアイテムの移動
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] プロジェクトに含まれるプロジェクト アイテムには、クエリ、接続、およびその他のファイルがあります。 クエリとその他のファイルはソリューション エクスプローラーで別のプロジェクトに移動することができますが、接続は移動できません。  
  
### <a name="to-move-items-in-solution-explorer"></a>ソリューション エクスプローラーでアイテムを移動するには  
  
1.  ソリューション エクスプローラーで、移動するアイテムを選択します。  
  
2.  **[編集]** メニューの **[切り取り]** をクリックします。  
  
3.  ソリューション エクスプローラーで、移動先を選択します。  
  
4.  **[編集]** メニューの **[貼り付け]** をクリックします。  
  
ソリューション エクスプローラー内でクエリやその他のファイルをドラッグして、アイテムを移動することもできます。 アイテムをドラッグする場合は、ドラッグ操作の結果を目で見て確認できます。 クエリを別の種類のプロジェクトに移動する場合、そのクエリが移動先のプロジェクトでその他のファイルと見なされることがあります。  
  
> [!NOTE]  
> 接続を指定したクエリを移動しても、接続は移動先のプロジェクトに移動しません。 クエリを別のプロジェクトに移動すると、接続の設定は消去されます。  
  
## <a name="see-also"></a>参照  
[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[ソリューションの項目のコピー](../../ssms/solution/copy-items-in-a-solution.md)  
  
