---
title: Azure Data Studio の Notebooks と SQL Kernel
description: このチュートリアルでは、SQL Server ノートブックを作成し、実行する方法を紹介します。
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: cd71a160036bdcb5768e7a2ca51529989f733eeb
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364209"
---
# <a name="create-and-run-a-sql-server-notebook"></a>SQL Server ノートブックを作成して実行する

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

このチュートリアルでは、SQL Server を使用し、Azure Data Studio でノートブックを作成し、実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [Azure Data Studio をインストールしていること](../download-azure-data-studio.md)
- SQL Server をインストールしていること
  - [Windows](../../database-engine/install-windows/install-sql-server.md)
  - [Linux](../../linux/sql-server-linux-setup.md)

## <a name="create-a--notebook"></a>ノートブックを作成する

次の手順では、Azure Data Studio でノートブック ファイルを作成する方法を示しています。

1. Azure Data Studio で SQL Server に接続します。

2. **[サーバー]** ウィンドウの **[接続]** の下で選択します。 次に **[新しいノートブック]** を選択します。

3. **[カーネル]** とターゲット コンテキスト ( **[アタッチ先]** ) が設定されるまで待ちます。 **[カーネル]** が **[SQL]** に設定されていることを確認し、SQL Server の **[アタッチ先]** を設定します (この例では *localhost* です)。

   ![[カーネル] と [アタッチ先] を設定する](media/notebooks-sql-kernel/set-kernel-and-attach-to.png)

ノートブックを保存するには、 **[ファイル]** メニューで **[保存]** または **[名前を付けて保存...]** コマンドを使用します。

ノートブックを開くには、 **[ファイル]** メニューで **[ファイルを開く...]** コマンドを使用して、 **[ようこそ]** ページで **[ファイルを開く]** を選択するか、コマンド パレットで **File:Open** コマンドを使用します。

## <a name="change-the-sql-connection"></a>SQL 接続を変更する

ノートブックの SQL 接続を変更するには、次のようにします。

1. ノートブック ツール バーから **[アタッチ先]** メニューを選択し、 **[接続の変更]** を選択します。

   ![ノートブックのツール バーから [アタッチ先] メニューを選択する](./media/notebooks-sql-kernel/select-attach-to-1.png)

2. これで最近使用した接続サーバーを選択するか、新しい接続の詳細を入力して接続できます。

## <a name="run-a-code-cell"></a>コード セルを実行する

その場で実行できる SQL コードを含むセルを作成するには、セルの左側にある **[セルの実行]** ボタン (黒の円矢印) をクリックします。 セルの実行が完了した後、結果がノートブックに表示されます。

次に例を示します。

1. ツールバーの **[+Code]** コマンドを選択して、新しいコード セルを追加します。

   ![ノートブック ツール バー](media/notebooks-guidance/notebook-toolbar.png)

2. 次の例をコピーしてセルに貼り付け、 **[セルの実行]** をクリックします。 この例では、新しいデータベースを作成します。

   ```sql
   USE master
   GO

   -- Drop the database if it already exists
   IF  EXISTS (
           SELECT name
           FROM sys.databases
           WHERE name = N'TestNotebookDB'
      )
   DROP DATABASE TestNotebookDB
   GO

   -- Create the database
   CREATE DATABASE TestNotebookDB
   GO
   ```

   ![セルの実行](media/notebooks-sql-kernel/run-notebook-cell.png)

## <a name="save-the-result"></a>結果を保存する

結果を返すスクリプトを実行する場合、結果の上部に表示されるツールバーを使用して、その結果を別の形式で保存できます。

- CSV として保存
- Excel として保存
- JSON として保存
- XML として保存

たとえば、次のコードでは [PI](../../t-sql/functions/pi-transact-sql.md) の結果が返されます。

```sql
SELECT PI() AS PI;
GO
```

![結果を保存する](media/notebooks-sql-kernel/run-notebook-cell-2.png)

## <a name="next-steps"></a>次のステップ

ノートブックについてさらに学習します:

- [Azure Data Studio でノートブックを使用する方法](./notebooks-guidance.md)
- [Python ノートブックを作成して実行する](././notebooks-python-kernel.md)
- [Spark を使用したサンプル ノートブックの実行](../../big-data-cluster/notebooks-tutorial-spark.md)