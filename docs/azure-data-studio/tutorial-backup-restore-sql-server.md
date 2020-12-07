---
title: データベースのバックアップと復元する
description: このチュートリアルでは、Azure Data Studio を使用してデータベースをバックアップおよび復元する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 808dec10c92bffe66122bfa9a55d7db1cc64f62e
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364172"
---
# <a name="tutorial-back-up-and-restore-databases-using-azure-data-studio"></a>チュートリアル:Azure Data Studio を使用したデータベースのバックアップと復元

このチュートリアルでは、次の目的で Azure Data Studio を使用する方法について説明します。
> [!div class="checklist"]
> * データベースをバックアップする。
> * バックアップ状態を表示する。
> * バックアップを実行するために使用するスクリプトを生成する。
> * データベースを復元する。
> * 復元タスクの状態を表示する。

## <a name="prerequisites"></a>前提条件

このチュートリアルには、SQL Server *TutorialDB* が必要です。 TutorialDB データベースを作成するには、次のクイックスタートを実行します。

* [Azure Data Studio を使用して、SQL Server に接続してクエリを実行する](quickstart-sql-server.md)

このチュートリアルでは、SQL Server データベースに接続する必要があります。 Azure SQL Database には自動バックアップがあるため、Azure Data Studio では Azure SQL Database のバックアップと復元が実行されません。 詳しくは、「[SQL Database 自動バックアップについての詳細情報](/azure/sql-database/sql-database-automated-backups)」をご覧ください。

## <a name="back-up-a-database"></a>データベースをバックアップする

1. **[サーバー]** サイドバーを開いて、TutorialDB データベース ダッシュボードを開きます。 次に、**Ctrl + G** を選択し、 **[データベース]** を展開して **TutorialDB** を右クリックし、 **[管理]** を選択します。

1. **[タスク]** ウィジェットで **[バックアップ]** を選択して、 **[データベースのバックアップ]** ダイアログ ボックスを開きます。

   ![タスク ウィジェットを示すスクリーンショット。](./media/tutorial-backup-restore-sql-server/tasks.png)

1. このチュートリアルでは、既定のバックアップ オプションを使用するため、 **[バックアップ]** を選択します。

   ![[バックアップ] ダイアログ ボックスを示すスクリーンショット。](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

**[バックアップ]** を選択すると、 **[データベースのバックアップ]** ダイアログ ボックスが消え、バックアップ プロセスが開始されます。

## <a name="view-the-backup-status-and-the-backup-script"></a>バックアップの状態とバックアップ スクリプトを表示する

1. **[タスク履歴]** ペインが表示されます。または、**Ctrl + T** を選択して開きます。

   ![[タスクの履歴] ペインを示すスクリーンショット。](./media/tutorial-backup-restore-sql-server/task-history.png)

1. エディターでバックアップ スクリプトを表示するには、 **[Backup Database succeeded]\(データベース バックアップに成功しました\)** を右クリックし、 **[スクリプト]** を選択します。

   ![バックアップ スクリプトを示すスクリーンショット。](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>データベースをバックアップ ファイルから復元する

1. **Ctrl + G** を選択して、 **[サーバー]** サイドバーを開きます。 次に、ご使用のサーバーを右クリックし、 **[管理]** を選択します。

1. **[タスク]** ウィジェットで **[復元]** を選択して、 **[データベースの復元]** ダイアログ ボックスを開きます。

   ![タスクの復元を示すスクリーンショット。](media/tutorial-backup-restore-sql-server/tasks-restore.png)

1. **[復元元]** ボックスで **[バックアップ ファイル]** を選択します。

1. **[バックアップ ファイル パス]** ボックスの省略記号 (...) を選択し、*TutorialDB* の最新バックアップ ファイルを選択します。

1. **[Destination]\(復元先\)** セクションの **[ターゲット データベース]** ボックスに「**TutorialDB_Restored**」と入力して、バックアップ ファイルを新しいデータベースに復元します。 次に、 **[復元]** を選択します。

   ![復元バックアップを示すスクリーンショット。](./media/tutorial-backup-restore-sql-server/restore.png)

1. 復元操作の状態を表示するには **Ctrl + T** を選択して **[タスク履歴]** を開きます。

   ![復元タスク履歴を示すスクリーンショット。](./media/tutorial-backup-restore-sql-server/task-history-restore.png)