---
title: プラン ガイドの有効化または無効化 | Microsoft Docs
description: SQL Server Management Studio または Transact-SQL を使用し、プラン ガイドを無効または有効にする方法について説明します。 データベース内の 1 つまたはすべてのプラン ガイドを無効または有効にします。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: e6fd86e44411fafef9e70e8981d0fa8728af9e76
ms.sourcegitcommit: 04d101fa6a85618b8bc56c68b9c006b12147dbb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2021
ms.locfileid: "99048957"
---
# <a name="enable-or-disable-a-plan-guide"></a>プラン ガイドの有効化または無効化
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、プラン ガイドを無効化および有効化できます。 データベース内の 1 つのプラン ガイドまたはすべてのプラン ガイドを有効化または無効化できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **プラン ガイドの無効化または有効化に使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   有効、無効にする場合のどちらでも、そのプラン ガイドで参照されている関数、ストアド プロシージャ、または DML トリガーを削除または変更しようとすると、エラーが発生します。 上記のいずれかのオブジェクトの削除または変更の前に、常に依存関係を確認してください。  
  
-   無効なプラン ガイドを無効にする場合や、有効なプラン ガイドを有効にする場合は影響は生じず、エラーなしで実行できます。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 OBJECT プラン ガイドの無効化または有効化には、プラン ガイドによって参照されるオブジェクト (関数、ストアド プロシージャなど) に対する ALTER 権限が必要です。 その他すべてのプラン ガイドでは、ALTER DATABASE 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>プラン ガイドを無効化または有効化するには  
  
1.  プラス記号をクリックして、無効化または有効化するプラン ガイドのあるデータベースを展開し、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  プラス記号をクリックして **[プラン ガイド]** フォルダーを展開します。  
  
3.  無効化または有効化するプラン ガイドを右クリックし、 **[無効化]** または **[有効化]** を選択します。  
  
4.  **[プラン ガイドの無効化]** または **[プラン ガイドの有効化]** ダイアログ ボックスで、選択した動作が成功したことを確認し、 **[閉じる]** をクリックします。  

#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>データベース内のすべてのプラン ガイドを無効化または有効化するには  
  
1.  プラス記号をクリックして、無効化または有効化するプラン ガイドのあるデータベースを展開し、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  **[プラン ガイド]** フォルダーを右クリックし、 **[すべて有効化]** または **[すべて無効化]** を選択します。  
  
3.  **[すべてのプラン ガイドを無効化]** または **[すべてのプラン ガイドを有効化]** ダイアログ ボックスで、選択した動作が成功したことを確認し、 **[閉じる]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>プラン ガイドを無効化または有効化するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>データベース内のすべてのプラン ガイドを無効化または有効化するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 詳細については、「[sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)」を参照してください。  
  
  
