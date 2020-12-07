---
description: データ品質照合の列 (Excel 用 MDS アドイン)
title: データ品質照合の列
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d55d071bac84fee4d97175fc7d4da502feaaebb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257947"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>データ品質照合の列 (Excel 用 MDS アドイン)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]でデータを照合した後、リボンの **[データ品質]** グループの **[詳細の表示]** をクリックすると照合の詳細が含まれる列を表示できます。  
  
 次の表に、データの照合時に表示される列を示します。  
  
|名前|説明|  
|----------|-----------------|  
|**CLUSTER_ID**|類似レコードのグループ化に使用する一意識別子です。 類似するすべての行は、同じ **CLUSTER_ID**を持ちます。 **CLUSTER_ID** が行に対して表示されない場合、類似レコードが見つかっていません。|  
|**RECORD_ID**|レコードの識別に使用する一意識別子です。 MDS リポジトリに格納されているコード値と同様に、レコードの識別に使用される値です。 照合が実行されるたびに自動的に生成されます。|  
|**PIVOT_MARK**|他のレコードと比較される任意のレコードで、スコアの値はありません。|  
|**学生**|グループ内のレコードがピボット レコードとどの程度類似しているかを表します。 このスコアは DQS によって決定されます。 スコアが表示されない場合、そのレコードは他のレコードのピボットであるか、照合が見つかりませんでした。|  
  
## <a name="see-also"></a>参照  
 [Excel 用 MDS アドインでのデータ品質照合](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [類似データ &#40;Excel 用 MDS アドインに一致&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [データ照合](../../data-quality-services/data-matching.md)  
  
  
