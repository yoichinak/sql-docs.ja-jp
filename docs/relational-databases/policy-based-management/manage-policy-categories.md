---
description: ポリシー カテゴリの管理
title: ポリシー カテゴリの管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policycategories.f1
ms.assetid: d188a819-731f-4029-98aa-780d3299a0ce
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 26b15222f570304f321337a4b3574c3fa2f3b945
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88494013"
---
# <a name="manage-policy-categories"></a>ポリシー カテゴリの管理
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、カテゴリ内の使用可能な、いずれかまたはすべてのポリシーを [!INCLUDE[tsql](../../includes/tsql-md.md)]のインスタンス全体に適用する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **カテゴリ ポリシーを SQL Server インスタンスに適用するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]を使用している場合、 **[データベースのサブスクリプションの要求]** チェック ボックスがオフになっているときには、サーバーの関連部分 (1 つ以上のデータベースやテーブルなど) にポリシー カテゴリを個別に適用する必要があります。  
  
-   存在しないポリシー カテゴリを指定すると、新しいポリシー カテゴリが作成され、ストアド プロシージャの実行時にすべてのデータベースに対してサブスクリプションが要求されます。 新しいカテゴリに要求されたサブスクリプションをクリアすると、そのサブスクリプションは、 *target_object* で指定したデータベースにのみ適用されます。 要求されたサブスクリプションの設定を変更する方法の詳細については、「[sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)」を参照してください。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 このストアド プロシージャは、ストアド プロシージャの現在の所有者のコンテキストで実行されます。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>カテゴリ ポリシーを SQL Server インスタンスに適用するには  
  
1.  **オブジェクト エクスプ ローラー** で、プラス記号をクリックして、カテゴリ ポリシーを適用するサーバーを展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  **[ポリシー管理]** を右クリックし、 **[カテゴリの管理]** をクリックします。  
  
     **[ポリシー カテゴリの管理]** ダイアログ ボックスには、次の情報が表示されます。  
  
     **Name**  
     ポリシー カテゴリの名前です。  
  
     **[データベースのサブスクリプションの要求]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのすべてのデータベースに、ポリシー カテゴリ内のポリシーを強制的に適用します。  
  
4.  ポリシー カテゴリを SQL Server インスタンスに適用するために、 **[データベースのサブスクリプションの要求]** の下のいずれかまたはすべてのチェック ボックスをオンまたはオフにします。  
  
5.  完了したら、 **[OK]** をクリックします。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>カテゴリ ポリシーを SQL Server インスタンスに適用するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb;  
    GO  
    -- configures the specified database to subscribe to a policy category that is named 'Table Naming Policies'.  
    EXEC dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
    , @target_object = N'AdventureWorks2012'  
    , @policy_category = N'Table Naming Policies';  
    GO  
    ```  
  
 詳細については、「[sp_syspolicy_add_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)」を参照してください。  
  
  
