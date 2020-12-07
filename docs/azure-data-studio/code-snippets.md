---
title: 再利用可能なコード スニペットの作成
description: データベースとデータベース オブジェクトの作成を簡単にする Azure Data Studio SQL コード スニペットを作成し、使用する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: aa1826539a6b9d2a5f649159e566d3ceda8d624d
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364129"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-azure-data-studio"></a>Azure Data Studio でコード スニペットを作成して使用し、Transact-SQL (T-SQL) スクリプトをすばやく作成する

Azure Data Studio のコード スニペットは、データベースおよびデータベース オブジェクトを簡単に作成できるようにするテンプレートです。 

Azure Data Studio には、適切な構文を迅速に生成するのに役立つ、複数の T-SQL スニペットが用意されています。 

ユーザー定義のコード スニペットを作成することもできます。

## <a name="using-built-in-t-sql-code-snippets"></a>組み込みの T-SQL コード スニペットの使用

1. 使用可能なスニペットにアクセスするには、クエリ エディターで「*sql*」と入力してリストを開きます。

   ![スニペット](media/code-snippets/sql-snippets.png)

2. 使用するスニペットを選択すると、T-SQL スクリプトが生成されます。 たとえば、*sqlCreateTable* を選択します。

   ![テーブル スニペットの作成](media/code-snippets/create-table.png)

3. 強調表示されたフィールドを特定の値で更新します。 たとえば、*TableName* と *Schema* をデータベースの値に置き換えます。

   ![スニペットからのテーブル](media/code-snippets/table-from-snippet.png)

   変更するフィールドが強調表示されなくなった場合 (これは、エディターの周囲でカーソルを移動したときに発生します)、変更する単語を右クリックし、 **[すべての出現箇所を変更]** を選択します。

   ![すべて変更](media/code-snippets/change-all.png)

4. 選択したスニペットに必要な追加の T-SQL を更新または追加します。 たとえば、*Column1*、*Column2* を更新し、さらに列を追加します。

## <a name="creating-sql-code-snippets"></a>SQL コード スニペットを作成する

独自のスニペットを定義できます。 編集するために SQL スニペット ファイルを開くには、次の操作を行います。

1. *コマンド パレット* (**Shift + Ctrl + P**) を開き、「*snip*」と入力して、 **[基本設定: ユーザー スニペットを開く]** を選択します。

   ![ユーザー スニペット](media/code-snippets/user-snippets.png)

2. **[SQL]** を選択します。

   > [!NOTE]
   > Azure Data Studio では Visual Studio Code からそのコード スニペット機能を継承するため、この記事では SQL スニペットの使用について具体的に説明します。 詳細については、Visual Studio Code ドキュメントの「[独自のスニペットを作成する](https://code.visualstudio.com/docs/editor/userdefinedsnippets)」を参照してください。 

   ![Select SQL](media/code-snippets/select-sql.png)

3. 次のコードを *sql.json* に貼り付けます。

    ```sql
    {
     "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "$1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "Column1 [NVARCHAR](50) NOT NULL,",
    "Column2 [NVARCHAR](50) NOT NULL",
    "-- specify more columns here",
    ");",
    "GO"
    ],
       "description": "User-defined snippet example 2"
       }
       }
       ```

4. Save the sql.json file.

5. Open a new query editor window by clicking **Ctrl+N**.

6. Type **sql**, and you see the two user snippets you just added; *sqlCreateTable2* and *sqlSelectTop5*.

Select one of the new snippets and give it a test run!

## Next steps

For information about the SQL editor, see [Code editor tutorial](tutorial-sql-editor.md).
