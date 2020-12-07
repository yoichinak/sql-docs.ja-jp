---
title: Transact-SQL スニペットの挿入
description: データベース エンジン クエリ エディターで新しい Transact-SQL ステートメントを作成する際の開始点として使用できる Transact-SQL コード スニペットを選択、挿入、および変更する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], snippets
- Transact-SQL snippets, code
- snippets [Transact-SQL], how to insert
ms.assetid: d66c96f4-2e84-4d79-9bfd-3635fdd98425
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2998121fff0be71019539a9e40da5a06bbf9133a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039024"
---
# <a name="insert-transact-sql-snippets"></a>Transact-SQL スニペットの挿入
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] コード スニペットは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディターで [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントを新規作成するときの開始位置として使用できるテンプレートです。  
  
## <a name="inserting-snippets"></a>スニペットの挿入  
 **[スニペットの挿入]** メニューを使用して、スニペットのカテゴリ別一覧からスニペットを選択できます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] スニペットには、置換ポイント (そのポイントに関連する構文を示すテキスト) が含まれています。 たとえば、CREATE TABLE スニペットには、テーブル名、列名、列のデータ型などの要素の置換ポイントが含まれます。 このスニペットを挿入した後は、置換テキストを変更して、有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントにする必要があります。 詳細については、「 [Transact-SQL スニペットの作成](./complete-transact-sql-snippets.md)」を参照してください。  
  
#### <a name="inserting-a-snippet-by-using-the-insert-snippet-menu"></a>[スニペットの挿入] メニューを使用したスニペットの挿入  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウで、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スニペットを挿入する位置にカーソルを置きます。  
  
2.  次の 3 つのうちいずれかの方法でスニペット ピッカーのヒントを起動します。  
  
    -   Ctrl キーを押しながら K キーを押し、Ctrl キーを押しながら X キーを押す。  
  
    -   **[編集]** メニューの **[IntelliSense]** をポイントし、 **[スニペットの挿入]** をクリックする。  
  
    -   右クリックし、ショートカット メニューの **[スニペットの挿入]** をクリックする。  
  
3.  スニペットをダブルクリックするか、スニペット ピッカーからスニペットを選択して、Tab キーまたは Enter キーを押します。  
  
## <a name="see-also"></a>参照  
 [ブロックの挿入 Transact-SQL スニペットの挿入](./insert-surround-with-transact-sql-snippets.md)  
  
