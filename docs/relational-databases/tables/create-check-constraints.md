---
description: CHECK 制約の作成
title: CHECK 制約の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 177caf959cd9f957525dd50a0b63a0dc2b304115
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128765"
---
# <a name="create-check-constraints"></a>CHECK 制約の作成
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してテーブルで CHECK 制約を作成して、1 つ以上の列に入力できるデータ値を指定します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **新しい CHECK 制約を作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-new-check-constraint"></a>新しい CHECK 制約を作成するには  
  
1.  **オブジェクト エクスプローラー** で、CHECK 制約を追加するテーブルを展開し、 **[制約]** を右クリックして、 **[新しい制約]** をクリックします。  
  
2.  **[CHECK 制約]** ダイアログ ボックスで、**[式]** フィールドをクリックして、省略記号 **[...]** をクリックします。  
  
3.  **[CHECK 制約式]** ダイアログ ボックスで、CHECK 制約の SQL 式を入力します。 たとえば、 `SellEndDate` テーブルの `Product` 列への入力を `SellStartDate` 列の日付と同じか、それよりも後の日付の値または NULL 値に限定するには、次のように入力します。  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     また、 `zip` 列への入力を 5 桁の数値に限定するには、次のように入力します。  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  数値以外の制約値は、必ず単一引用符 (') で囲んでください。  
  
4.  **[OK]** をクリックします。  
  
5.  **[ID]** カテゴリでは、CHECK 制約の名前を変更し、制約の説明 (拡張プロパティ) を追加できます。  
  
6.  **テーブル デザイナー** のカテゴリでは、制約が適用されるタイミングを設定できます。  
  
    |**次のように** 変更します。|**[はい] を選択するフィールド:**|  
    |-------------|---------------------------------------------|  
    |制約を作成する前に既に存在していたデータで制約をテストする|**[作成または有効化するときに既存データを確認]**|  
    |このテーブルでレプリケーション操作が発生するたびに制約を適用する|**[レプリケーションに対して適用]**|  
    |このテーブルの行を挿入または更新するたびに制約を適用する|**[INSERT および UPDATE に適用]**|  
  
7.  **[閉じる]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-new-check-constraint"></a>新しい CHECK 制約を作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>  
