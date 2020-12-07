---
description: グループの条件を指定する方法 (Visual Database Tools)
title: グループの条件の指定
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 4bd698f250585e967511f9846bec34da0e2e80d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369048"
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>グループの条件を指定する方法 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
グループ全体に適用する条件を HAVING 句で指定すると、クエリに出力するグループを制限できます。 データをグループ化し、集計した後、HAVING 句で条件を適用します。 条件を満たすグループだけがクエリに表示されます。  
  
たとえば、 `titles` テーブルで、出版社別のすべての本の平均価格のうち、$10.00 を超える平均価格だけを表示できます。 その場合、HAVING 句に `AVG(price) > 10`などの条件を指定します。  
  
> [!NOTE]  
> 場合によっては、グループ全体に条件を適用する前に、グループから個別の行を削除する必要があります。 詳細については、「[同一クエリ内で HAVING 句および WHERE 句を使用する (Visual Database Tools)](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)」を参照してください。  
  
AND または OR で条件を結合して、HAVING 句に複合条件を作成できます。 検索条件での AND および OR の使用の詳細については、「[1 つの列に対して複数の検索条件を指定する (Visual Database Tools)](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)」を参照してください。  
  
### <a name="to-specify-a-condition-for-a-group"></a>グループの条件を指定するには  
  
1.  検索するグループを指定します。 詳しくは、「[クエリ結果内の行のグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)」をご覧ください。  
  
2.  条件の基準になる列が[抽出条件ペイン](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)にまだない場合は、抽出条件ペインに追加します。 条件に含まれている列が、既にグループ列または集計列となっている場合がよくあります。集計関数または GROUP BY 句の一部である列は使用できません。  
  
3.  **[フィルター]** 列で、グループに適用する条件を指定します。  
  
    次の例に示すように、 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) により、 [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)のステートメントに HAVING 句が自動的に作成されます。  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
4.  条件を追加指定するたびに、手順 2. および手順 3. を繰り返します。  
  
## <a name="see-also"></a>参照  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
