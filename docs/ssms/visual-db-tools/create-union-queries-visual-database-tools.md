---
description: UNION クエリの作成 (Visual Database Tools)
title: UNION クエリの作成
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b6d4d7618b3130e2b06d3efb8e9e2a35bc7ca0ee
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038375"
---
# <a name="create-union-queries-visual-database-tools"></a>UNION クエリの作成 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
UNION キーワードを使用すると、2 つの SELECT ステートメントの結果を、1 つのテーブルに表示できます。 いずれかの SELECT ステートメントから返された行がすべて組み合わされて、UNION 式の結果として表示されます。 例については、「 [SELECT の例 (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
> ダイアグラム ペインに表示できるのは、1 つの SELECT 句だけです。 したがって、UNION クエリを使用している場合、クエリ デザイナーにはテーブル操作ペインは表示されません。  
  
### <a name="to-create-a-merged-select-query"></a>マージされた選択クエリを作成するには  
  
1.  クエリを開くか、新規作成します。  
  
2.  SQL ペインに有効な UNION 式を入力します。  
  
    次の例は、有効な UNION 式です。  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  **[クエリ デザイナー]** メニューの **[SQL の実行]** をクリックして、クエリを実行します。  
  
    UNION クエリがクエリ デザイナーによって書式化されます。  
  
## <a name="see-also"></a>関連項目  
[サポートされるクエリの種類](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[クエリに関する基本操作の実行](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](../../t-sql/language-elements/set-operators-union-transact-sql.md)