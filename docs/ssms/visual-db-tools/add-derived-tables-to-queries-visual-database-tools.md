---
description: クエリへの派生テーブルの追加 (Visual Database Tools)
title: クエリへの派生テーブルの追加
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [Visual Database Tools]
- joins [SQL Server], derived tables
- table joins [SQL Server]
- derived tables
ms.assetid: 05f1ba1d-465f-4e36-84bb-21b963c9b8f9
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: ec4389810e09af78f61e99762dbb30862919f1d1
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037192"
---
# <a name="add-derived-tables-to-queries-visual-database-tools"></a>クエリへの派生テーブルの追加 (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
派生テーブルは、クエリのソース テーブルとして使用される結果セットです。 **ダイアグラム ペイン**でクエリに派生テーブルを追加できます。  
  
### <a name="to-add-a-derived-table-to-a-query"></a>クエリに派生テーブルを追加するには  
  
1.  既存のクエリを開くか、新しいクエリを作成します。  
  
2.  **ダイアグラム ペイン** を右クリックし、 **[派生した新しいテーブルの追加]** を選択します。  
  
    derivedtbl_*N* という名前で新しいテーブルが追加され、派生テーブルの SELECT ステートメントがクエリの FROM 句に追加されます。  
  
## <a name="see-also"></a>参照  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[クエリの作成 (Visual Database Tools)](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[クエリを開く (Visual Database Tools)](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)  
[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
