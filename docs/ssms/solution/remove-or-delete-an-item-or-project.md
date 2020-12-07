---
description: アイテムやプロジェクトのクリアまたは削除
title: アイテムやプロジェクトのクリアまたは削除
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5e8389848928507d29be094faaf626f99ba9c8ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491833"
---
# <a name="remove-or-delete-an-item-or-project"></a>アイテムやプロジェクトのクリアまたは削除
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] プロジェクトに含まれるプロジェクト アイテムには、クエリ、接続、およびその他のファイルがあります。 プロジェクトのクエリとその他のファイルは、記憶域に残したままソリューションからクリアできます。 現在のソリューションでは使用せずに、別のソリューションで使用する場合は、プロジェクトやアイテムをクリアします。  
  
### <a name="to-remove-a-project-item"></a>プロジェクト アイテムをクリアするには  
  
1.  ソリューション エクスプローラーで、クリアするプロジェクト アイテムを選択します。  
  
2.  **[編集]** メニューの **[削除]** をクリックします。  
  
3.  確認ダイアログで **[削除]** をクリックすると、プロジェクトからアイテムが削除されます。  
  
クリアしたアイテムは、ファイル システムにまだ存在しています。 したがって、クリアしたアイテムは、元のソリューションまたは別のソリューションに追加することができます。  
  
#### <a name="to-remove-a-project"></a>プロジェクトをクリアするには  
  
1.  ソリューション エクスプローラーで、クリアするプロジェクトを選択します。  
  
2.  **[編集]** メニューの **[削除]** をクリックします。  
  
3.  確認ダイアログで **[OK]** をクリックします。ソリューションからプロジェクトがクリアされます。  
  
プロジェクトは完全に削除できますが、最初に [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ソリューションからプロジェクトへの参照をすべてクリアし、次に [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows エクスプローラーを使用して、関連付けられているファイルを記憶域から完全に削除する必要があります。  
  
#### <a name="to-delete-a-project"></a>プロジェクトを削除するには  
  
1.  ソリューション エクスプローラーで、ソリューションから削除するプロジェクトをクリアします。  
  
2.  Windows エクスプローラーで、削除するプロジェクトまたはアイテムに関連付けられているファイルを検索して選択します。  
  
3.  **[ファイル]** メニューの **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[プロジェクトへの新規項目の追加](../../ssms/solution/add-new-items-to-a-project.md)  
[既存の項目をプロジェクトに追加する](../../ssms/solution/add-existing-items-to-a-project.md)  
  
