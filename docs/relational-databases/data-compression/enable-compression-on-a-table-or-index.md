---
title: テーブルまたはインデックスの圧縮の有効化
description: SQL Server Management Studio または Transact-SQL を使用し、SQL Server のテーブルまたはインデックスで圧縮を有効にする方法について説明します。
ms.custom: ''
ms.date: 01/22/2021
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.compwiz.compressiontype.f1
- sql13.swb.compwiz.outputoptions.f1
- sql13.swb.compwiz.summary.f1
- sql13.swb.compwiz.scriptfileoption.f1
- sql13.swb.compwiz.progress.f1
- sql13.swb.compwiz.welcome.f1
- sql13.swb.compwiz.createjob.f1
- sql13.swb.compwiz.selectaction.f1
helpviewer_keywords:
- data compression wizard
- compression [SQL Server], enable
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016'
ms.openlocfilehash: 79a7a0fa7932f058218359b8bbe607b45f567a6b
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99251157"
---
# <a name="enable-compression-on-a-table-or-index"></a>テーブルまたはインデックスの圧縮の有効化

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

この記事では、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、テーブルまたはインデックスで[データ圧縮](../../relational-databases/data-compression/data-compression.md)を有効にする方法について説明します。
  
 **この記事の内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **次を使用してテーブルまたはインデックスの圧縮を有効にするには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   システム テーブルで圧縮を有効にすることはできません。  
  
-   テーブルがヒープの場合、ONLINE モードでは、再構築操作がシングル スレッドになります。 マルチスレッドのヒープの再構築操作では、OFFLINE モードを使用してください。 ONLINE オプションを指定しない限り、再構築操作は OFFLINE です。 ONLINE 再構築の実行の詳細については、「[オンラインでのインデックス操作の実行](../indexes/perform-index-operations-online.md)」を参照してください。
  
-   固定されていないインデックスがテーブルにある場合、そのパーティションの圧縮設定を変更できません。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 テーブルまたはインデックスに対する ALTER 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-enable-compression-on-a-table-or-index"></a>テーブルまたはインデックスの圧縮を有効にするには  
  
1.  オブジェクト エクスプローラーで、圧縮するテーブルを含むデータベースを展開します。次に、 **[テーブル]** フォルダーを展開します。  
  
2.  インデックスを圧縮するには、圧縮するインデックスを含むテーブルを展開します。次に、 **[インデックス]** フォルダーを展開します。  
  
3.  圧縮するテーブルまたはインデックスを右クリックし、 **[ストレージ]** をポイントして、 **[圧縮の管理]** をクリックします。  
  
4.  データ圧縮ウィザードの **[データ圧縮ウィザードへようこそ]** ページで、 **[次へ]** を選択します。  
  
5.  **[圧縮の種類の選択]** ページで、圧縮するテーブルまたはインデックスの各パーティションに適用する圧縮の種類を選択します。 完了したら **[次へ]** を選択します。  
  
     **[圧縮の種類の選択]** ページには次のオプションがあります。  
  
     **[すべてのパーティションに同じ種類の圧縮を使用する]** チェック ボックス  
     すべてのパーティションに対して同じ圧縮設定を構成する場合に選択します。 これにより、選択ボックスが有効になり、グリッドにある **[圧縮の種類]** 列が無効になります。 オンにすると、隣接するリストのオプションは、 **[なし]** 、 **[行]** 、および **[ページ]** になります。  
  
     **[パーティション番号]**  
     テーブルまたはインデックスで各パーティションを一覧表示します。 この列は読み取り専用です。  
  
     **[圧縮の種類]**  
     各パーティションの圧縮オプションを選択します。 **[すべてのパーティションに対して同じ圧縮の種類を使用]** が選択されている場合は、使用できません。 リストのオプションは、 **[なし]** 、 **[行]** 、および **[ページ]** です。  
  
     **[境界]**  
     パーティションの境界が表示されます。 この列は読み取り専用です。  
  
     **行数**  
     このパーティションの行数を表示します。 この列は読み取り専用です。  
  
     **[現在の領域]**  
     このパーティションが占有する現在の領域をメガバイト (MB) 単位で表示します。 この列は読み取り専用です。  
  
     **[要求された圧縮の領域]**  
     **[計算]** を選択した場合、この列には、 **[圧縮の種類]** 列に指定した設定を使用して圧縮後の各パーティションを推定したサイズが表示されます。 この列は読み取り専用です。  
  
     **[計算]**  
     **[圧縮の種類]** 列に指定した設定を使用して圧縮後の各パーティションのサイズを推定する場合に選択します。  
  
6.  **[出力オプションの選択]** ページで、圧縮を完了する方法を指定します。 ウィザードの前のページに基づいて SQL スクリプトを作成するには、 **[スクリプトの作成]** を選択します。 ウィザードの残りのすべてのページが完了した後に新しいパーティション テーブルを作成するには、 **[すぐに実行する]** を選択します。 事前に定義した時刻に新しいパーティション テーブルを作成するには、 **[スケジュール]** を選択します。  
  
     **[スクリプトの作成]** を選択した場合、 **[スクリプト オプション]** で次のオプションを使用できます。  
  
     **[スクリプトをファイルに保存]**  
     スクリプトを .sql ファイルとして生成します。 **[ファイル名]** ボックスにファイルの名前と場所を入力するか、 **[参照]** を選択して **[スクリプト ファイルの場所]** ダイアログ ボックスを開きます。 **[名前を付けて保存]** で、 **[Unicode テキスト]** または **[ANSI テキスト]** を選択します。  
  
     **[スクリプトをクリップボードに保存]**  
     スクリプトをクリップボードに保存します。  
  
     **[スクリプトを新しいクエリ ウィンドウに保存]**  
     新しいクエリ エディター ウィンドウにスクリプトを生成します。 これは既定値です。  
  
     **[スケジュール]** を選択した場合は、 **[スケジュールの変更]** を選択します。  
  
    1.  **[新しいジョブ スケジュール]** ダイアログ ボックスで、 **[名前]** ボックスに、ジョブのスケジュールの名前を入力します。  
  
    2.  **[スケジュールの種類]** ボックスで、スケジュールの種類を選択します。  
  
        -   **[SQL Server エージェントの開始時に自動的に開始]**  
  
        -   **[CPU がアイドル状態になったときに開始]**  
  
        -   **[定期的]** 。 新しいパーティション テーブルを新しい情報で定期的に更新するには、このオプションを選択します。  
  
        -   **[指定日時]** 。 既定では、このオプションが選択されています。  
  
    3.  **[有効]** チェック ボックスをオンまたはオフにして、スケジュールを有効または無効にします。  
  
    4.  **[定期的]** を選択した場合:  
  
        1.  **[頻度]** の **[実行]** ボックスの一覧で、実行の頻度を指定します。  
  
            -   **[日単位]** を選択した場合は、 **[間隔]** ボックスに、ジョブ スケジュールを繰り返す頻度を日単位で入力します。  
  
            -   **[週単位]** を選択した場合は、 **[間隔]** ボックスに、ジョブ スケジュールを繰り返す頻度を週単位で入力します。 ジョブ スケジュールを実行する曜日を選択します。  
  
            -   **[月単位]** を選択した場合は、 **[日]** または **[曜日]** を選択します。  
  
                -   **[日]** を選択した場合は、ジョブ スケジュールを実行する日付と、ジョブ スケジュールを繰り返す頻度を月単位で指定します。 たとえば、隔月の 15 日にジョブ スケジュールを実行する場合は、 **[日]** を選択し、1 番目のボックスに「15」と入力し、2 番目のボックスに「2」と入力します。 2 番目のボックスで使用できる最大値は "99" であることにご注意ください。  
  
                -   **[曜日]** を選択した場合は、ジョブ スケジュールを実行する曜日と、ジョブ スケジュールを繰り返す頻度を月単位で指定します。 たとえば、隔月の最後の平日にジョブ スケジュールを実行する場合は、 **[日]** を選択し、リストから **[最終]** を選択します。次に 2 番目のリストから **[平日]** を選択し、最後のボックスに「2」と入力します。 **[第 1]** 、 **[第 2]** 、 **[第 3]** 、または **[第 4]** も、特定の平日 (たとえば、日曜日や水曜日) に加えて、最初の 2 つのリストから選択できます。 最後のボックスで使用できる最大値は "99" であることにご注意ください。  
  
        2.  **[一日のうちの頻度]** で、頻度、ジョブ スケジュールを実行する当日にジョブ スケジュールを繰り返す頻度を指定します。  
  
            -   **[1 回]** を選択した場合は、ジョブ スケジュールを実行する特定の時刻を **[1 回]** ボックスに入力します。 間、分、秒に加え、午前か午後かを入力します。  
  
            -   **[間隔]** を選択した場合は、 **[頻度]** で選択した日にジョブ スケジュールを実行する頻度を指定します。 たとえば、ジョブ スケジュールを実行する当日に 2 時間おきにジョブ スケジュールを実行する場合は、 **[間隔]** を選択し、1 番目のボックスに「2」と入力してから、 **[時間]** を選択します。 このリストでは、 **[分]** と **[秒]** を選択することもできます。 1 番目のボックスで使用できる最大値は "100" であることにご注意ください。  
  
                 **[開始]** ボックスに、ジョブ スケジュールの実行を開始する時刻を入力します。 **[終了]** ボックスに、ジョブ スケジュールの実行を終了する時刻を入力します。 間、分、秒に加え、午前か午後かを入力します。  
  
        3.  **[期間]** で、 **[開始日]** に、ジョブ スケジュールの実行を開始する日付を入力します。 **[終了日]** を選択します。ジョブ スケジュールの実行を停止するタイミングを指定しない場合は、 **[終了日なし]** を選択します。 **[終了日]** を選択した場合は、ジョブ スケジュールの実行を停止する日付を入力します。  
  
    5.  **[指定日時]** を選択した場合は、 **[指定日時に発生]** の **[日付]** ボックスに、ジョブ スケジュールを実行する日付を入力します。 **[時刻]** ボックスに、ジョブ スケジュールを実行する時刻を入力します。 間、分、秒に加え、午前か午後かを入力します。  
  
    6.  **[概要]** の **[説明]** で、すべてのジョブ スケジュール設定が適切であることを確認します。  
  
    7.  **[OK]** を選択します。  
  
     このページを完了したら、 **[次へ]** を選択します。  
  
7.  **[概要の確認]** ページの **[選択内容の確認]** で、使用可能なすべてのオプションを展開し、すべての圧縮設定が適切であることを確認します。 すべての設定が適切であることを確認したら、 **[完了]** を選択します。  
  
8.  **[圧縮ウィザードの進行状況]** ページで、パーティションの作成ウィザードの操作に関する状態情報を監視します。 ウィザードで選択したオプションに応じて、[進行状況] ページに 1 つまたは複数のアクションが含まれる可能性があります。 上部のボックスには、ウィザードの全体的な状態と受信した状態メッセージ、エラー メッセージ、および警告メッセージの数が表示されます。  
  
     **[圧縮ウィザードの進行状況]** ページでは、次のオプションを使用できます。  
  
     **詳細**  
     アクション、状態、およびウィザードで実行したアクションから返されたメッセージが提供されます。  
  
     **操作**  
     各アクションの種類と名前を指定します。  
  
     **状態**  
     全体としてウィザードのアクションが **[成功]** または **[失敗]** のいずれの値を返したかを示します。  
  
     **メッセージ**  
     プロセスから返されたすべてのエラー メッセージまたは警告メッセージを提供します。  
  
     **Report**  
     パーティションの作成ウィザードの結果を含むレポートを作成します。 **[レポートの表示]** 、 **[レポートをファイルに保存]** 、 **[レポートをクリップボードにコピー]** 、 **[レポートを電子メールとして送信]** の各オプションがあります。  
  
     **[レポートの表示]**  
     パーティションの作成ウィザードの進行状況に関するテキスト レポートを表示する **[レポートの表示]** ダイアログ ボックスを開きます。  
  
     **[レポートをファイルに保存]**  
     **[レポートに名前を付けて保存]** ダイアログ ボックスを開きます。  
  
     **[レポートをクリップボードにコピー]**  
     ウィザードの進行状況レポートの結果をクリップボードにコピーします。  
  
     **[レポートを電子メールとして送信]**  
     ウィザードの進行状況レポートの結果を電子メール メッセージにコピーします。  
  
     完了したら、 **[閉じる]** を選択します。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  

### <a name="sql-server"></a>SQL Server

SQL Server で、`sp_estimate_data_compression_savings` を実行してから、テーブルまたはインデックスの圧縮を有効にします。 以下のセクションをご覧ください。 

#### <a name="to-enable-compression-on-a-table"></a>テーブルで圧縮を有効にするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  標準バーで、 **[新しいクエリ]** を選択します。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** を選択します。 この例では、最初にストアド プロシージャ `sp_estimate_data_compression_savings` を実行して、行の圧縮設定を使用した場合のオブジェクトの推定サイズを返します。 次に、指定したテーブルのすべてのパーティションで行の圧縮を有効にします。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_estimate_data_compression_savings 'Production', 'TransactionHistory', NULL, NULL, 'ROW' ;  
  
    ALTER TABLE Production.TransactionHistory REBUILD PARTITION = ALL  
    WITH (DATA_COMPRESSION = ROW);   
    GO  
    ```  
  
#### <a name="to-enable-compression-on-an-index"></a>インデックスで圧縮を有効にするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  標準バーで、 **[新しいクエリ]** を選択します。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** を選択します。 この例では、最初に `sys.indexes` カタログ ビューを問い合わせて、 `index_id` テーブルの各インデックスの名前と `Production.TransactionHistory` を返します。 次に、ストアド プロシージャ `sp_estimate_data_compression_savings` を実行して、ページの圧縮設定を使用した場合の指定されたインデックス ID の推定サイズを返します。 最後に、インデックス ID 2 (`IX_TransactionHistory_ProductID`) を再構築し、ページの圧縮を指定します。  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, index_id  
    FROM sys.indexes  
    WHERE OBJECT_NAME (object_id) = N'TransactionHistory';  
  
    EXEC sp_estimate_data_compression_savings   
        @schema_name = 'Production',   
        @object_name = 'TransactionHistory',  
        @index_id = 2,   
        @partition_number = NULL,   
        @data_compression = 'PAGE' ;   
  
    ALTER INDEX IX_TransactionHistory_ProductID ON Production.TransactionHistory REBUILD PARTITION = ALL WITH (DATA_COMPRESSION = PAGE);  
    GO  
    ``` 
    
### <a name="on-azure-sql-database"></a>Azure SQL Database 上

Azure SQL Database データベースでは、`sp_estimate_data_compression_savings` ストアド プロシージャはサポートされていません。 次のスクリプトでは、圧縮率を推定せずに圧縮を行うことができます。 

#### <a name="to-enable-compression-on-a-table"></a>テーブルで圧縮を有効にするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  標準バーで、 **[新しいクエリ]** を選択します。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** を選択します。 この例では、指定したテーブルのすべてのパーティションで行の圧縮を有効にします。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  

    ALTER TABLE Production.TransactionHistory REBUILD PARTITION = ALL  
    WITH (DATA_COMPRESSION = ROW);   
    GO  
    ```  
  
#### <a name="to-enable-compression-on-an-index"></a>インデックスで圧縮を有効にするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  標準バーで、 **[新しいクエリ]** を選択します。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** を選択します。 この例では、最初に `sys.indexes` カタログ ビューを問い合わせて、 `index_id` テーブルの各インデックスの名前と `Production.TransactionHistory` を返します。 最後に、インデックス ID 2 (`IX_TransactionHistory_ProductID`) を再構築し、ページの圧縮を指定します。  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, index_id  
    FROM sys.indexes  
    WHERE OBJECT_NAME (object_id) = N'TransactionHistory';  
    
    ALTER INDEX IX_TransactionHistory_ProductID ON Production.TransactionHistory REBUILD PARTITION = ALL WITH (DATA_COMPRESSION = PAGE);  
    GO  
    ``` 
  
 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」および「[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データの圧縮](../../relational-databases/data-compression/data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)  
  
  
