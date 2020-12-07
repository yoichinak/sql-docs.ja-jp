---
title: ブロックの挿入 Transact-SQL スニペットの挿入
description: コード ブロックにステートメントを配置するための開始点として機能する、ブロックの挿入スニペットを挿入する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- snippets [Transact-SQL], surround with
- IntelliSense [SQL Server], surround with snippets
- Transact-SQL snippets, surround with
ms.assetid: 5b5a8c6c-968e-4361-a7f5-9e2ac186d927
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7596e6ef216682ad66695b30712b3e77e2aa5ab
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038997"
---
# <a name="insert-surround-with-transact-sql-snippets"></a>ブロックの挿入 Transact-SQL スニペットの挿入
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  ブロックの挿入スニペットは、BEGIN、IF、または WHILE ブロックで一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを囲むときに出発点として使用できるテンプレートです。  
  
## <a name="inserting-surround-with-snippets"></a>ブロックの挿入スニペットの挿入  
 ブロックの挿入スニペットは、ショートカット キー、 **[編集]** メニュー、およびショートカット メニューの 3 とおりの方法で起動できます。  
  
 このスニペットを挿入した後は、置換テキストを変更して、有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントにする必要があります。 詳細については、「 [Transact-SQL スニペットの作成](./complete-transact-sql-snippets.md)」を参照してください。  
  
#### <a name="to-insert-a-surround-with-snippet"></a>ブロックの挿入スニペットを挿入するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウで、ブロックに含める一連のステートメントを選択します。  
  
2.  次の 3 つの方法のいずれかを使用して、ブロックの挿入スニペットの一覧を表示します。  
  
    -   Ctrl キーを押しながら K キーを押し、Ctrl キーを押しながら S キーを押す。  
  
    -   **[編集]** メニューの **[IntelliSense]** をポイントして、 **[ブロックの挿入]** をクリックする。  
  
    -   選択したテキストを右クリックし、ショートカット メニューの **[ブロックの挿入]** をクリックする。  
  
3.  マウスを使用するか、スニペットの名前を入力し、Tab キーまたは Enter キーを押して、一覧からスニペットの名前 (BEGIN、IF、または WHILE) を選択します。  
  
## <a name="see-also"></a>参照  
 [Transact-SQL スニペットの挿入](./insert-transact-sql-snippets.md)  
  
