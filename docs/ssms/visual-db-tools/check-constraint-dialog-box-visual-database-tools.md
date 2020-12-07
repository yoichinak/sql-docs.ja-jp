---
description: '[制約のチェック] ダイアログ ボックス (Visual Database Tools)'
title: '[制約式の確認] ダイアログ ボックス'
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: b37e339dc13577bd30491f1c155ebb8114868d60
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038954"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>[制約のチェック] ダイアログ ボックス (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

 このダイアログ ボックスは、テーブル デザイナーのテーブル定義グリッドを右クリックし、**[制約のチェック]** をクリックすると表示されます。 このダイアログ ボックスには、データベースのテーブルに関連付けられた、一意でない制約のプロパティ セットが含まれています。 UNIQUE 制約に適用されるプロパティは、 **[インデックス/キー]** ダイアログ ボックスに表示されます。  
  
> [!NOTE]  
> テーブルをレプリケーションのためにパブリッシュする場合は、Transact-SQL ステートメントの [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) または SQL Server 管理オブジェクト (SMO) を使用してスキーマを変更する必要があります。 テーブル デザイナーまたはデータベース ダイアグラム デザイナーを使用してスキーマを変更するとき、テーブルはいったん削除されてから再作成されます。 パブリッシュされたオブジェクトは削除できないので、スキーマの変更は失敗します。  
  
## <a name="options"></a>オプション

**[選択された制約のチェック]**  
使用できる CHECK 制約を一覧表示します。 制約のプロパティを表示するには、一覧の中から選択します。  
  
**追加**  
選択したデータベース テーブルの制約を新しく作成し、その制約に既定の名前と他の値を割り当てます。 制約は、その制約用の式を入力するまで、有効にできません。  
  
**削除**  
選択した制約をテーブルから削除します。 追加した CHECK 制約を取り消すには、このボタンを使用して制約を削除します。  
  
**[全般] カテゴリ**  
展開して **[式]** のプロパティ フィールドを表示します。  
  
**[式]**  
選択した CHECK 制約の式を表示します。 新しい制約の場合は、このボックスを終了する前に式を入力する必要があります。 既存の CHECK 制約を編集することもできます。 詳細については、[制約の使用](../../relational-databases/tables/unique-constraints-and-check-constraints.md)に関するページを参照してください。  
  
**[IDENTITY] カテゴリ**  
展開して **[名前]** と **[説明]** のプロパティを表示します。  
  
**名前**  
選択した CHECK 制約の名前を表示します。 この制約の名前を変更するには、プロパティ フィールドに直接テキストを入力します。  
  
**説明**  
この CHECK 制約の説明を記述します。 プロパティ フィールドに入力することで説明を編集できます。またプロパティ フィールドの右側に表示されている省略記号ボタン ( **[...]** ) をクリックすると、**[説明のプロパティ]** ダイアログ ボックスで説明を編集できます。  
  
**[テーブル デザイナー] カテゴリ**  
展開して **[作成時または再度有効化するときに既存データを確認]**、 **[INSERTs および UPDATEs に適用]**、および **[レプリケーションに対して適用]** の各プロパティを表示します。  
  
**Check Existing Data On Creation or Re-Enabling**  
既存のすべてのデータ (制約を作成する前からテーブルに存在しているデータ) を制約で検証するかどうかを指定します。  
  
**[INSERTs および UPDATEs に適用]**  
テーブルにデータを挿入するときやテーブルのデータを更新するときに、制約を適用するかどうかを指定します。  
  
**[レプリケーションに対して適用]**  
レプリケーション エージェントがこのテーブルに対して挿入または更新を行うときに制約を適用するかどうかを示します。  
  
## <a name="see-also"></a>参照

[[制約の使用]](../../relational-databases/tables/unique-constraints-and-check-constraints.md)
[[インデックス/キー] ダイアログ ボックス &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/indexes-keys-dialog-box-visual-database-tools.md)