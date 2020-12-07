---
title: Transact-SQL スニペットの作成
description: Transact-SQL スニペットは、コード テンプレートです。 置換ポイントでコンテンツを挿入し、テンプレートに構文要素を追加することによって、その使用をカスタマイズする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f5e6f93c102c4f08d2f52e0359e77d2c450a74d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039113"
---
# <a name="complete-transact-sql-snippets"></a>Transact-SQL スニペットの作成
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] コード スニペットがスクリプトに挿入されると、スニペットのコンテンツを編集して [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを作成できます。  
  
## <a name="completing-snippets"></a>スニペットの作成  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] スニペットをスクリプトに追加した場合、挿入されたスニペット ステートメントには 1 つ以上の置換ポイントが含まれ、強調表示されます。 置換ポイント上にマウス ポインターを置くと、指定できる構文要素の説明を含むツールヒントが表示されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターは、ソース ファイルを閉じるまで、スニペットを周囲のスクリプトと区別します。 ソース ファイルを閉じるまで、置換ポイントはアクティブのままになります。  
  
 スニペットによって挿入されたテンプレート コードに追加の構文要素も追加できます。 たとえば、テーブルの作成スニペット テンプレートは、2 列の定義を生成します。3 列以上のテーブルを作成するには、列定義を追加する必要があります。  
  
#### <a name="completing-the-snippet-statement"></a>スニペット ステートメントの作成  
  
1.  1 つの置換ポイントから次の置換ポイントに移動するには、Tab キーを使用します。 前の置換ポイントに移動するには、Shift キーを押しながら Tab キーを押します。  
  
2.  IntelliSense を呼び出すには、Ctrl キーを押しながら Space キーを押します。  
  
3.  一覧からアイテムを選択するか、置換を入力します。  
  
## <a name="see-also"></a>参照  
 [Transact-SQL スニペットの挿入](./insert-transact-sql-snippets.md)   
 [ブロックの挿入 Transact-SQL スニペットの挿入](./insert-surround-with-transact-sql-snippets.md)  
  
