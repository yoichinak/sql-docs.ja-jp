---
description: ダイアグラムへのテーブルの追加 (Visual Database Tools)
title: ダイアグラムへのテーブルの追加
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
ms.assetid: 5440fdf7-ac04-4325-9f32-181f4cd402e5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 5aa8b90a1a6d3b03ec7a8c091d2f17cbb669823f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462932"
---
# <a name="add-tables-to-diagrams-visual-database-tools"></a>ダイアグラムへのテーブルの追加 (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

データベース ダイアグラムにテーブルを追加すると、そのテーブルの構造の編集や、ダイアグラム内にある他のテーブルとの関連付けを行えます。 テーブルを追加する方法には、ダイアグラムに既存のデータベース テーブルを追加する方法と、データベースで未定義の新しいテーブルを挿入する方法があります。
  
## <a name="to-insert-a-new-table-into-a-diagram"></a>ダイアグラムに新しいテーブルを挿入するには

1. テーブルを作成するデータベースに接続していることを確認します。

   現在のダイアグラムにテーブルを作成するには、ツール バーの **[新しいテーブル]** をクリックします。

   - または -  

   ダイアグラムを右クリックし、 **[新しいテーブル]** をクリックします。

2. **[名前の選択]** ダイアログ ボックスで、システムによって割り当てられたテーブル名を必要に応じて変更し、 **[OK]** をクリックします。

   ダイアグラムに新しいテーブルが [標準] ビューで表示されます。

3. 新しいテーブルの最初のセルに列名を入力します。 次に、Tab キーを押して次のセルに移動します。

4. **[データ型]** で列のデータ型を選択します。 各列には、名前とデータ型が必要です。

   テーブル デザイナーで列のその他のプロパティを設定できます。

5. テーブルに列を追加するたびに、手順 3. および手順 4. を繰り返します。

> [!NOTE]
> データベース ダイアグラムを保存すると、データベースに新しいテーブルが追加されます。

### <a name="to-add-an-existing-table-to-a-diagram"></a>ダイアグラムに既存のテーブルを追加するには

1. テーブルを編集するデータベースに接続していることを確認します。

2. **[テーブル]** フォルダーでテーブルを選択します。

3. データベース ダイアグラムにテーブルをドラッグします。

4. マウスのボタンを離します。

> [!NOTE]
> 選択したテーブルがダイアログの他のテーブルとの間にリレーションシップを持つ場合は、自動的にリレーションシップの線が引かれます。

### <a name="to-add-related-tables-to-a-diagram"></a>ダイアグラムに関連テーブルを追加するには  

1. データベース ダイアグラムで、外部キー制約を含む 1 つ以上のテーブルを選択します。  

2. 選択したテーブルの 1 つを右クリックし、 **[関連テーブルの追加]** をクリックします。  

> [!NOTE]
> 選択したテーブルから外部キー制約によって参照されるテーブルと、選択したテーブルを外部キー制約によって参照するテーブルの両方が、ダイアグラムに追加されます。  

## <a name="see-also"></a>参照

[データベース ダイアグラムの操作](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[データベース ダイアグラムでのテーブルの操作](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)
