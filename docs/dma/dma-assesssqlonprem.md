---
title: SQL Server 移行の評価を実行する
titleSuffix: Data Migration Assistant
description: Data Migration Assistant を使用して、別の SQL Server またはに移行する前に、オンプレミスの SQL Server を評価する方法について説明し Azure SQL Database
ms.date: 01/15/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 5c0ddd9aa7c89f7f77212155a0b85089c34087d9
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726302"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Data Migration Assistant を使用した SQL Server 移行評価の実行

次の手順に従って、オンプレミスの SQL Server に移行するための最初の評価、Azure VM での SQL Server 実行、または Data Migration Assistant を使用した Azure SQL Database を行うことができます。

   > [!NOTE]
   > Data Migration Assistant v1.0 では、アプリケーションコードでデータベース接続と埋め込み SQL クエリを分析するためのサポートが導入されています。 詳細については、 [Data Migration Assistant を使用したアプリケーションのデータアクセス層の評価に](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)関するブログ記事を参照してください。

## <a name="create-an-assessment"></a>評価を作成する

1. [ **新規** ] (+) アイコンを選択し、[ **評価** ] プロジェクトの種類を選択します。

2. ソースとターゲットのサーバーの種類を設定します。

    オンプレミスの SQL Server インスタンスを最新のオンプレミスの SQL Server インスタンスにアップグレードする場合、または Azure VM でホストされている SQL Server にアップグレードする場合は、ソースとターゲットのサーバーの種類を **SQL Server**に設定します。 Azure SQL Database に移行している場合は、代わりに対象サーバーの種類を **Azure SQL Database**に設定します。

3. **Create** をクリックしてください。

   ![評価を作成する](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>評価オプションの選択

1. 移行を計画するターゲット SQL Server バージョンを選択します。

2. レポートの種類を選択します。

   オンプレミスの SQL Server または Azure VM ターゲットでホストされている SQL Server に移行するためにソース SQL Server インスタンスを評価する場合は、次のいずれかまたは両方の評価レポートの種類を選択できます。

    - **互換性の問題**
    - **新機能の推奨事項**

   ![SQL Server ターゲットの評価レポートの種類を選択します](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Azure SQL Database に移行するためにソース SQL Server インスタンスを評価する場合は、次のいずれかまたは両方の評価レポートの種類を選択できます。

    - **データベース互換性をチェックする**
    - **機能の類似性をチェックする**

    ![SQL Database ターゲットの評価レポートの種類を選択します](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>評価するデータベースと拡張イベントトレースの追加

1. [ **ソースの追加** ] を選択して、接続のフライアウトメニューを開きます。

2. SQL server インスタンス名を入力し、認証の種類を選択して、適切な接続プロパティを設定し、[ **接続**] を選択します。

3. 評価するデータベースを選択し、[ **追加**] を選択します。

    > [!NOTE]
    > 複数のデータベースを削除するには、Shift キーまたは Ctrl キーを押しながら選択し、[ **ソースの削除**] をクリックします。 また、[ **ソースの追加**] を選択して、複数の SQL Server インスタンスからデータベースを追加することもできます。

4. アドホックまたは動的 SQL クエリ、またはアプリケーションデータレイヤーを介して開始された DML ステートメントがある場合は、収集したすべての拡張イベントセッションファイルを配置したフォルダーへのパスを入力して、ソース SQL Server のワークロードをキャプチャします。

     次の例は、ソース SQL Server で拡張イベントセッションを作成して、アプリケーションデータレイヤーのワークロードをキャプチャする方法を示しています。  ピーク時のワークロードを表す期間のワークロードをキャプチャします。

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. **[次へ]** をクリックして評価を開始します。

    ![ソースを追加して評価を開始する](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> 複数の評価を同時に実行し、**[All Assessments]\(すべての評価\)** ページを開いて評価の状態を表示できます。

## <a name="view-results"></a>結果の表示

評価期間は、追加されたデータベースの数と各データベースのスキーマサイズによって異なります。 結果は、データベースが使用可能になるとすぐに表示されます。

1. 評価が完了したデータベースを選択し、スイッチャーを使用して **互換性の問題** と **機能に関する推奨事項** を切り替えます。

2. [ **オプション** ] ページで選択したターゲット SQL Server バージョンでサポートされているすべての互換性レベルで、互換性の問題を確認します。

互換性の問題を確認するには、影響を受けるオブジェクト、その詳細、および **重大な変更**、 **動作の変更**、および **非推奨の機能**で特定されたすべての問題に対する修正プログラムを分析します。

![評価結果の表示](../dma/media/dma-assesssqlonprem/review-results.png)

同様に、 **パフォーマンス**、 **ストレージ**、 **セキュリティ** の各領域で、機能の推奨事項を確認することもできます。

機能に関する推奨事項は、インメモリ OLTP、列ストア、Stretch Database、Always Encrypted、動的データマスク、Transparent Data Encryption などのさまざまな機能に対応しています。

![機能に関する推奨事項の表示](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Azure SQL Database の場合、評価によって、移行のブロックの問題と機能のパリティの問題が発生します。特定のオプションを選択して、両方のカテゴリの結果を確認します。

- **SQL Server 機能のパリティ**カテゴリは、一連の推奨事項、Azure で利用可能な別のアプローチ、および手順の軽減を提供します。 これは、移行プロジェクトでこの作業を計画するのに役立ちます。

  ![SQL Server 機能のパリティに関する情報の表示](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- **互換性の問題**カテゴリには、オンプレミスの SQL Server データベースを Azure SQL データベースに移行できない部分的にサポートされている機能やサポートされていない機能があります。その後、これらの問題に対処するための推奨事項を提供します。

  ![互換性の問題の表示](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>ターゲット準備のためにデータ資産を評価する

これらの評価をデータ資産全体にさらに拡張し、Azure SQL Database への移行用に SQL Server インスタンスとデータベースの相対的な準備を確認する場合は、[ **Azure Migrate にアップロード**] を選択して Azure Migrate ハブに結果をアップロードします。

これにより、Azure Migrate hub プロジェクトで統合された結果を表示できるようになります。

ターゲット準備評価の詳細なステップバイステップガイダンスについては、 [こちら](./dma-assess-sql-data-estate-to-sqldb.md?view=sql-server-2017)を参照してください。

   ![結果を Azure Migrate にアップロードする](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>結果のエクスポート

すべてのデータベースで評価が完了したら、[ **レポートのエクスポート** ] を選択して、結果を JSON ファイルまたは CSV ファイルにエクスポートします。 その後、データを独自の便利な方法で分析できます。

## <a name="save-and-load-assessments"></a>評価の保存と読み込み

評価の結果をエクスポートするだけでなく、評価の詳細をファイルに保存し、評価ファイルを読み込んで後で確認することもできます。  詳細については、「 [Data Migration Assistant を使用した保存と読み込みの評価](../dma/dma-save-load-assessments.md)」を参照してください。