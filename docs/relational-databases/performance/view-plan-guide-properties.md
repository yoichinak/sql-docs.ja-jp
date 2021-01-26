---
title: プラン ガイド プロパティの表示 | Microsoft Docs
description: SQL Server Management Studio または Transact-SQL を使用し、SQL Server でプラン ガイドのプロパティを表示する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.planguideprop.general.f1
helpviewer_keywords:
- plan guides [SQL Server], view plan guide properties
- viewing plan guide properties
ms.assetid: 8c0d2f39-59c1-4168-a649-65473f6a771b
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 72b34306250bc24018c719f10700a29f4b7d6d0c
ms.sourcegitcommit: 108bc8e576a116b261c1cc8e4f55d0e0713d402c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2021
ms.locfileid: "98766480"
---
# <a name="view-plan-guide-properties"></a>プラン ガイド プロパティの表示
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のプラン ガイドのプロパティは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または  を使用して表示できます。 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **以下を使用してプラン ガイドのプロパティを表示するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 カタログ ビューでのメタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>プラン ガイドのプロパティを表示するには  
  
1.  プラス記号をクリックして、プロパティを表示するプラン ガイドのあるデータベースを展開し、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  プラス記号をクリックして **[プラン ガイド]** フォルダーを展開します。  
  
3.  プロパティを表示するプラン ガイドを右クリックし、 **[プロパティ]** を選択します。  
  
     **[プラン ガイドのプロパティ]** ダイアログ ボックスに次のプロパティが表示されます。  
  
     **[ヒント]**  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに適用されるクエリ ヒントまたはクエリ プランが表示されます。 クエリ プランがヒントとして指定されている場合は、そのプランの XML プラン表示出力が表示されます。  
  
     **[無効化]**  
     プラン ガイドの状態が表示されます。 指定できる値は、 **[True]** および **[False]** です。  
  
     **名前**  
     プラン ガイドの名前が表示されます。  
  
     **パラメーター**  
     スコープの種類が SQL または TEMPLATE の場合は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに埋め込まれているすべてのパラメーターの名前とデータ型が表示されます。  
  
     **[スコープ バッチ]**  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含むバッチ テキストが表示されます。  
  
     **[スコープ オブジェクト名]**  
     スコープの種類が OBJECT の場合は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含む [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ、ユーザー定義スカラー関数、複数ステートメントのテーブル値関数、または DML トリガーの名前が表示されます。  
  
     **[スコープ スキーマ名]**  
     スコープの種類が OBJECT の場合は、そのオブジェクトを含むスキーマの名前が表示されます。  
  
     **[スコープの種類]**  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含むエンティティの種類が表示されます。 これは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとプラン ガイドを照合するコンテキストを示します。 選択できる値は、 **OBJECT**、 **SQL**、および **TEMPLATE** です。  
  
     **ステートメント**  
     プラン ガイドの適用対象の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが表示されます。  
  
4.  **[OK]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>プラン ガイドのプロパティを表示するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- If a plan guide named "Guide1" already exists in the AdventureWorks2012 database, delete it.  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID(N'Guide1') IS NOT NULL  
       EXEC sp_control_plan_guide N'DROP', N'Guide1';  
    GO  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
    GO  
    -- Gets the name, created date, and all other relevant property information on the plan guide created above.   
    SELECT name AS plan_guide_name,  
       create_date,  
       query_text,  
       scope_type_desc,  
       OBJECT_NAME(scope_object_id) AS scope_object_name,  
       scope_batch,  
       parameters,  
       hints,  
       is_disabled  
    FROM sys.plan_guides  
    WHERE name = N'Guide1';  
    GO  
    ```  
  
 詳細については、「[sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)」を参照してください。  
  
  
