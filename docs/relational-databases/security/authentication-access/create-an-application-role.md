---
title: アプリケーション ロールの作成 | Microsoft Docs
description: SQL Server Management Studio または Transact-SQL を使用して SQL Server でアプリケーション ロールを作成し、アプリケーションを使用した場合を除いてデータベースへのアクセスを制限します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.approle.general.f1
helpviewer_keywords:
- application roles [SQL Server], creating
ms.assetid: 6b8da1f5-3d8e-4f88-b111-b915788b06f1
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b9d77743864b3b5425379ec7b5c570629b470e04
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250752"
---
# <a name="create-an-application-role"></a>アプリケーション ロールの作成
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  このトピックでは、 [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]でアプリケーション ロールを作成する方法について説明します。 アプリケーション ロールは、特定のアプリケーションを使用する場合を除き、データベースへのユーザー アクセスを制限します。 アプリケーション ロールにはユーザーが含まれないため、 **[アプリケーション ロール]** が選択されている場合には、 **[ロール メンバー]** の一覧は表示されません。  
  
> [!IMPORTANT]  
>  アプリケーション ロールのパスワードを設定するときには、パスワードの複雑性が確認されます。 アプリケーション ロールを呼び出すアプリケーションは、これらのパスワードを格納する必要があります。 アプリケーション ロールのパスワードは常に暗号化して保存する必要があります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **アプリケーション ロールを作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 データベースに対する ALTER ANY APPLICATION ROLE 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
##### <a name="to-create-an-application-role"></a>アプリケーション ロールを作成するには  
  
1.  オブジェクト エクスプローラーで、アプリケーション ロールを作成するデータベースを展開します。  
  
2.  **[セキュリティ]** フォルダーを展開します。  
  
3.  **[ロール]** フォルダーを展開します。  
  
4.  **[アプリケーション ロール]** フォルダーを右クリックし、 **[新しいアプリケーション ロール...]** をクリックします。  
  
5.  **[アプリケーション ロール - 新規]** ダイアログ ボックスの **[全般]** ページで、 **[ロール名]** ボックスに、新しいアプリケーション ロールの名前を入力します。  
  
6.  **[既定のスキーマ]** ボックスで、オブジェクト名の入力によってこのロールが作成するオブジェクトを所有するスキーマを指定します。 または、省略記号 **[...]** をクリックして、 **[スキーマの検索]** ダイアログ ボックスを開きます。  
  
7.  **[パスワード]** ボックスに、新しいロールのパスワードを入力します。 **[パスワードの確認]** ボックスに、パスワードを再度入力します。  
  
8.  **[このロールが所有するスキーマ]** から、このロールが所有するスキーマを選択または表示します。 スキーマを所有できるのは、1 つのスキーマまたはロールのみです。  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="additional-options"></a>追加オプション  
 **[アプリケーション ロール - 新規 ]** ダイアログ ボックスには次の 2 つのページもあり、それぞれにオプションが用意されています: **[セキュリティ保護可能なリソース]** 、 **[拡張プロパティ]** 。  
  
-   **[セキュリティ保護可能なリソース]** ページには、すべてのセキュリティ保護可能なリソースと、ログインに付与できる、セキュリティ保護可能なリソースに対する権限が一覧表示されます。  
  
-   **[拡張プロパティ]** ページでは、カスタム プロパティをデータベース ユーザーに追加できます。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-an-application-role"></a>アプリケーション ロールを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates an application role called "weekly_receipts" that has the password "987Gbv876sPYY5m23" and "Sales" as its default schema.  
  
    CREATE APPLICATION ROLE weekly_receipts   
        WITH PASSWORD = '987G^bv876sPY)Y5m23'   
        , DEFAULT_SCHEMA = Sales;  
    GO  
    ```  
  
 詳細については、「[CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md)」を参照してください。  
  
  
