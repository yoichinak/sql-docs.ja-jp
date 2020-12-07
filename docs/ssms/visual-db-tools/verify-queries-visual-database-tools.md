---
description: クエリの検査 (Visual Database Tools)
title: クエリの検査
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 944d34dbbec6da87d4f3ebd7920d9acd2ad162c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417728"
---
# <a name="verify-queries-visual-database-tools"></a>クエリの検査 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
問題を回避するために、作成したクエリを検証して、構文が正しいことを確認できます。 このオプションは、 [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)にステートメントを入力する場合に特に便利です。  
  
次に、クエリの検査について注意が必要な点を挙げます。  
  
-   **ダイアグラム ペイン** および **抽出条件ペイン**に表示できない場合でも、有効なステートメントは正しく検査されます。  
  
-   SQL 検査では SQL エラーのすべてが検出されるわけではありません。 SQL 検査で検出されないエラーがクエリにある場合は、クエリを実行するときに、データベースによってエラーが検出されます。  
  
-   パラメーターを含むクエリは検査できません。  
  
### <a name="to-verify-an-sql-statement"></a>SQL ステートメントを検査するには  
  
-   **SQL ペイン**を右クリックし、ショートカット メニューの **[SQL 構文の確認]** を選択します。  
  
## <a name="see-also"></a>参照  
[クエリの実行 (Visual Database Tools)](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[クエリに関する基本操作の実行 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
