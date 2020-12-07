---
title: 移行ガイド:DB2 から SQL Server
description: このガイドに従って、DB2 サーバーを SQL Server に移行します。
ms.custom: ''
ms.date: 08/17/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4a4aa024d94908800c020fdc5d2362d48d03becd
ms.sourcegitcommit: b09f069c6bef0655b47e9953a4385f1b52bada2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92734666"
---
# <a name="migration-guide-db2-to-sql-server"></a>移行ガイド:DB2 から SQL Server
[!INCLUDE[sqlserver](../../../includes/applies-to-version/sqlserver.md)]

この移行ガイドでは、SQL Server Migration Assistant for DB2 を使用して、ユーザー データベースを DB2 から SQL Server に移行する方法について説明します。 

その他の移行ガイドについては、[データベースの移行](https://datamigration.microsoft.com/)に関するページを参照してください。 


## <a name="prerequisites"></a>前提条件

DB2 データベースを SQL Server に移行するには、以下が必要です。

- ソース環境がサポートされていることを確認する。
- [SQL Server Migration Assistant (SSMA) for DB2](https://www.microsoft.com/download/details.aspx?id=54254)。



## <a name="pre-migration"></a>移行前

前提条件を満たすと、環境のトポロジを検出し、移行の可能性を評価する準備は完了です。 

### <a name="assess"></a>アクセス 

SQL Server Migration Assistant (SSMA) を使用して評価を作成します。 

評価を作成するには、次の手順を行います。

1. SQL Server Migration Assistant (SSMA) for DB2 を開きます。 
1. **[ファイル]** を選択し、 **[新しいプロジェクト]** を選択します。 
1. プロジェクト名とプロジェクトを保存する場所を指定し、ドロップダウンから SQL Server 移行ターゲットを選択します。 **[OK]** を選択します。 

   :::image type="content" source="media/db2-to-sql-server/new-project.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::


1. **[DB2 への接続]** ダイアログ ボックスで、DB2 接続の詳細の値を入力します。 

   :::image type="content" source="media/db2-to-sql-server/connect-to-db2.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::


1. 移行する DB2 スキーマを右クリックし、 **[レポートの作成]** を選択します。 これにより、HTML レポートが生成されます。 また、スキーマを選択した後、ナビゲーション バーから **[レポートの作成]** を選択することもできます。 

   :::image type="content" source="media/db2-to-sql-server/create-report.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. HTML レポートを確認し、変換の統計情報とエラーまたは警告を把握します。 また、Excel でレポートを開き、DB2 オブジェクトのインベントリとスキーマ変換の実行に必要な作業量を確認することもできます。 レポートの既定の場所は、SSMAProjects 内のレポート フォルダーです。

   (例: `drive:\<username>\Documents\SSMAProjects\MyDB2Migration\report\report_<date>`)。 

   :::image type="content" source="media/db2-to-sql-server/report.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::


### <a name="validate-data-types"></a>データ型を検証する

既定のデータ型マッピングを検証し、必要に応じて要件に基づいて変更します。 これを行うには、次のステップに従います。 

1. メニューから **[ツール]** を選択します。 
1. **[プロジェクトの設定]** を選択します。 
1. **[Type mappings]\(型のマッピング\)** タブを選択します。 

   :::image type="content" source="media/db2-to-sql-server/type-mapping.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. **DB2 メタデータ エクスプローラー** でテーブルを選択することにより、各テーブルの型マッピングを変更できます。 

### <a name="convert-schema"></a>スキーマの変換 

スキーマを変換するには、次の手順を行います。

1. (省略可能) 動的またはアドホック クエリをステートメントに追加します。 ノードを右クリックし、 **[Add statements]\(ステートメントの追加\)** を選択します。 
1. **[SQL Server への接続]** を選択します。 
    1. 接続の詳細を入力して、SQL Server インスタンスに接続します。 
    1. ターゲット サーバー上の既存のデータベースに接続するか、新しい名前を指定してターゲット サーバー上に新しいデータベースを作成するかを選択します。 
    1. **[接続]** を選択します。 

   :::image type="content" source="media/db2-to-sql-server/connect-to-sql-server.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::


1. スキーマを右クリックして、 **[スキーマの変換]** を選択します。 または、スキーマを選択した後、上部のナビゲーション バーから **[スキーマの変換]** を選択することもできます。 

   :::image type="content" source="media/db2-to-sql-server/convert-schema.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. 変換が完了したら、スキーマの構造を比較し、確認して、潜在的な問題を特定し、推奨事項に基づいて対処します。 

   :::image type="content" source="media/db2-to-sql-server/compare-review-schema-structure.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. オフライン スキーマ修復の演習のために、プロジェクトをローカルに保存します。 **[ファイル]** メニューから **[プロジェクトの保存]** を選択します。 


## <a name="migrate"></a>Migrate

データベースの評価と不整合への対処が完了したら、次の手順は移行プロセスの実行です。

スキーマを発行し、データを移行するには、次の手順を行います。

1. スキーマを発行する: **SQL Server メタデータ エクスプローラー** の **[データベース]** ノードからデータベースを右クリックし、 **[データベースとの同期]** を選択します。

   :::image type="content" source="media/db2-to-sql-server/synchronize-with-database.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. データを移行する: **DB2 メタデータ エクスプローラー** からスキーマを右クリックし、 **[データの移行]** を選択します。 

   :::image type="content" source="media/db2-to-sql-server/migrate-data.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. DB2 インスタンスと SQL Server インスタンスの両方の接続の詳細を指定します。 
1. **データ移行レポート** を確認します。 

   :::image type="content" source="media/db2-to-sql-server/data-migration-report.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

1. SQL Server Management Studio を使用して SQL Server インスタンスに接続し、データとスキーマを確認して移行を検証します。 

   :::image type="content" source="media/db2-to-sql-server/compare-schema-in-ssms.png" alt-text="プロジェクトの詳細を入力し、[OK] を選択して保存します。":::

## <a name="post-migration"></a>移行後 

移行段階が正常に完了したら、移行後の一連のタスクを実行し、確実にすべてが可能な限り円滑かつ効率的に機能するようにする必要があります。

### <a name="remediate-applications"></a>アプリケーションを修復する 

データがターゲット環境に移行された後、以前にソースを使用していたすべてのアプリケーションは、ターゲットの使用を開始する必要があります。 これを実現するには、場合によってはアプリケーションの変更が必要になります。

### <a name="perform-tests"></a>テストを実行する

データベース移行のテストア プローチは、次のアクティビティで構成されています。

1. **検証テストを作成する** : データベースの移行をテストするには、SQL クエリを使用する必要があります。 ソース データベースとターゲット データベースの両方に対して実行する検証クエリを作成する必要があります。 検証クエリには、定義したスコープが含まれている必要があります。
1. **テスト環境を設定する** : テスト環境には、ソース データベースとターゲット データベースのコピーが含まれている必要があります。 必ずテスト環境を分離してください。
1. **検証テストを実行する** : ソースとターゲットに対して検証テストを実行してから、結果を分析します。
1. **パフォーマンス テストを実行する** : ソースとターゲットに対してパフォーマンス テストを実行し、結果を分析して比較します。

   > [!NOTE]
   > 移行後の検証テストの開発と実行を支援するために、パートナーの [QuerySurge](https://www.querysurge.com/company/partners/microsoft) から入手できる Data Quality Solution を検討してください。 

## <a name="migration-assets"></a>移行資産 

詳細については、次のリソースを参照してください。これらは、実際の移行プロジェクトの取り組みをサポートするために開発されました。

|Asset  |説明  |
|---------|---------|
|[データ ワークロード評価モデルとツール](https://github.com/Microsoft/DataMigrationTeam/tree/master/Data%20Workload%20Assessment%20Model%20and%20Tool)| このツールを使用すると、特定のワークロードに対して、推奨される "最適な" ターゲット プラットフォーム、クラウドの準備状況、アプリケーションとデータベースの修復レベルがわかります。 シンプルなワンクリックの計算とレポート生成機能があり、自動化された均一なターゲット プラットフォームの決定プロセスが用意されているので、大規模な不動産評価を加速させることができます。|
|[DB2 zOS データ資産の検出および評価パッケージ](https://github.com/Microsoft/DataMigrationTeam/tree/master/DB2%20zOS%20Data%20Assets%20Discovery%20and%20Assessment%20Package)|データベース上で SQL スクリプトを実行した後、結果をファイル システム上のファイルにエクスポートできます。 スプレッドシートなど、外部ツールで結果をキャプチャできるように、*.csv などの複数のファイル形式がサポートされています。 この方法を使用すると、ワークベンチをインストールしていないチームと結果を簡単に共有することができます。|
|[IBM DB2 LUW インベントリ スクリプトと成果物](https://github.com/Microsoft/DataMigrationTeam/tree/master/IBM%20DB2%20LUW%20Inventory%20Scripts%20and%20Artifacts)|この資産には、IBM DB2 LUW バージョン 11.1 システム テーブルにヒットし、スキーマおよびオブジェクトの種類ごとのオブジェクトの数、各スキーマの "生データ" の概算値、および各スキーマのテーブルのサイズを提供し、結果を CSV 形式で格納する SQL クエリが含まれます。|
|[Azure 上の DB2 LUW pureScale - 設定ガイド](https://github.com/Microsoft/DataMigrationTeam/blob/master/Whitepapers/DB2%20PureScale%20on%20Azure.pdf)|このガイドは、DB2 実装計画の開始点として役立ちます。 業務要件は違っても、同じ基本パターンが適用されます。 このアーキテクチャ パターンは、Azure 上の OLAP アプリケーションにも使用できます。|

これらのリソースは、Azure Data Group エンジニアリング チームがスポンサーである Data SQL Ninja プログラムの一部として開発されました。 Data SQL Ninja プログラムの中核となるのは、複雑なモダン化のブロックを解除して加速し、データ プラットフォームを Microsoft の Azure Data プラットフォームに移行する機会を獲得することです。 組織が Data SQL Ninja プログラムへの参加に関心があると思われる場合は、アカウント チームに連絡し、申請を提出するよう依頼してください。

## <a name="next-steps"></a>次の手順

移行後は、[移行後の検証と最適化ガイド](../../../relational-databases/post-migration-validation-and-optimization-guide.md)を確認してください。 

さまざまなデータベースとデータの移行シナリオ、および特殊なタスクを支援するために使用できる Microsoft とサードパーティのサービスとツールのマトリックスについては、[データ移行サービスとツール](/azure/dms/dms-tools-matrix)に関するページを参照してください。

その他の移行ガイドについては、[データベースの移行](https://datamigration.microsoft.com/)に関するページを参照してください。 

ビデオ コンテンツについては、以下をご覧ください。
- [データベース移行ガイドを使用する方法](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/)
- [移行の過程の概要](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/)
