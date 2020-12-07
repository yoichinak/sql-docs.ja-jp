---
title: 'データベースの復元: 差分'
description: この記事では、SQL Server Management Studio または Transact-SQL を使用して、SQL Server でデータベースの差分バックアップを復元する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- restoring databases [SQL Server], full differential backups
- database backups [SQL Server], full differential backups
- database restores [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
ms.assetid: 0dd971a4-ee38-4dd3-9f30-ef77fc58dd11
author: cawrites
ms.author: chadam
ms.openlocfilehash: 6015242cd42a2e3b932a88cff827968cfb514c39
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129186"
---
# <a name="restore-a-differential-database-backup-sql-server"></a>データベースの差分バックアップの復元 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、データベースの差分バックアップを復元する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **データベースの差分バックアップを復元する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   RESTORE は、明示的または暗黙的なトランザクションでは使用できません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって作成されたバックアップは、それより前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では復元できません。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンを使用して作成したデータベース バックアップからユーザー データベースを復元できます。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   完全復旧モデルまたは一括ログ復旧モデルを使用する場合は、データベースを復旧する前に、ログの末尾と呼ばれるアクティブ トランザクション ログをバックアップする必要があります。 詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)」を参照してください。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています (FROM DATABASE_SNAPSHOT オプションを使用する場合、データベースは常に存在します)。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-restore-a-differential-database-backup"></a>データベースの差分バックアップを復元するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の適切なインスタンスに接続後、オブジェクト エクスプローラーでサーバー名をクリックして、サーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。 復元するデータベースに応じて、ユーザー データベースを選択するか、 **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[復元]** をポイントして、 **[データベース]** をクリックします。  
  
4.  **[全般]** ページの **復元元** のセクションを使用して、復元するバックアップ セットの復元元ファイルと場所を指定します。 以下のオプションの 1 つを選択します。  
  
    -   **[データベース]**  
  
         復元するデータベースをドロップダウン リストから選択します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    > [!NOTE]  
    >  別のサーバーで作成されたバックアップの場合、復元先のサーバーには指定されたデータベースのバックアップ履歴情報が存在しません。 この場合、 **[デバイス]** をクリックして、復元するファイルまたはデバイスを手動で指定します。  
  
    -   **[デバイス]**  
  
         参照ボタン ( **[...]** ) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[バックアップ メディアの種類]** ボックスから、デバイスの種類を 1 つ選択します。 **[バックアップ メディア]** ボックスにデバイスを追加するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
         **[ソース: デバイス:データベース]** リスト ボックスで、復元するデータベースの名前を選択します。  
  
         **メモ** この一覧は **[デバイス]** をクリックした場合にのみ使用できます。 選択されたデバイスにバックアップを持つデータベースのみが使用できるようになります。  
  
5.  **復元先のセクション** の **[データベース]** ボックスに、復元するデータベースの名前が自動的に表示されます。 データベースの名前を変更するには、 **[データベース]** ボックスに新しい名前を入力します。  
  
    > [!NOTE]  
    >  特定の時点で復元を停止するには、 **[タイムライン]** をクリックして、 **[バックアップのタイムライン]** ダイアログ ボックスにアクセスします。 特定の時点でデータベースの復元を停止する方法については、「[SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
6.  **[復元するバックアップ セット]** グリッドで、差分バックアップを通じて復元するバックアップを選択します。  
  
     **[復元するバックアップ セット]** グリッドの列の詳細については、「[データベースの復元 &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)」を参照してください。  
  
7.  **[オプション]** ページの **[復元オプション]** パネルでは、状況に応じて、次の任意のオプションを選択できます。  
  
    -   **[既存のデータベースを上書きする (WITH REPLACE)]**  
  
    -   **[レプリケーションの設定を保存する (WITH KEEP_REPLICATION)]**  
  
    -   **[各バックアップを復元する前に確認する]**  
  
    -   **[復元するデータベースへのアクセスを制限する (WITH RESTRICTED_USER)]**  
  
     これらのオプションの詳細については、「[データベースの復元 &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)」を参照してください。  
  
8.  **[復旧状態]** ボックスのオプションを選択します。 このボックスの選択内容により、復元操作後のデータベースの状態が決まります。  
  
    -   **[RESTORE WITH RECOVERY]** : コミットされていないトランザクションをロールバックして、データベースを使用可能な状態にします。これが既定の動作です。 別のトランザクション ログは復元できません。 このオプションは、必要なバックアップをすべて復元する場合に選択します。  
  
    -   **[RESTORE WITH NORECOVERY]** : データベースは操作不可状態のままとなり、コミットされていないトランザクションはロールバックされません。 別のトランザクション ログは復元できます データベースは、復旧されるまで使用できません。  
  
    -   **[RESTORE WITH STANDBY]** : データベースを読み取り専用モードにします。 コミットされていないトランザクションは元に戻されますが、復旧結果を元に戻せるように元に戻す操作をスタンバイ ファイルに保存します。  
  
     オプションの詳細については、「[データベースの復元 &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)」を参照してください。  
  
9. データベースへのアクティブな接続がある場合、復元操作は失敗します。 **とデータベース間のすべてのアクティブな接続を閉じるには、** [既存の接続を閉じる] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] オプションをオンにします。  
  
10. 復元操作と復元操作の間に、その都度、確認のメッセージを表示するには、 **[各バックアップを復元する前に確認する]** をオンにします。 通常は、その必要はありません。データベースが大きく、復元操作のステータスを監視する必要がある場合にのみ使用します。  
  
11. (省略可) データベースを新しい場所に復元するには、 **[ファイル]** ページを使用します。 データベースの移動に関する詳細については、「[データベースを新しい場所に復元する &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)」を参照してください。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-restore-a-differential-database-backup"></a>データベースの差分バックアップを復元するには  
  
1.  NORECOVERY 句を指定して RESTORE DATABASE ステートメントを実行し、データベースの差分バックアップの前に、データベースの完全バックアップを復元します。 詳細については、「[完全バックアップの復元](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)に関するページを参照してください。  
  
2.  RESTORE DATABASE ステートメントを実行して、データベースの差分バックアップを復元します。そのとき、以下を指定します。  
  
    -   データベースの差分バックアップを適用するデータベースの名前。  
  
    -   データベースの差分バックアップの復元元であるバックアップ デバイス。  
  
    -   NORECOVERY 句。データベースの差分バックアップを復元した後、適用するトランザクション ログ バックアップがある場合に指定します。 それ以外の場合は、RECOVERY 句を指定します。  
  
3.  完全復旧モデルでも、一括ログ復旧モデルでも、データベースの差分バックアップの復元では、データベースの差分バックアップが完了した時点にデータベースが復元されます。 障害の時点にさかのぼってデータベースを復旧するには、直前のデータベースの差分バックアップを作成した後に生成されたすべてのトランザクション ログ バックアップを適用する必要があります。 詳細については、「[トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)」を参照してください。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 例 (Transact-SQL)  
  
#### <a name="a-restoring-a-differential-database-backup"></a>A. データベースの差分バックアップの復元  
 この例では、 `MyAdvWorks` データベースのデータベース バックアップおよびデータベースの差分バックアップを復元します。  
  
```sql  
-- Assume the database is lost, and restore full database,   
-- specifying the original full database backup and NORECOVERY,   
-- which allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   RECOVERY;  
GO  
```  
  
#### <a name="b-restoring-a-database-differential-database-and-transaction-log-backup"></a>B. データベース バックアップ、データベースの差分バックアップ、およびトランザクション ログ バックアップの復元  
 この例では、 `MyAdvWorks` データベースのデータベース バックアップ、データベースの差分バックアップ、およびトランザクション ログ バックアップを復元します。  
  
```sql  
-- Assume the database is lost at this point. Now restore the full   
-- database. Specify the original full database backup and NORECOVERY.  
-- NORECOVERY allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   NORECOVERY;  
GO  
-- Now restore each transaction log backup created after  
-- the differential database backup.  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log1  
   WITH NORECOVERY;  
GO  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log2  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
