---
description: 列の別名の作成 (Visual Database Tools)
title: 列の別名の作成
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 53d94906857c8a2e8c272d99f6545ee2eadb99f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480050"
---
# <a name="create-column-aliases-visual-database-tools"></a>列の別名の作成 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
列名に別名を作成すると、列名、計算、および集計値を簡単に操作できるようになります。 たとえば、列の別名を作成するのは次の場合です。  
  
-   `(quantity * unit_price)` などの式や集計関数に対して、"Total Amount" などの列名を作成する場合。  
  
-   次のものに対する `"d_id"` など、列名の短縮形を作成する場合: `"discounts.stor_id."`  
  
列の別名を定義すると、その別名を選択クエリで使用してクエリ出力を指定できます。  
  
### <a name="to-create-a-column-alias"></a>列の別名を作成するには  
  
1.  **[抽出条件ペイン]** で、別名を作成するデータ列を含む行を指定し、必要に応じて出力対象として設定します。 グリッドにデータ列がない場合は、列を追加します。  
  
2.  その行の **[エイリアス]** 列に別名を入力します。 別名を付けるときは、SQL の名前付け規則に従う必要があります。 入力した別名にスペースが含まれる場合は、自動的に区切り記号が付きます。  
  
## <a name="see-also"></a>参照  
[クエリへの列の追加 (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[クエリ結果の要約 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
