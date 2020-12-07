---
title: クイック スタート:PostgreSQL に対する接続およびクエリ
description: クイックスタートで Azure Data Studio を使用して PostgreSQL に接続し、SQL ステートメントを使用してデータベースを作成し、クエリを実行します。
ms.custom: seodec18
ms.date: 09/18/2019
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu, maghan, sstein
ms.topic: quickstart
author: sunilagarwal
ms.author: sunila
ms.openlocfilehash: fddbceec338a05d693fd9d1e039d08e271bbc01f
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785005"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-postgresql"></a>クイック スタート:Azure Data Studio を使用して、PostgreSQL に接続してクエリを実行する

このクイック スタートでは、Azure Data Studio を使用して PostgreSQL に接続し、SQL ステートメントを使用して、データベース *tutorialdb* を作成し、クエリを実行する方法を示します。

## <a name="prerequisites"></a>前提条件

このクイック スタートを完了するには、Azure Data Studio、Azure Data Studio 用の PostgreSQL 拡張機能、PostgreSQL サーバーへのアクセス権が必要です。

- [Azure Data Studio をインストールする](./download-azure-data-studio.md?view=sql-server-ver15)。
- [Azure Data Studio 用の PostgreSQL 拡張機能をインストールする](./extensions/postgres-extension.md)。
- [PostgreSQL をインストールする](https://www.postgresql.org/download/)。 (または、[az postgres up](/azure/postgresql/quickstart-create-server-up-azure-cli) を使用して、クラウドに Postgres データベースを作成することもできます)。 

## <a name="connect-to-postgresql"></a>PostgreSQL への接続

1. **Azure Data Studio** を起動します。

2. 初めて Azure Data Studio を起動すると、 **[接続]** ダイアログが開きます。 **[接続]** ダイアログが開いていない場合は、 **[サーバー]** ページの **[新しい接続]** アイコンをクリックします。

   ![新しい接続アイコン](media/quickstart-postgresql/new-connection-icon.png)

3. ポップアップ表示されたフォームで、 **[接続の種類]** に移動し、ドロップダウンから **[PostgreSQL]** を選択します。


4. ご利用の PostgreSQL サーバーのサーバー名、ユーザー名、パスワードを使用して、残りのフィールドに入力します。 

   ![新しい接続画面](media/quickstart-postgresql/new-connection-screen.png)  

   | 設定       | 値の例 | 説明 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバー名** | localhost | 完全修飾サーバー名 |
   | **ユーザー名** | postgres | ログインに使用するユーザー名。 |
   | **パスワード (SQL ログイン)** | *password* | ログインに使用するアカウントのパスワード。 |
   | **パスワード** | *確認事項* | 接続するたびにパスワードを入力したくない場合は、このボックスをオンにします。 |
   | **データベース名** | \<Default\> | 接続でデータベースを指定する必要がある場合は、これを入力します。 |
   | **[サーバー グループ]** | \<Default\> | このオプションを使用すると、作成した特定のサーバー グループにこの接続を割り当てることができます。 | 
   | **名前 (省略可能)** | *空白のままにする* | このオプションを使用すると、サーバーのフレンドリ名を指定できます。 | 

5. **[接続]** を選択します。 

接続が正常に行われると、ご利用のサーバーが **[サーバー]** サイドバーに表示されます。


## <a name="create-a-database"></a>データベースを作成する

次の手順では、**tutorialdb** という名前のデータベースを作成します。

1. **[サーバー]** サイドバーで PostgreSQL サーバーを右クリックし、 **[新しいクエリ]** を選択します。

2. 開いたクエリ エディターにこの SQL ステートメントを貼り付けます。

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. ツール バーで **[実行]** を選択して、クエリを実行します。 通知が、 **[メッセージ]** ウィンドウに表示され、クエリの進行状況が表示されます。

>[!TIP]
> **[実行]** を使用する代わりに、キーボードの **F5** キーを使用してステートメントを実行することができます。

クエリが完了したら、 **[データベース]** を右クリックし、 **[最新の情報に更新]** を選択すると、 **[データベース]** ノードの下の一覧に **tutorialdb** が表示されます。


## <a name="create-a-table"></a>テーブルを作成する

 次の手順では、**tutorialdb** でテーブルを作成します。

1. クエリ エディターのドロップダウンを使用して、接続コンテキストを **tutorialdb** に変更します。 

   ![変更コンテキスト](media/quickstart-postgresql/change-context.png)

2. クエリ エディターに次の SQL ステートメントを貼り付けて、 **[実行]** をクリックします。 

   > [!NOTE]
   > これを追加するか、エディターで既存のクエリを上書きするかのいずれかを行うことができます。 **[実行]** をクリックすると、強調表示されているクエリのみが実行されます。 何も強調表示されていない場合、 **[実行]** をクリックすると、エディター内のすべてのクエリが実行されます。

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>行を挿入する

クエリ ウィンドウに次のスニペットを貼り付けて、 **[実行]** をクリックします。

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>データにクエリを実行する

1. クエリ エディターに次のスニペットを貼り付けて、 **[実行]** をクリックします。
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. クエリの結果が表示されます:

   ![結果の表示](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>次の手順

[Azure Data Studio で Postgres に使用できるシナリオ](./extensions/postgres-extension.md)について学習します。