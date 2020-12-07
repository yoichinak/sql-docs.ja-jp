---
title: Azure SQL データベースに対する接続およびクエリ
description: クイックスタートで Azure Data Studio を使用して Azure SQL Database サーバーに接続し、データベースを作成してクエリを実行します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu; maghan; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; sqlfreshmay19; seo-lt-2019
ms.date: 05/14/2019
ms.openlocfilehash: 7eb89be3b94565f7a8642dad893642176a22822b
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439296"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-azure-sql-database"></a>クイック スタート:Azure Data Studio を使用して、Azure SQL Database に接続してクエリを実行する

このクイック スタートでは、Azure Data Studio を使用して Azure SQL Database サーバーに接続します。 次に、Transact-SQL (T-SQL) ステートメントを実行して、他の Azure Data Studio チュートリアルで使用されている TutorialDB データベースを作成し、クエリを実行します。

## <a name="prerequisites"></a>前提条件

このクイック スタートを完了するには、Azure Data Studio と Azure SQL Database サーバーが必要です。

- [Azure Data Studio をインストールする](./download-azure-data-studio.md?view=sql-server-ver15)

Azure SQL サーバーがない場合は、次のいずれかの Azure SQL Database クイック スタートを完了します。 後の手順のために、完全修飾サーバー名とサインイン資格情報を覚えておいてください。

- [DB の作成 - ポータル](/azure/sql-database/sql-database-get-started-portal)
- [DB の作成 - CLI](/azure/sql-database/sql-database-get-started-cli)
- [DB の作成 - PowerShell](/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Azure SQL Database サーバーへの接続

Azure Data Studio を使用して、Azure SQL Database サーバーへの接続を確立します。

1. 最初に Azure Data Studio を実行すると、 **[ようこそ]** ページが開きます。 **ウェルカム** ページが表示されない場合は、 **[ヘルプ]**  >  **[ようこそ]** を選択します。 **[新しい接続]** を選択して、 **[接続]** ウィンドウを開きます。
   
   ![[次の接続] オプションが選択されている Azure Delta Studio の [ようこそ] ダイアログ ボックスを示すスクリーンショット。](media/quickstart-sql-database/new-connection-icon.png)

2. この記事では、SQL サインインを使用しますが、Windows 認証もサポートされています。 ご利用の Azure SQL サーバーのサーバー名、ユーザー名、パスワードを使用して、次のようにフィールドに入力します。

   | 設定       | 推奨値 | 説明 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバー名** | 完全修飾サーバー名 | **servername.database.windows.net** のようなものです。 |
   | **認証** | SQL ログイン| このチュートリアルでは、SQL 認証を使用します。 |
   | **ユーザー名** | サーバー管理者アカウントのユーザー名 | サーバーの作成に使用したアカウントのユーザー名。 |
   | **パスワード (SQL ログイン)** | サーバー管理者アカウントのパスワード | サーバーの作成に使用したアカウントのパスワード。 |
   | **パスワードを保存しますか?** | はい、いいえ | 毎回パスワードを入力したくない場合は、 **[はい]** を選択します。 |
   | **データベース名** | *空白のままにする* | ここでは、サーバーに接続するだけです。 |
   | **サーバー グループ** | <Default> を選択 | 作成した特定のサーバー グループにフィールドを設定できます。 | 

   ![Azure Data Studio のスクリーンショット - [接続] ページ。](media/quickstart-sql-database/new-connection-screen.png)  

3. **[接続]** を選択します。

4. サーバーに Azure Data Studio の接続を許可するファイアウォール規則がない場合は、 **[新しいファイアウォール規則の作成]** フォームが開きます。 フォームに入力して、新しいファイアウォール規則を作成します。 詳細については、[ファイアウォール規則](/azure/sql-database/sql-database-firewall-configure)に関するページを参照してください。

   ![新しいファイアウォール規則](media/quickstart-sql-database/firewall.png)  

接続が正常に行われると、ご利用のサーバーが **[サーバー]** サイドバーに表示されます。

## <a name="create-the-tutorial-database"></a>チュートリアル データベースの作成

次のセクションでは、他の Azure Data Studio チュートリアルで使用されている TutorialDB データベースを作成します。

1. **[サーバー]** サイドバーで Azure SQL サーバーを右クリックし、 **[新しいクエリ]** を選択します。

1. この SQL をクエリ エディターに貼り付けます。

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. ツール バーで **[実行]** を選択します。 通知が、 **[メッセージ]** ウィンドウに表示され、クエリの進行状況が表示されます。

## <a name="create-a-table"></a>テーブルを作成する

クエリ エディターは **master** データベースに接続されていますが、 **TutorialDB** データベースにテーブルを作成する必要があります。 

1. **TutorialDB** データベースに接続します。

   ![変更コンテキスト](media/quickstart-sql-database/change-context2.png)



1. `Customers` テーブルを作成します。 

   クエリ エディターで前のクエリをこのクエリに置き換え、 **[実行]** を選択します。

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>テーブルに行を挿入する

前のクエリをこのクエリに置き換えて、 **[実行]** を選択します。

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>結果を表示する

前のクエリをこのクエリに置き換えて、 **[実行]** を選択します。

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

クエリ結果が表示されます。

   ![結果の選択](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>リソースをクリーンアップする

この後のクイック スタートの記事は、ここで作成したリソースに基づいています。 これらの記事を使用する場合は、これらのリソースを削除しないようにしてください。 それ以外の場合は、Azure portal で、不要になったリソースを削除します。 詳細については、「[リソースのクリーンアップ](/azure/sql-database/sql-database-get-started-portal#clean-up-resources)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure SQL データベースに正常に接続してクエリを実行したので、[コード エディターのチュートリアル](tutorial-sql-editor.md)をお試しください。