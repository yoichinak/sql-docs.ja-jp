---
title: サーバー監査およびデータベース監査の仕様を作成する
description: SQL Server Management Studio または Transact-SQL (T-SQL) を使用して SQL Server の監査とデータベース監査の仕様を作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d015a1adf0bdd5e5f47b49a8dabb6783b8538b7e
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250084"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>サーバー監査およびデータベース監査の仕様を作成する
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  この記事では、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] でサーバー監査とデータベース監査の仕様を作成する方法について説明します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスや [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースの監査では、システムで発生するイベントを追跡およびログ記録する必要があります。 *SQL Server Audit* オブジェクトは、監視するサーバーレベルまたはデータベースレベルのアクションおよびアクション グループの単一のインスタンスを収集します。 監査は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス レベルで行われます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスごとに複数の監査を使用できます。 " *データベース レベルの監査の仕様* " オブジェクトも、監査に属しています。 各監査では、SQL Server データベースごとに 1 つのデータベース監査の仕様を作成できます。 詳細については、「[SQL Server Audit &#40;データベース エンジン&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
 ##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめる前に  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
 データベース監査仕様は、セキュリティ保護できないオブジェクトであり、特定のデータベースに保存されます。 データベース監査の仕様は、作成した時点では無効の状態です。  
  
 ユーザー データベース内のデータベース監査の仕様を作成または変更する場合、システム ビューなどのサーバー スコープ オブジェクトの監査アクションを含めないでください。 サーバー スコープ オブジェクトが含まれている場合、監査が作成されます。 ただし、サーバー スコープ オブジェクトは含まれず、エラーは返されません。 サーバー スコープ オブジェクトを監査するには、マスター データベース内のデータベース監査の仕様を使用します。  
  
 **TempDB** システム データベースを除いて、データベース監査の仕様は、それが作成されたデータベース内にあります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
  
-   ALTER ANY DATABASE AUDIT 権限を持つユーザーは、データベース監査の仕様を作成し、任意の監査にバインドできます。  
  
-   データベース監査の仕様が作成されると、CONTROL SERVER 権限または ALTER ANY DATABASE AUDIT 権限を持つプリンシパルはそれを表示できます。 sysadmin アカウントでも表示できます。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-server-audit"></a>サーバー監査を作成するには  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ]** フォルダーを展開します。  
  
2.  **Audits** フォルダーを右クリックし、 **[新しい監査]** を選択します。 詳細については、「[サーバー監査およびサーバー監査の仕様を作成する方法](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)」を参照してください。  
  
3.  オプションの選択が完了したら、 **[OK]** を選択します。  

#### <a name="to-create-a-database-level-audit-specification"></a>データベース レベルの監査仕様を作成するには  
  
1.  オブジェクト エクスプローラーで、監査の仕様を作成するデータベースを展開します。  
  
2.  **[セキュリティ]** フォルダーを展開します。  
  
3.  **Database Audit Specifications** フォルダーを右クリックして、 **[新しいデータベース監査の仕様]** を選択します。  
  
     **[データベース監査の仕様の作成]** ダイアログ ボックスでは、次のオプションを使用できます。  
  
     **名前**  
     データベース監査の仕様の名前。 サーバー監査の使用を作成する場合、名前は自動的に生成されます。 名前は編集できます。  
  
     **監査**  
     既存のサーバー監査オブジェクトの名前。 監査の名前を入力するか、一覧から選択します。  
  
     **[監査アクションの種類]**  
     キャプチャするデータベース レベルの監査アクション グループと監査アクションを指定します。 データベース レベルの監査アクション グループと監査アクションの一覧、およびそれらに含まれるイベントの説明については、「[SQL Server 監査のアクション グループとアクション](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)」を参照してください。  
  
     **[オブジェクト スキーマ]**  
     指定した **[オブジェクト名]** のスキーマを表示します。  
  
     **[オブジェクト名]**  
     監査するオブジェクトの名前。 このオプションは、監査アクションに対してのみ使用できます。 これは、監査グループには適用されません。  
  
     **省略記号 (...)**  
     **[オブジェクトの選択]** ダイアログ ボックスが開いて、指定した **[監査アクションの種類]** に基づいて、使用可能なオブジェクトを参照して選択することができます。  
  
     **[プリンシパル名]**  
     監査対象のオブジェクトで監査をフィルター選択するためのアカウント。  
  
     **省略記号 (...)**  
     **[オブジェクトの選択]** ダイアログ ボックスが開いて、指定した **[オブジェクト名]** に基づいて、使用可能なオブジェクトを参照して選択することができます。  
  
4.  オプションの選択が完了したら、 **[OK]** を選択します。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-server-audit"></a>サーバー監査を作成するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  標準バーで、 **[新しいクエリ]** を選択します。  
  
3.  次の例をクエリ ウィンドウに貼り付けて、 **[実行]** を選択します。  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>データベース レベルの監査仕様を作成するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  標準バーで、 **[新しいクエリ]** を選択します。  
  
3.  次の例をクエリ ウィンドウに貼り付けて、 **[実行]** を選択します。 この例では、`Audit_Pay_Tables`という名前のデータベース監査の仕様を作成します。 これは、前のセクションで定義したサーバー監査に基づき、`HumanResources.EmployeePayHistory` テーブルについて、`dbo` ユーザーによる SELECT ステートメントと INSERT ステートメントを監査します。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 詳細については、「[CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)」と「[CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)」を参照してください。  
  
  
