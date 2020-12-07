---
title: SSMS 使用のヒントとテクニック
description: SQL Server Management Studio でコードをコメント化する、コードのコメント化を解除する、テキストをインデントする、オブジェクトをフィルター処理する、エラー ログにアクセスする、SQL Server インスタンス名を見つける方法について説明します。
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: sstein
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- Find SQL Server Instance
- find instance name
- find sql server instance name
ms.custom: seo-lt-2019
ms.date: 03/13/2018
ms.openlocfilehash: 1f05ea22f092573364e663165559be73857ca320
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038919"
---
# <a name="tips-and-tricks-for-using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) の使用に関するヒントとテクニック

この記事では、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) を使用するためのヒントとテクニックについて説明します。 この記事で取り上げるテクニック: 

> [!div class="checklist"]
> * Transact-SQL (T-SQL) のテキストをコメント化する/コメント解除する
> * テキストをインデントする
> * オブジェクト エクスプローラーでオブジェクトにフィルターを適用する
> * [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログにアクセスする
> * [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前を検索する

## <a name="prerequisites"></a>前提条件

この記事に記載されている手順をテストするには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、SQL サーバーへのアクセス、および AdventureWorks データベースが必要です。 

* [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md) をインストールします。
* [[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールします。
* [AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases)をダウンロードする。 SSMS でデータベースを復元する方法については、[データベースの復元](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)に関するページを参照してください。 

## <a name="commentuncomment-your-t-sql-code"></a>T-SQL コードをコメント化する/コメント解除する

ツール バーの **[コメント]** ボタンを使用し、テキストの一部をコメント化したり、コメント化を解除したりできます。 コメント化されたテキストは実行されません。

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開きます。

2. SQL Server に接続します。

3. [新しいクエリ] ウィンドウを開きます。

4. 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] をテキスト ウィンドウに貼り付けます。

    ```sql
    USE master
        GO

        -- Drop the database if it already exists
        IF  EXISTS (
            SELECT name 
                FROM sys.databases 
                WHERE name = N'TutorialDB'
                )

        DROP DATABASE TutorialDB
        GO

        CREATE DATABASE TutorialDB
        GO

        ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
        GO
   ```

5. テキストの **Alter Database** 部分を強調表示し、ツール バーの **[コメント]** ボタンを選択します。 

    ![[コメント] ボタン](media/ssms-tricks/comment.png)
6. **[実行]** を選択し、テキストのコメント解除された部分を実行します。 

7. **Alter Database** コマンド以外をすべて強調表示し、 **[コメント]** ボタンを選択します。

    ![すべてをコメント化する](media/ssms-tricks/commenteverything.png)

    > [!NOTE]
    > テキストをコメント化するためのキーボード ショートカットは **CTRL + K、CTRL + C** です。

8. テキストの **Alter Database** 部分を強調表示し、ツール バーの **[Uncomment]\(コメントを解除する\)** ボタンを選択してコメントを解除します。

    ![テキストのコメントを解除する](media/ssms-tricks/uncomment.png)

    > [!NOTE]
    > テキストのコメントを解除するためのキーボード ショートカットは **CTRL + K、CTRL + C** です。

9. **[実行]** を選択し、テキストのコメント解除された部分を実行します。

## <a name="indent-your-text"></a>テキストをインデントする

ツール バーのインデント ボタンを使用し、テキストのインデントを増減できます。

1. [新しいクエリ] ウィンドウを開きます。

2. 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードをテキスト ウィンドウに貼り付けます。

    ```sql
    USE master
      GO

      --Drop the database if it already exists
      IF  EXISTS (
            SELECT name
                FROM sys.databases
                WHERE name = N'TutorialDB'
              )

      DROP DATABASE TutorialDB
      GO

      CREATE DATABASE TutorialDB
      GO

      ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
      GO
    ```

3. テキストの **Alter Database** の部分を強調表示し、ツール バーの **[インデント]** を選択してこのテキストを右に移動します。

    ![インデントを増やす](media/ssms-tricks/increaseindent.png)

4. テキストの **Alter Database** の部分を強調表示し、 **[インデント解除]** ボタンを選択してこのテキストを左に移動します。

    ![インデントを減らす](media/ssms-tricks/decreaseindent.png)

## <a name="filter-objects-in-object-explorer"></a>オブジェクト エクスプローラーでオブジェクトにフィルターを適用する

多くのオブジェクトが含まれるデータベースの場合は、フィルターを使用して特定のテーブル、ビューなどを検索できます。このセクションでは、テーブルにフィルターを適用する方法について説明しますが、次の手順はオブジェクト エクスプローラーの他のノードでも利用できます。

1. SQL Server に接続します。

2. **[データベース]**  >  **[AdventureWorks]**  >  **[テーブル]** の順に展開します。 データベース内のすべてのテーブルが表示されます。

3. **[テーブル]** を右クリックし、 **[フィルター]**  >  **[フィルターの設定]** の順に選択します。

    ![フィルターの設定](media/ssms-tricks/filtersettings.png)

4. **[フィルターの設定]** ウィンドウで、次のフィルター設定の一部を変更できます。
    * 名前でフィルター: 

      ![名前でフィルター](media/ssms-tricks/filterbyname.png)

    * スキーマでフィルター: 

      ![スキーマでフィルター](media/ssms-tricks/filterbyschema.png)

5. フィルターを消去するには、 **[テーブル]** を右クリックし、 **[フィルターの削除]** を選択します。

    ![フィルターの削除](media/ssms-tricks/removefilter.png)

## <a name="access-your-sql-server-error-log"></a>SQL Server のエラー ログにアクセスする

エラー ログは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内で発生したことに関する詳細な情報を含むファイルです。 SSMS では、エラー ログを参照したり、クエリを実行したりできます。 エラー ログは、ディスクに置かれている .log ファイルです。

### <a name="open-the-error-log-in-ssms"></a>SSMS でエラー ログを開く

1. ご利用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続します  

2. **[管理]**  >  **[SQL Server ログ]** の順に展開します。 

3. **[現在]** のエラー ログを右クリックし、 **[SQL Server ログの表示]** を選択します。

    ![SSMS でエラー ログを表示する](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-the-error-log-in-ssms"></a>SSMS でエラー ログにクエリを実行する

1. SQL Server に接続します。

2. [新しいクエリ] ウィンドウを開きます。

3. 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードをクエリ ウィンドウに貼り付けます。

     ```sql
       sp_readerrorlog 0,1,'Server process ID'
      ```

4. 単一引用符で囲まれたテキストを検索するテキストに変更します。

5. クエリを実行し、結果を確認します。

    ![エラー ログにクエリを実行する](media/ssms-tricks/queryerrorlog.png)

### <a name="find-the-error-log-location-if-youre-connected-to-sql-server"></a>SQL Server に接続されている場合にエラー ログの場所を検索する

1. ご利用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続します

2. [新しいクエリ] ウィンドウを開きます。

3. クエリ ウィンドウに次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを貼り付けて、 **[実行]** を選択します。

     ```sql
        SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
      ```

4. 結果に、ファイル システム内のエラー ログの場所が示されます。 

    ![クエリでエラー ログを見つける](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-the-error-log-location-if-you-cant-connect-to-sql-server"></a>SQL Server に接続できない場合にエラー ログの場所を検索する

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログのパスは、構成設定によって異なる場合があります。 エラー ログの場所のパスは、SQL Server 構成マネージャー内の、起動時のパラメーターで確認できます。 次の手順に従って、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログの場所を特定するための、関連する起動時のパラメーターを見つけます。 "*ユーザーのパスは次に示されるパスとは異なる場合があります*"。

1. SQL Server 構成マネージャーを開きます。

2. **[サービス]** を展開します。

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを右クリックして、 **[プロパティ]** を選択します。

    ![構成マネージャー サーバーのプロパティ](media/ssms-tricks/serverproperties.PNG)

4. **[起動時のパラメーター]** タブを選択します。

5. **[既存のパラメーター]** 領域で、"-e" の後のパスがエラー ログの場所です。 

    ![エラー ログ](media/ssms-tricks/errorlog.png)

    この場所には複数のエラー ログ ファイルがあります。 *.log で終わるファイル名が現在のエラー ログ ファイルです。 数字で終わるファイル名は以前のログ ファイルです。 SQL Server が再起動するたびに新しいログが作成されます。

6. メモ帳で errorlog.log ファイルを開きます。

## <a name="find-sql-server-instance-name"></a>SQL Server インスタンス名を見つける

SQL Server に接続する前に、あるいは接続した後に、いくつかの方法で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前を検索できます。  

### <a name="before-you-connect-to-sql-server"></a>SQL Server に接続する前

1. 次の手順で[ディスク上の SQL Server エラー ログ](#find-the-error-log-location-if-you-cant-connect-to-sql-server)を探します。 実際のパスは次の図のパスとは異なる場合があります。

2. メモ帳で errorlog.log ファイルを開きます。

3. *Server name is* というテキストを探します。

    単一引用符で囲まれているのが、これから接続する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前です。

    ![エラー ログでサーバー名を見つける](media/ssms-tricks/servernameinlog.png)

    名前の形式は "ホスト名\インスタンス名" です。 ホスト名しか表示されない場合、既定のインスタンスをインストールしており、インスタンス名は MSSQLSERVER です。 既定のインスタンスに接続するとき、ホスト名だけを入力して SQL Server に接続できます。  

### <a name="when-youre-connected-to-sql-server"></a>SQL Server に接続しているとき

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続しているとき、3 か所でサーバー名が見つかります。 

1. サーバーの名前はオブジェクト エクスプローラーに表示されます。

    ![オブジェクト エクスプローラーの SQL Server インスタンス名](media/ssms-tricks/nameinobjectexplorer.png)
2. サーバーの名前はクエリ ウィンドウに表示されます。

    ![クエリ ウィンドウの SQL Server インスタンス名](media/ssms-tricks/nameinquerywindow.png)
3. サーバーの名前は **[プロパティ]** に表示されます。
    * **[表示]** メニューで、 **[プロパティ ウィンドウ]** を選択します。

      ![プロパティ ウィンドウの SQL Server インスタンス名](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>別名または可用性グループ リスナーに接続している場合

別名または可用性グループ リスナーに接続している場合、その情報がオブジェクト エクスプローラーとプロパティに表示されます。 その場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前はすぐにはわからないことがあり、クエリを行う必要があります。

1. SQL Server に接続します。

2. [新しいクエリ] ウィンドウを開きます。

3. 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを新しいファイルに貼り付けます。

      ```sql
       select @@Servername
     ```

4. クエリの結果を見て、接続している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前を確認します。 

    ![SQL Server 名を問い合わせる](media/ssms-tricks/queryservername.png)

## <a name="next-steps"></a>次のステップ

SSMS に慣れ親しむには、実践的な経験を積むのが最も効果的です。 以下の "*チュートリアル*" と "*操作方法*" に関する記事は、SSMS 内で使用できるさまざまな機能を使用するのに役立ちます。  以下の記事では、SSMS のコンポーネントを管理する方法と、頻繁に使用する機能にアクセスする方法が説明されています。

* [インスタンスに接続してクエリを実行する](../quickstarts/connect-query-sql-server.md)
* [スクリプトの作成](scripting-ssms.md)
* [SSMS でテンプレートを使用する](../template/templates-ssms.md)
* [SSMS を構成する](ssms-configuration.md)