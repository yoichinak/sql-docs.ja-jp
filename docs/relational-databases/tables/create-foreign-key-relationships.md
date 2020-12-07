---
description: 外部キーのリレーションシップの作成
title: 外部キーのリレーションシップの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea3a7bec04dcd7e584d541cf4fa4ccee3cf48915
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645847"
---
# <a name="create-foreign-key-relationships"></a>外部キーのリレーションシップの作成


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

この記事では、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で外部キーのリレーションシップを作成する方法について説明します。 あるテーブルの行と他のテーブルの行を関連付ける場合は、2 つのテーブル間にリレーションシップを作成します。

## <a name="permissions"></a>アクセス許可

外部キーが設定された、新しいテーブルを作成するには、データベースの [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 権限と、テーブルを作成するスキーマの [ALTER](../../t-sql/statements/alter-schema-transact-sql.md) 権限が必要です。

既存のテーブルに外部キーを作成するには、テーブルに対する [ALTER](../../t-sql/statements/alter-table-transact-sql.md) 権限が必要です。

## <a name="limits-and-restrictions"></a><a name="BeforeYouBegin"></a>制限事項と制約事項

- 外部キー制約は、別のテーブルの主キー制約にのみリンクする必要はありません。 外部キーは、別のテーブルの UNIQUE 制約の列を参照するように定義することもできます。
- FOREIGN KEY 制約の列に NULL 以外の値を入力するときは、その値が参照される列に存在している必要があります。 それ以外の場合、外部キー違反のエラー メッセージが返されます。 複合外部キー制約のすべての値が検証されるようにするには、参加しているすべての列に NOT NULL を指定します。
- FOREIGN KEY 制約は、同じサーバー上の同じデータベース内のテーブルのみを参照できます。 複数のデータベースにまたがる参照整合性は、トリガーを使って実装する必要があります。 詳細については、[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) に関するページをご覧ください。
- FOREIGN KEY 制約は、同じテーブル内の他の列を参照でき、自己参照として参照されます。
- 列レベルで指定された FOREIGN KEY 制約は、参照列を 1 つだけ表示できます。 この参照列は、制約が定義されている列と同じデータ型である必要があります。
- テーブルレベルで指定された FOREIGN KEY 制約は、制約列リスト内の列の数と同じ数の参照列を持っている必要があります。 また、各参照列のデータ型は、列リスト内の、参照列に対応する列と同じでなければなりません。
- [!INCLUDE[ssDE](../../includes/ssde-md.md)] には、他のテーブルを参照するテーブルに含めることができる FOREIGN KEY 制約の数に対して定義済みの制限はありません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、特定のテーブルを参照する他のテーブルが所有する FOREIGN KEY 制約の数も制限されません。 ただし、使用できる FOREIGN KEY 制約の実際の数は、ハードウェア構成やデータベースおよびアプリケーションのデザインにより制限されます。 テーブルから、他のテーブルと列を最大 253 個まで外部キーとして参照 (発信参照) することができます。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、1 つのテーブル内の列を参照 (着信参照) できる他のテーブルと列の数が 253 から 10,000 までに限られています。 (少なくとも 130 の互換性レベルが必要です)。増加には、次の制限があります。

  - 253 を超える外部キー参照は、DELETE と UPDATE DML 操作でのみサポートされています。 MERGE 操作はサポートされません。
  - テーブル自体に対する外部キー参照も、253 の外部キー参照に制限されます。
  - 現在、253 を超える外部キー参照は、列ストア インデックス、メモリ最適化テーブル、Stretch Database、では使用できません。

- FOREIGN KEY 制約は一時テーブルには設定されません。
- CLR ユーザー定義型の列に対して外部キーを定義する場合は、型の実装でバイナリ順がサポートされている必要があります。 詳細については、「 [CLR ユーザー定義型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」を参照してください。
- **varchar(max)** 型の列は、その列が参照する主キーも **varchar(max)** 型として定義されている場合にのみ FOREIGN KEY 制約で使用できます。

## <a name="create-a-foreign-key-relationship-in-table-designer"></a>テーブル デザイナーで外部キー リレーションシップを作成する

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio を使用する

1. オブジェクト エクスプローラーで、リレーションシップの外部キー側となるテーブルを右クリックして、 **[デザイン]** をクリックします。

   [ **[テーブル デザイナー]** ](../../ssms/visual-db-tools/design-tables-visual-database-tools.md) にテーブルが表示されます。
2. **[テーブル デザイナー]** メニューの **[リレーションシップ]** をクリックします。
3. **[外部キーのリレーションシップ]** ダイアログ ボックスで、 **[追加]** をクリックします。

   リレーションシップが **[選択されたリレーションシップ]** ボックスに表示されます。このリレーションシップには、FK_\<*tablename*>_\<*tablename*> (*tablename* は外部キー テーブルの名前) という形式の名前が自動的に割り当てられます。
4. **[選択されたリレーションシップ]** ボックスの一覧で、リレーションシップをクリックします。
5. 右側のグリッドの **[テーブルと列の指定]** をクリックし、その右側にある省略記号 ( **[...]** ) をクリックします。
6. **[テーブルと列]** ダイアログ ボックスの **[主キー]** ボックスの一覧で、リレーションシップの主キー側となるテーブルをクリックします。
7. 下のグリッドで、テーブルの主キーになる列を選択します。 各列の右横のグリッド セルで、外部キー テーブルの対応する外部キー列を選択します。

   リレーションシップの名前は、**テーブル デザイナー** によって割り当てられます。 この名前を変更するには、 **[リレーションシップ名]** ボックスの内容を編集します。
8. **[OK]** をクリックしてリレーションシップを作成します。
9. テーブル デザイナー ウィンドウを閉じ、変更を **[保存]** して外部キー リレーションシップの変更を有効にします。

## <a name="create-a-foreign-key-in-a-new-table"></a>新しいテーブルに外部キーを作成する

### <a name="using-transact-sql"></a>Transact-SQL の使用

次の例では、AdventureWorks データベース内で、テーブルを作成し、`Sales.SalesReason` テーブル内の `SalesReasonID` 列を参照する外部キー制約を `TempID` 列に定義します。 ON DELETE CASCADE 句および ON UPDATE CASCADE 句を使用することによって、`Sales.SalesReason` テーブルに対する変更が自動的に `Sales.TempSalesReason` テーブルにも反映されるようにしています。    

```sql
CREATE TABLE Sales.TempSalesReason 
   (
      TempID int NOT NULL, Name nvarchar(50)
      , CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID)
      , CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)
        REFERENCES Sales.SalesReason (SalesReasonID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
   )
;
```

## <a name="create-a-foreign-key-in-an-existing-table"></a>既存のテーブルに外部キーを作成する

### <a name="using-transact-sql"></a>Transact-SQL の使用
次の例では、AdventureWorks データベース内で、`TempID` 列に外部キーを作成し、`Sales.SalesReason` テーブルの `SalesReasonID` 列を参照します。

```sql
ALTER TABLE Sales.TempSalesReason
   ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)
      REFERENCES Sales.SalesReason (SalesReasonID)
      ON DELETE CASCADE
      ON UPDATE CASCADE
;
```

## <a name="next-steps"></a>次のステップ

詳細については、次を参照してください。

- [主キー制約と外部キー制約](primary-and-foreign-key-constraints.md)
- [GRANT (データベース アクセス許可の許可)](../../t-sql/statements/grant-database-permissions-transact-sql.md)
- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)。
