---
title: Azure Synapse Analytics を使用した接続およびクエリ
description: このクイックスタートでは、Azure Data Studio を使用して Azure Synapse Analytics 内の専用 SQL プールに接続する方法を示します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.reviewer: maghan, jrasnick
ms.custom: seodec18; seo-lt-2019
ms.date: 10/15/2020
ms.openlocfilehash: 1b0fe9ee55f9e0e1243ea72e8160b39a95876a55
ms.sourcegitcommit: 2144a22ad4380182133e87664a907fe6f06b5f95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2020
ms.locfileid: "94570928"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-data-using-a-dedicated-sql-pool-in-azure-synapse-analytics"></a>クイックスタート: Azure Data Studio を使用して Azure Synapse Analytics の専用 SQL プールに接続し、データにクエリを実行する

このクイックスタートでは、Azure Data Studio を使用して Azure Synapse Analytics 内の専用 SQL プールに接続する方法を示します。

## <a name="prerequisites"></a>前提条件
このクイックスタートを完了するには、Azure Data Studio、および Azure Synapse Analytics の専用 SQL プールが必要です。

- [Azure Data Studio をインストールする](./download-azure-data-studio.md)。

専用 SQL プールがない場合は、[専用 SQL プールの作成](/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)に関する記事を参照してください。

サーバー名とログイン資格情報を覚えておいてください。


## <a name="connect-to-your-dedicated-sql-pool"></a>専用 SQL プールに接続する

Azure Data Studio を使用して、Azure Synapse Analytics サーバーへの接続を確立します。

1. 最初に Azure Data Studio を実行すると、 **[接続]** ページが開きます。 **[接続]** ページが表示されない場合は、 **[接続の追加]** を選択するか、 **[サーバー]** サイドバーの **[新しい接続]** アイコンを選択します。
   
   ![[接続] ページのスクリーンショット。[新しい接続] アイコンが選択されています。](media/quickstart-sql-dw/new-connection-icon.png)

2. この記事では、*SQL ログイン* を使用しますが、*Windows 認証* もサポートされています。 *ご利用の* Azure SQL サーバーのサーバー名、ユーザー名、パスワードを使用して、次のようにフィールドに入力します。

   |   設定    | 推奨値 | 説明 |
   |--------------|-----------------|-------------| 
   | **サーバー名** | 完全修飾サーバー名 | たとえば、**sqlpoolservername.database.windows.net** のような名前を指定します。 |
   | **認証** | SQL ログイン| このチュートリアルでは、SQL 認証を使用します。 |
   | **ユーザー名** | サーバー管理者アカウント | これはサーバーを作成したときに指定したアカウントです。 |
   | **パスワード (SQL ログイン)** | サーバー管理者アカウントのパスワード | これはサーバーを作成したときに指定したパスワードです。 |
   | **パスワードを保存しますか?** | はい、いいえ | 毎回パスワードを入力したくない場合は、 [はい] を選択します。 |
   | **データベース名** | *空白のままにする* | 接続先となるデータベースの名前。 |
   | **サーバー グループ** | <Default> を選択 | サーバー グループを作成した場合は、特定のサーバー グループに設定できます。 | 

3. サーバーに Azure Data Studio の接続を許可するファイアウォール規則がない場合は、 **[新しいファイアウォール規則の作成]** フォームが開きます。 フォームに入力して、新しいファイアウォール規則を作成します。 詳細については、[ファイアウォール規則](/azure/sql-database/sql-database-firewall-configure)に関するページを参照してください。

4. ご利用のサーバーに接続が正常に行われると、 *[サーバー]* サイドバーに表示されます。

## <a name="create-a-database-in-your-dedicated-sql-pool"></a>専用 SQL プールにデータベースを作成する

1. オブジェクト エクスプローラーでご利用のサーバーを右クリックし、 **[新しいクエリ]** を選択します。

2. クエリ エディターに次のスニペットを貼り付けて、 **[実行]** を選択します。

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```

## <a name="create-a-table"></a>テーブルを作成する

クエリ エディターはまだ *master* データベースに接続されていますが、*TutorialDB* データベースにテーブルを作成する必要があります。 

1. 接続コンテキストを **TutorialDB** に変更します。

2. クエリ エディターに次のスニペットを貼り付けて、 **[実行]** を選択します。

   > [!NOTE]
   > これを追加したり、エディターで前のクエリを上書きしたりすることができます。 **[実行]** を選択すると、選択されているクエリのみが実行されることに注意してください。 何も選択されていない場合、 **[実行]** を選択すると、エディター内のすべてのクエリが実行されます。

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

    :::image type="content" source="media/quickstart-sql-dw/create-table.png" alt-text="TutorialDB データベースにテーブルを作成する":::


## <a name="insert-rows"></a>行を挿入する

1. クエリ エディターに次のスニペットを貼り付けて、 **[実行]** を選択します。

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```

    :::image type="content" source="media/quickstart-sql-dw/create-rows.png" alt-text="テーブルに行を作成する":::

## <a name="view-the-result"></a>結果を表示する

1. クエリ エディターに次のスニペットを貼り付けて、 **[実行]** を選択します。

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

2. クエリの結果が表示されます:

    :::image type="content" source="media/quickstart-sql-dw/view-results.png" alt-text="結果を確認する":::


## <a name="clean-up-resources"></a>リソースをクリーンアップする

この記事で作成したサンプル データベースの操作を続行する予定がない場合は、[リソース グループを削除](/azure/synapse-analytics/sql-data-warehouse/create-data-warehouse-portal#clean-up-resources)してください。

## <a name="next-steps"></a>次のステップ
詳細については、[Azure Data Studio を使用した Synapse SQL への接続](https://docs.microsoft.com/azure/synapse-analytics/sql/get-started-azure-data-studio)に関する記事を参照してください。

Azure Synapse Analytics に正常に接続してクエリを実行したので、[コード エディターのチュートリアル](tutorial-sql-editor.md)を試してください。