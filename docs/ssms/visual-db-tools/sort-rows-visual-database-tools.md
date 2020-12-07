---
description: 行の並べ替え (Visual Database Tools)
title: 行の並べ替え
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2cc6ae5da87b1ef1f70c7b66fe3f06d8e6b2ed90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491585"
---
# <a name="sort-rows-visual-database-tools"></a>行の並べ替え (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
クエリ結果の行は、並べ替えることができます。 つまり、特定の列または列のセットを指定し、その値で結果セットの行の順序を決定できます。  
  
> [!NOTE]  
> 並べ替え順序を決定する要素として列の照合順序があります。 この照合順序は、 [[照合順序] ダイアログ ボックス](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)で変更できます。  
  
クエリ結果は、次の方法で並べ替えられます。  
  
-   **昇順または降順に行を並べ替える** 既定では、SQL は ORDER BY 句で指定された列を使用して、行を昇順に並べ替えます。 たとえば、書名を値段の安い順に並べるには、price 列を基準に行を単純に並べ替えます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
    ```  
  
    反対に、価格の高い本から順に書名を配列する場合は、最も高価なものを先頭にして並べ替えるように明示的に指定します。 つまり、price 列の値を降順にして結果行を並べ替えるように指定します。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **複数の列を使って並べ替える** たとえば、最初に州、次に都市の順序で並べ替えると、各著者に対して 1 行を表示する結果セットを作成できます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
    ```  
  
-   **結果セットに含まれない列を使って並べ替える** たとえば、価格が結果セットに含まれていなくても、価格の高い順に書名を並べた結果セットを作成できます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **派生列を使って並べ替える** たとえば、印税が最高額である本の書名を最初に表示する結果セットを作成できます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
    ```  
  
    各本の 1 冊あたりの印税を計算する式は、太字で示してあります。  
  
    派生列の計算には、上記の例のように SQL 構文を使用することも、スカラー値を返すユーザー定義関数を使用することもできます。 ユーザー定義関数の詳細については、SQL Server のマニュアルを参照してください。  
  
-   **グループ化された行を並べ替える** たとえば、都市とその都市の著者数が各行に記述されていて、多数の著者を含む都市が最初に表示される結果セットを作成できます。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
    ```  
  
    2 番目の並べ替えの基準にする列として、 `state` 列が指定されています。 したがって、著者の数が同じ州がある場合は、アルファベット順に表示されます。  
  
-   **各種言語のデータを使用して並べ替える** つまり、列の既定の規則とは異なる照合規則を使用して、列を並べ替えることができます。 たとえば、Jaime Patino の作品の全書名を取得するクエリを作成できます。 アルファベット順に書名を表示するには、書名列に対してスペイン語の照合規則を使用します。 結果の SQL ステートメントは次のようになります。  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>参照  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
