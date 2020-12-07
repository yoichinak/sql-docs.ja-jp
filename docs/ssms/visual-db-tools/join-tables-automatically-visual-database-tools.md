---
description: テーブルの自動結合 (Visual Database Tools)
title: テーブルの自動結合
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 3efc96cafe9a7759834591473007dd3818b16e25
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462800"
---
# <a name="join-tables-automatically-visual-database-tools"></a>テーブルの自動結合 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 クエリに複数のテーブルを追加すると、[クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)により、これらのテーブルが相互に関連しているかどうかの確認が行われます。 関連している場合は、テーブルまたはテーブル構造オブジェクトを示す四角形の間に、結合線が自動的に表示されます。  
  
クエリおよびビュー デザイナーでは、次の場合にテーブルの結合が認識されます。  
  
-   データベースにテーブルの関連を指定する情報がある場合。  
  
-   各テーブルの 1 つの列が、それぞれ同じ名前および同じデータ型を持っている場合。 少なくとも一方のテーブルの列は、主キーである必要があります。 たとえば、 `employee` テーブルおよび `jobs` テーブルを追加し、 `job_id` テーブルに `jobs` 列という主キーがあり、それぞれのテーブルに同じデータ型の `job_id` という列がある場合、これらのテーブルは自動的に結合されます。  
  
    > [!NOTE]  
    > クエリおよびビュー デザイナーでは、同じ名前および同じデータ型の列の間で結合が 1 つだけ作成されます。 複数の結合が作成できる場合でも、クエリおよびビュー デザイナーは、最初に検出された一致列から結合を 1 つだけ作成します。  
  
-   検索条件 (WHERE 句) が、実際には結合条件であると検出された場合。 たとえば、 `employee` テーブルおよび `jobs`テーブルを追加し、両方のテーブルの `job_id` 列の値が一致する行を検索する検索条件を作成する場合があります。 その場合、検索条件が結合になることが検出され、検索条件に基づいて結合条件が作成されます。  
  
クエリおよびビュー デザイナーによって作成された結合がクエリに適していない場合、結合の変更または削除を行うことができます。 詳しくは、「[結合演算子の変更 (Visual Database Tools)](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md)」および「[結合の削除 (Visual Database Tools)](../../ssms/visual-db-tools/remove-joins-visual-database-tools.md)」をご覧ください。  
  
クエリでテーブルが自動的に結合されない場合は、結合を手動で作成できます。 詳しくは、「[手動でのテーブルの結合 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[クエリおよびビュー デザイナーでの結合の表示方法 (Visual Database Tools)](../../ssms/visual-db-tools/how-the-query-and-view-designer-represents-joins-visual-database-tools.md)  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[結合を使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
