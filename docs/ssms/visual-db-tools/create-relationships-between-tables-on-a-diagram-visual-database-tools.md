---
description: ダイアグラムでテーブル間のリレーションシップを作成する方法 (Visual Database Tools)
title: ダイアグラムでテーブル間のリレーションシップを作成する
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 0b758a04f81dffc31844af91933a544960f6ba2d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037530"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>ダイアグラムでテーブル間のリレーションシップを作成する方法 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
ダイアグラム デザイナーでは、テーブル間で列をドラッグすることにより、異なるテーブルの列の間にリレーションシップを作成できます。  
  
### <a name="to-create-a-relationship-graphically"></a>リレーションシップをグラフィカルに作成するには  
  
1.  データベース デザイナーで、別のテーブル内の列に関連付ける 1 つ以上のデータベース列の行セレクターをクリックします。  
  
2.  選択した列を関連テーブルにドラッグします。  
  
3.  **[外部キーのリレーションシップ]** ダイアログ ボックスと **[テーブルと列]** ダイアログ ボックスが表示されます。後者のダイアログ ボックスが手前に表示されます。  
  
4.  **[リレーションシップ名]** には、FK_*localtable*\_*foreigntable* という形式の名前が表示されます。 この値は変更できます。  
  
5.  **[主キー テーブル]** に適切なテーブルが指定されていることを確認します。  
  
6.  グリッドには、ローカル列とそれに対応する外部列が表示されます。 テーブル列の追加や削除またはマッピングの変更が可能です。  
  
7.  **[OK]** を選びます。  
  
    **[外部キーのリレーションシップ]** ダイアログ ボックスが表示されます。 **[選択されたリレーションシップ]** には、作成したリレーションシップが表示されます。  
  
8.  グリッド内のリレーションシップのプロパティを変更します。  
  
9. **[OK]** をクリックしてリレーションシップを作成します。  
  
    データベース デザイナーでは、選択した列間のリレーションシップが表示されます。  
  
## <a name="see-also"></a>参照  
[[テーブルと列] ダイアログ ボックス (Visual Database Tools)](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[制約の使用](../../relational-databases/tables/unique-constraints-and-check-constraints.md)  
[データベース ダイアグラムでのテーブルの使用 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
