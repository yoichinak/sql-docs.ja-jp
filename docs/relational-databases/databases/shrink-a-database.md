---
title: データベースの圧縮 | Microsoft Docs
description: SQL Server Management Studio または Transact-SQL を使用して、SQL Server でオブジェクトを使用してデータベースを圧縮する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e2eced4a7ca9a8e8f443c709d65cc6e2906082a
ms.sourcegitcommit: e8c0c04eb7009a50cbd3e649c9e1b4365e8994eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2021
ms.locfileid: "100489496"
---
# <a name="shrink-a-database"></a>データベースの圧縮
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] のオブジェクトを使用して、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のデータベースを圧縮する方法について説明します。  
  
 ファイルの末尾にあるデータのページを、ファイルの先頭に近い占有されていない領域に移動することにより、データ ファイルが圧縮され、領域が回復されます。 ファイル末尾に十分な空き領域が作成された場合は、ファイル末尾のデータ ページの割り当てを解除して、ファイル システムに戻すことができます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用してデータベースを圧縮するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [データベースを圧縮する](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベースは、そのデータベースの最小サイズより小さくすることはできません。 最小サイズは、データベースが最初に作成されたときに指定されたサイズか、DBCC SHRINKFILE などのファイル サイズ変更操作によって最後に明示的に設定されたサイズのいずれかになります。 たとえば、作成時にサイズを 10 MB に指定したデータベースが 100 MB まで拡張した場合、データベース内のすべてのデータを削除したとしても、縮小できる限界は 10 MB までです。  
  
-   データベースのバックアップ中、データベースを圧縮することはできません。 逆に、データベースの圧縮操作の進行中、データベースをバックアップすることはできません。
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
  
-   データベース内にある現在の空き (未割り当て) 領域の大きさを確認します。 詳細については、「 [データベースのデータ領域とログ領域情報の表示](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)」をご覧ください。  
  
-   データベースを圧縮する場合は次のことを考慮してください。  
  
    -   圧縮操作は、テーブルの切り捨てやテーブルの削除操作など、大きな未使用領域を生成する操作の後に実行すると最も効果的です。  
  
    -   ほとんどのデータベースでは、毎日の定期的操作で使用するための空き領域が必要です。 データベースを何度圧縮しても、データベースのサイズが大きくなってしまう場合は、通常の操作にそれだけの領域が必要であることを示しています。 このような場合、繰り返しデータベースを圧縮することは無意味です。  
  
    -   圧縮操作では、データベース内のインデックスの断片化状態は保持されず、一般に、断片化の程度が大きくなります。 この理由からも、データベースを繰り返し圧縮することはお勧めできません。  
  
    -   特別な要件がない限り、AUTO_SHRINK データベース オプションを ON に設定しないでください。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-shrink-a-database"></a>データベースを圧縮するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、圧縮するデータベースを右クリックします。  
  
3.  **[タスク]** 、 **[圧縮]** の順にポイントし、 **[データベース]** をクリックします。  
  
     **[データベース]**  
     選択しているデータベースの名前が表示されます。  
  
     **[現在割り当てられている領域]**  
     選択されているデータベースの使用済み領域と未使用領域の合計を表示します。  
  
     **[使用可能な空き領域]**  
     選択されているデータベースのログ ファイルおよびデータ ファイル内の空き領域の合計を表示します。  
  
     **[未使用領域の解放前にファイルを再構成する]**  
     このオプションをオンにすることは、目的のパーセント オプションを指定して DBCC SHRINKDATABASE を実行することと同じです。 このオプションをオフにすると、TRUNCATEONLY オプションを使用して DBCC SHRINKDATABASE を実行するのと同じ効果があります。 既定では、ダイアログが開いたときに、このオプションはオフに設定されます。 このオプションをオンにした場合、ユーザーは目的のパーセント オプションを指定する必要があります。  
  
     **[圧縮後のファイルの最大空き領域]**  
     データベースを圧縮した後に、データベース ファイル内に残す空き領域の最大パーセンテージを入力します。 0 ～ 99 の値を指定できます。  
  
4.  **[OK]** をクリックします。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-shrink-a-database"></a>データベースを圧縮するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) を使用して、 `UserDB` データベース内のデータ ファイルとログ ファイルのサイズを圧縮し、データベースの空き領域が `10` % になるようにします。  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../relational-databases/databases/codesnippet/tsql/shrink-a-database_1.sql)]  
  
##  <a name="follow-up-after-you-shrink-a-database"></a><a name="FollowUp"></a>補足情報: データベースを圧縮した後  
 ファイルを圧縮するために移動されたデータは、ファイル内のあらゆる使用可能な場所に分散される場合があります。 これにより、インデックスの断片化が発生し、広範なインデックスを検索するクエリのパフォーマンスが低下する場合があります。 断片化を解消するには、圧縮後にファイルのインデックスを再構築することを検討してください。  
  
## <a name="see-also"></a>参照  
 [ファイルの圧縮](../../relational-databases/databases/shrink-a-file.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [データベース ファイルとファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
