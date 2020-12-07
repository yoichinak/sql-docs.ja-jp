---
title: 統計
description: クエリ オプティマイザーでは、クエリのパフォーマンスを向上させるクエリ プランを作成するために統計を使用します。 クエリ最適化を使用するための概念とガイドラインについて説明します。
ms.custom: ''
ms.date: 11/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1374be401f379dceb73a41f7a4e2f38882a9a98c
ms.sourcegitcommit: f2bdebed3efa55a2b7e64de9d6d9d9b1c85f479e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "96130174"
---
# <a name="statistics"></a>統計

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  クエリ オプティマイザーでは、クエリのパフォーマンスを向上させるクエリ プランを作成するために統計を使用します。 ほとんどのクエリでは、高品質のクエリ プランに必要な統計がクエリ オプティマイザーによって既に生成されていますが、最適な結果を得るために追加の統計情報を作成したり、クエリのデザインを変更したりする必要がある場合もあります。 このトピックでは、クエリ最適化に関する統計の概念と、それを効果的に使用するためのガイドラインについて説明します。  
  
##  <a name="components-and-concepts"></a><a name="DefinitionQOStatistics"></a> コンポーネントおよび概念  
### <a name="statistics"></a>統計  
 クエリ最適化に関する統計は、テーブルまたはインデックス付きビューの 1 つまたは複数の列の値の分布に関する統計情報を格納するバイナリ ラージ オブジェクト (BLOB) です。 クエリ オプティマイザーでは、これらの統計を使用してクエリ結果の *カーディナリティ*、つまり行数を推定します。 これらの *カーディナリティの推定* に基づいて、クエリ オプティマイザーでは高品質なクエリ プランを作成できます。 たとえば、ご利用の述語によっては、クエリ オプティマイザーがカーディナリティの推定を使用して、リソース消費の多い Index Scan 操作ではなく Index Seek 操作を選択することがあります。そうすることで、クエリのパフォーマンスが高まります。  
  
 統計オブジェクトは 1 つ以上のテーブル列で構成されるリストごとに作成され、それぞれに最初の列の値の分布を示す *ヒストグラム* が含まれます。 複数列の統計オブジェクトには、さらに、列間の値の相関関係に関する統計情報も格納されます。 これらの相関関係の統計情報 ( *密度*) は、個別の列値を持つ行の数から得られます。 

#### <a name="histogram"></a><a name="histogram"></a> ヒストグラム  
**ヒストグラム** では、データセットの個別の値ごとに出現頻度を測定します。 クエリ オプティマイザーでは、統計オブジェクトの最初のキー列の列値に基づいてヒストグラムを計算し、行を統計的にサンプリングするかテーブルまたはビュー内のすべての行でフル スキャンを実行することによって列値を選択します。 サンプリングされた行のセットからヒストグラムを作成する場合、格納される行の総数および個別の値の数は推定値であり、必ずしも整数にはなりません。

> [!NOTE]
> <a name="frequency"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のヒストグラムは、単一の列 (統計オブジェクトのキー列のセットの最初の列) に対してのみ作成されます。
  
ヒストグラムを作成するには、クエリ オプティマイザーで列値を並べ替え、個別の列値ごとに一致する値の数を計算し、列値を最大 200 の連続したヒストグラム区間に集計します。 各ヒストグラム区間には、列値の範囲と上限の列値が順番に含まれます。 この範囲には、境界値の間 (境界値自体は除く) のすべての有効な列値が含まれます。 格納される最小の列値は、最初のヒストグラム区間の上限境界値になります。

具体的には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の 3 つの区間で、並べ替えられた列値のセットから **ヒストグラム** を作成します。

- **ヒストグラムの初期化**:最初の区間で、並べ替えられたセットの先頭から始まる値のシーケンスが処理され、*range_high_key*、*equal_rows*、*range_rows*、*distinct_range_rows* の最大 200 個の値が収集されます (この区間の間、*range_rows* と *distinct_range_rows* は常にゼロです)。 最初の区間は、すべての入力が使用されたとき、または 200 個の値が見つかったときに終了します。 
- **バケットのマージを使用したスキャン**:2 つ目の手順では、統計キーの先頭の列から追加された各値が並び順で処理されます。連続する各値は最後の範囲に追加されるか、末尾に新しい範囲が作成されます (これは、入力値が並べ替えられているため可能です)。 新しい範囲が作成されると、既存の隣接する範囲の 1 組が 1 つの範囲に折りたたまれます。 情報の損失を最小限に抑えるために、この範囲の組が選択されます。 この方法では、*区間幅を最大にする* アルゴリズムを使用して境界値の差を最大にし、ヒストグラムの区間の数を最小限に抑えます。 範囲を折りたたんだ後の手順の数は、この手順全体で 200 個のままです。
- **ヒストグラムの統合**:3 番目の区間では、失われる情報の量が少なければ、より多くの範囲が折りたたまれる可能性があります。 ヒストグラムの区間の数は、境界点が 200 より少ない列でも、個別の値の数より少なくなることがあります。 そのため、列に 200 を超える一意の値が含まれていても、ヒストグラムの区間の数は 200 未満となることがあります。 一意の値のみで構成される列の場合、統合されたヒストグラムには最小で 3 つの区間が存在します。

> [!NOTE]
> fullscan ではなくサンプルを使用してヒストグラムが作成されている場合、*equal_rows*、*range_rows*、*distinct_range_rows*、*average_range_rows* の値は推定されます。そのため、これらの値は整数である必要はありません。

次の図は、6 つの区間があるヒストグラムを示しています。 最初の上限境界値の左側にある領域が最初の区間です。
  
![ヒストグラム](../../relational-databases/system-dynamic-management-views/media/histogram-2.svg "ヒストグラム") 
  
上記のヒストグラムの各区間は、以下のように表されます。
-   太線は、上限境界値 (*range_high_key*) およびその出現回数 (*equal_rows*) を表します。  
  
-   *range_high_key* の左にある領域は、列値の範囲、およびそれぞれの列値の平均出現回数 (*average_range_rows*) を表します。 最初のヒストグラム区間の *average_range_rows* は常に 0 です。  
  
-   点線は、範囲内にある個別の値の総数 (*distinct_range_rows*) および範囲内の値の総数 (*range_rows*) を推定するために使用されるサンプリングされた値を表します。 クエリ オプティマイザーでは、*range_rows* および *distinct_range_rows* を使用して *average_range_rows* を計算します。サンプリングされた値は格納されません。   
  
#### <a name="density-vector"></a><a name="density"></a>密度ベクトル  
**密度** とは、特定の列または列の組み合わせにおける重複の数に関する情報であり、1/(個別の値の数) の式で計算されます。 クエリ オプティマイザーでは、同一のテーブルまたはインデックス付きビューから複数の列を返すクエリに対するカーディナリティの推定を向上させるために密度を使用します。 密度が減少するにつれて、値の選択度が高くなります。 たとえば、車を表すテーブルの場合、同メーカーの車がいくつもあります。ただし、VIN (車両番号) はそれぞれの車両固有のものです。 VIN 上のインデックスは、製造元でのインデックスより選択度が高くなります。これは VIN の密度が製造元の場合より低いからです。 

> [!NOTE]
> 頻度とは、統計オブジェクトの最初のキー列における各個別値の発生に関する情報であり、"行数 * 密度" の式で計算されます。 最大頻度 1 は、一意の値を持つ列で確認できます。

密度ベクトルには、統計オブジェクトの列のプレフィックスごとに 1 つの密度が格納されます。 たとえば、統計オブジェクトに `CustomerId`、`ItemId`、`Price` というキー列がある場合、以下の列プレフィックスごとに密度が計算されます。
  
|列プレフィックス|密度の計算対象|  
|---|---|
|(CustomerId)|CustomerId の値が一致する行|  
|(CustomerId, ItemId)|CustomerId および ItemId の値が一致する行|  
|(CustomerId, ItemId, Price)|CustomerId、ItemId、および Price の値が一致する行| 

### <a name="filtered-statistics"></a>フィルター選択された統計情報  
 適切に定義されたデータのサブセットから選択するクエリでは、フィルター選択された統計情報を使用するとクエリのパフォーマンスを向上させることができます。 フィルター選択された統計情報では、統計情報に含まれるデータのサブセットを選択するためにフィルター述語を使用します。 統計情報を適切にフィルター選択すると、テーブル全体の統計情報を使用する場合と比べて、クエリ実行プランが向上します。 フィルター述語の詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。 フィルター選択された統計情報を作成する場合の詳細については、このトピックの「 [統計を作成する場合](#CreateStatistics) 」を参照してください。  
 
### <a name="statistics-options"></a>統計オプション  
 統計の作成と更新のタイミングおよび方法を指定するための 3 つのオプションを設定できます。 これらのオプションは、データベース レベルでのみ設定されます。  
  
#### <a name="auto_create_statistics-option"></a><a name="AutoUpdateStats"></a>AUTO_CREATE_STATISTICS オプション  
 統計の自動作成オプション [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) がオンの場合、クエリ プランのカーディナリティの推定を向上させるために、クエリ オプティマイザーによってクエリ述語内の個々の列に関する統計が必要に応じて作成されます。 これらの 1 列ずつの統計は、既存の統計オブジェクトにまだ[ヒストグラム](#histogram)がない列について作成されます。 AUTO_CREATE_STATISTICS オプションでは、インデックスに対する統計を作成するかどうかは判断されません。 また、フィルター選択された統計情報も生成されません。 このオプションは、テーブル全体の 1 列ずつの統計にのみ適用されます。  
  
 AUTO_CREATE_STATISTICS オプションを使用した結果としてクエリ オプティマイザーによって統計が作成された場合、その統計名は `_WA` で始まります。 次のクエリを使用すると、クエリ オプティマイザーでクエリ述語列の統計が作成されたかどうかを判断できます。  
  
```sql  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s 
INNER JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
#### <a name="auto_update_statistics-option"></a>AUTO_UPDATE_STATISTICS オプション  
 統計の自動更新オプション [AUTO_UPDATE_STATISTICS ](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) がオンの場合、古くなっている可能性がある統計がクエリ オプティマイザーによって判断され、それらがクエリで使用されると更新されます。 挿入、更新、削除、またはマージの各操作によってテーブルまたはインデックス付きビューのデータの分布が変わると、統計は古くなったと判断されます。 クエリ オプティマイザーでは、統計が前回更新されてから発生したデータ変更の数をカウントし、その変更の数をしきい値と比較することで、統計が古くなっている可能性がないかを判断します。 このしきい値は、テーブルまたはインデックス付きビューの行数に基づいて決められます。  
  
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] まで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は変更された行の割合に基づくしきい値を使用します。 これには、テーブル内の行数は考慮されません。 しきい値は次のようになります。
    * 統計情報が評価された時点でテーブルのカーディナリティが 500 以下の場合、500 回変更されるたびに更新されます。
    * 統計情報が評価された時点でテーブルのカーディナリティが 500 よりも大きい場合、500 プラス 20% の数の変更があるたびに更新されます。

* [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降で、[データベースの互換性レベル](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)が 130 未満の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、テーブル内の行数に基づいて調整された、より小さな値の動的な統計情報更新しきい値を使用します。 これは、1,000 と現在のテーブルのカーディナリティの積の平方根として計算されます。 たとえば、テーブルに 200 万行含まれている場合、計算は sqrt(1000 * 2000000) = 44721.359 となります。 この変更により、大規模なテーブルの統計がより頻繁に更新されます。 ただし、データベースの互換性レベルが 130 未満の場合、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のしきい値が適用されます。 ?

> [!IMPORTANT]
> [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、または [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降の[データベース互換性レベル](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 120 以下では、[トレース フラグ 2371](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を有効にして、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で低下した動的統計更新しきい値が使用されるようにします。

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] より前の環境でトレース フラグ 2371 を有効にするには、次のガイダンスを使用できます。

 - 古い統計が原因でパフォーマンスの問題が発生していない場合は、このトレース フラグを有効にする必要はありません。
 - SAP システムを使用している場合は、このトレース フラグを有効にします。  その他の情報については、こちらの[ブログ](/archive/blogs/saponsqlserver/changes-to-automatic-update-statistics-in-sql-server-traceflag-2371)を参照してください。
 - 現在の自動更新が十分頻繁にトリガーされないため、夜間ジョブを使用して統計を更新する必要がある場合は、トレース フラグ 2371 を有効にしてしきい値を小さくすることを検討します。
  
クエリ オプティマイザーによる古い統計の確認は、クエリをコンパイルする前と、キャッシュされたクエリ プランを実行する前に行われます。 クエリをコンパイルする前は、クエリ オプティマイザーで、クエリ述語内の列、テーブル、およびインデックス付きビューを使用して古くなっている可能性がある統計が判断されます。 キャッシュされたクエリ プランを実行する前は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で、クエリ プランが最新の統計を参照しているかどうかが確認されます。  
  
AUTO_UPDATE_STATISTICS オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) ステートメントを使用して作成された統計に適用されます。 また、フィルター選択された統計情報にも適用されます。  
 
[sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) を使用すると、テーブルで変更された行数を正確に追跡し、統計を手動で更新するかどうかを判断できます。



  
#### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC  
統計の非同期更新オプション [AUTO_UPDATE_STATISTICS_ASYNC](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics_async) によって、クエリ オプティマイザーで統計の同期更新と非同期更新のどちらを使用するかが決まります。 既定では、統計の非同期更新オプションはオフであり、クエリ オプティマイザーによる統計の更新は同期更新になります。 AUTO_UPDATE_STATISTICS_ASYNC オプションは、インデックスに対して作成された統計オブジェクト、クエリ述語内の列に対して 1 列ずつ作成された統計オブジェクト、および [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) ステートメントを使用して作成された統計に適用されます。  
 
> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の *[データベースのプロパティ]* ウィンドウの *[オプション]* ページで統計の非同期更新オプションを設定するには、 *[統計の自動更新]* と *[統計の非同期的自動更新]* の両方のオプションを **True** に設定する必要があります。
  
統計の更新には、同期更新 (既定) と非同期更新があります。 統計の同期更新では、クエリは常に最新の統計を使用してコンパイルおよび実行されます。統計が古い場合、クエリ オプティマイザーでは、統計が更新されるまでクエリのコンパイルおよび実行を待機します。 統計の非同期更新では、クエリは、既存の統計が古い場合でもその統計を使用してコンパイルされます。クエリのコンパイル時に古い統計が使用された場合、クエリ オプティマイザーで最適なクエリ プランが選択されない可能性があります。 非同期更新の完了後にコンパイルされるクエリには、更新された統計を使用できます。  
  
テーブルの切り捨てや大部分の行の一括更新を行うなど、データの分布が変わる操作を実行する場合は、同期統計を使用することを検討してください。 操作が完了した後に統計を更新していない場合、同期統計を使用すれば、変更されたデータに対するクエリを実行する前に統計が最新になります。  
  
次のような場合は、非同期統計を使用してクエリの応答時間を予測しやすくすることを検討してください。  
  
* アプリケーションで同じクエリ、類似のクエリ、またはキャッシュされた類似のクエリ プランを頻繁に実行する場合。 クエリの応答時間は、統計の同期更新を使用するよりも非同期更新を使用した方が予測しやすくなります。非同期更新の場合、クエリ オプティマイザーでは、統計が最新になるまで待機せずに着信クエリを実行できるためです。 これにより、一部のクエリの遅延については回避することができます。  
  
* アプリケーションで統計の更新を待機している 1 つ以上のクエリによって、クライアント要求がタイムアウトする場合。 場合によっては、同期統計を待機していることが原因で、厳しいタイムアウト時間が設定されたアプリケーションが失敗することがあります。  

> [!NOTE]
> ローカル一時テーブルの統計は、AUTO_UPDATE_STATISTICS_ASYNC オプションに関係なく、常に同期的に更新されます。 グローバル一時テーブルの統計は、ユーザー データベースに対して設定された AUTO_UPDATE_STATISTICS_ASYNC オプションに従って、同期的または非同期的に更新されます。

統計の非同期更新は、バックグラウンド要求によって実行されます。 要求は、更新された統計情報をデータベースに書き込む準備ができた時点で、統計メタデータ オブジェクトに対するスキーマ変更ロックの取得を試みます。 別のセッションが同じオブジェクトに対して既にロックを保持している場合、スキーマ変更ロックを取得できるようになるまで、非同期統計の更新がブロックされます。 同様に、クエリをコンパイルするために統計メタデータ オブジェクトに対するスキーマ安定性ロックを取得する必要があるセッションは、既にスキーマ変更ロックの取得を保持しているか待機している非同期統計更新のバックグラウンド セッションによってブロックされる可能性があります。 したがって、クエリのコンパイルや統計の更新が非常に頻繁に行われるワークロードでは、非同期統計を使用すると、ロックのブロックによる同時実行の問題が起きる可能性が高くなる場合があります。

Azure SQL Database では、ASYNC_STATS_UPDATE_WAIT_AT_LOW_PRIORITY [データベース スコープ構成](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)を有効にすると、非同期統計の更新を使用して潜在的な同時実行の問題を回避可能です。 この構成を有効にすると、バックグラウンド要求は、優先度の低い別のキューに対するスキーマ変更ロックの取得を待機します。これにより、他の要求では既存の統計情報を使用したクエリのコンパイルを続行できます。 他のセッションが統計メタデータ オブジェクトのロックを保持しなくなると、バックグラウンド要求はそのスキーマ変更ロックおよび更新統計を取得します。 まれに、バックグラウンド要求が数分のタイムアウト期間内にロックを取得できない場合、非同期統計の更新は中止されます。統計は、別の自動統計更新がトリガーされるか、[手動で更新](update-statistics.md)されるまで更新されません。

#### <a name="incremental"></a>INCREMENTAL  
 CREATE STATISTICS の INCREMENTAL オプションが ON の場合、作成される統計情報はパーティションごとの統計になります。 OFF の場合、統計ツリーが削除され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって統計が再計算されます。 既定値は OFF です。 この設定は、データベース レベルの INCREMENTAL プロパティをオーバーライドします。 増分統計の作成の詳細については、「[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)」を参照してください。 パーティションごとの統計を自動的に作成する方法の詳細については、「[[データベースのプロパティ] &#40;[オプション] ページ&#41;](../../relational-databases/databases/database-properties-options-page.md#automatic)」と「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。 
  
 大きなテーブルに新しいパーティションを追加した場合、新しいパーティションが含まれるように統計を更新する必要があります。 ただし、テーブル全体のスキャン (FULLSCAN または SAMPLE オプション) に要する時間は非常に長くなることがあります。 また、新しいパーティションに対する統計のみが必要となるため、テーブル全体をスキャンする必要はありません。 増分オプションでは、パーティションごとの統計が作成され格納されるため、更新時には、新しい統計を必要とするそれらのパーティションの統計のみを更新します。  
  
 パーティションごとの統計がサポートされていない場合、このオプションは無視され、警告が生成されます。 次の種類の統計では、増分統計がサポートされていません。  
  
* ベース テーブルにパーティションで固定されていないインデックスを使用して作成された統計。  
* Always On の読み取り可能なセカンダリ データベースに対して作成された統計。  
* 読み取り専用のデータベースに対して作成された統計。  
* フィルター選択されたインデックスに対して作成された統計。  
* ビューに対して作成された統計。  
* 内部テーブルに対して作成された統計。  
* 空間インデックスまたは XML インデックスを使用して作成された統計。  
  
**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。 
  
## <a name="when-to-create-statistics"></a><a name="CreateStatistics"></a> 統計を作成する場合  
 クエリ オプティマイザーによって、既に次のようにして統計が作成されています。  
  
1.  インデックスの作成時に、クエリ オプティマイザーによってテーブルまたはビューのインデックスに対する統計が作成されます。 これらの統計は、インデックスのキー列について作成されます。 インデックスがフィルター選択されたインデックスの場合は、フィルター選択されたインデックスに指定された行のサブセットと同じ行のサブセットについて、フィルター選択された統計が作成されます。 フィルター選択されたインデックスの詳細については、「[フィルター選択されたインデックスの作成](../../relational-databases/indexes/create-filtered-indexes.md)」および 「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  

    > [!NOTE]
    > [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降では、パーティション インデックスが作成または再構築された場合、テーブル内のすべての行をスキャンして統計を作成することはできません。 代わりに、クエリ オプティマイザーが既定のサンプリング アルゴリズムを使用して統計を生成します。 パーティション インデックスでデータベースをアップグレードした後で、これらのインデックスのヒストグラム データに違いが見つかる場合があります。 この動作の変更はクエリ パフォーマンスに影響しない可能性があります。 テーブル内のすべての行をスキャンしてパーティション インデックスの統計を作成するには、`FULLSCAN` 句で `CREATE STATISTICS` または `UPDATE STATISTICS` を使用します。 
  
2.  [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) がオンの場合、クエリ オプティマイザーによってクエリ述語内の列に対して 1 列ずつ統計が作成されます。  

ほとんどのクエリでは、これらの 2 つの方法で作成された統計を使用すれば、高品質のクエリ プランになります。ただし、 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) ステートメントを使用して追加の統計を作成することで、クエリ プランが向上する場合もあります。 これらの追加の統計では、クエリ オプティマイザーでインデックスまたは 1 列ずつの統計を作成する場合には考慮されない統計的相関関係を取り込むことができます。 アプリケーションのテーブル データには、計算して統計オブジェクトに含めればクエリ オプティマイザーでクエリ プランを向上させることができる、他の統計的相関関係が含まれている場合があります。 たとえば、データ行のサブセットに関するフィルター選択された統計情報や、クエリ述語列の複数列統計を使用することで、クエリ プランが向上することがあります。  
  
CREATE STATISTICS ステートメントを使用して統計を作成する場合、AUTO_CREATE_STATISTICS オプションをオンのままにし、クエリ述語列に対する 1 列ずつの統計がクエリ オプティマイザーによって通常どおり作成されるようにしておくことをお勧めします。 クエリ述語の詳細については、「[検索条件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)」を参照してください。  
  
次のいずれかに該当する場合は、CREATE STATISTICS ステートメントを使用して統計を作成することを検討してください。  

* [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーで統計を作成するように提示される。 
* 相関関係にある複数の列がクエリ述語に含まれているが、それらがまだ同じインデックスに存在しない。  
* データのサブセットから選択するクエリを使用する。  
* クエリに統計がない。  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>相関関係にある複数の列がクエリ述語に含まれている  
列間に相関関係や依存関係がある複数の列がクエリ述語に含まれている場合、複数列の統計を使用するとクエリ プランが向上することがあります。 複数列の統計には、 *密度* と呼ばれる列間の相関関係の統計が含まれます。これは、1 列ずつの統計では使用できません。 複数の列間のデータの相関関係によってクエリ結果が異なる場合、密度を使用するとカーディナリティの推定が向上します。  
  
列が同じインデックスに既に存在する場合、複数列統計オブジェクトは既に存在するため、手動で作成する必要はありません。 列が同じインデックスにまだ存在しない場合は、列のインデックスを作成するか [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) ステートメントを使用することによって、複数列統計を作成できます。 メンテナンスに必要なシステム リソースは、インデックスの方が統計オブジェクトよりも多くなります。 複数列のインデックスを必要としないアプリケーションの場合は、インデックスを作成せずに統計オブジェクトを作成すると、システム リソースを節約できます。  
  
複数列統計を作成する場合、統計オブジェクト定義内の列の順序によって、カーディナリティの推定に密度を使用した場合の効果が変わります。 統計オブジェクトには、統計オブジェクト定義内のキー列の各プレフィックスの密度が格納されます。 密度の詳細については、このページの[密度](#density)に関するセクションを参照してください。  
  
カーディナリティの推定に効果的な密度を作成するには、クエリ述語内の列が、統計オブジェクト定義内の列のいずれかのプレフィックスに一致する必要があります。 たとえば、次の例では、列 `LastName`、 `MiddleName`、および `FirstName`に対する複数列統計オブジェクトを作成しています。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
この例では、統計オブジェクト `LastFirst` に、列プレフィックス (`(LastName)`)、(`(LastName, MiddleName)`)、および (`(LastName, MiddleName, FirstName)`) の密度が格納されています。 (`(LastName, FirstName)`) の密度は使用できません。 `LastName` を使用せずに `FirstName` と `MiddleName` を使用したクエリの場合は、カーディナリティの推定に密度を使用することはできません。  
  
### <a name="query-selects-from-a-subset-of-data"></a>データのサブセットから選択するクエリを使用する  
クエリ オプティマイザーでは、1 列ずつおよびインデックスに対して統計を作成する際、すべての行の値に対する統計を作成します。 行のサブセットから選択するクエリの場合、その行のサブセットのデータ分布が一意であれば、フィルター選択された統計情報を使用することでクエリ プランを向上させることができます。 フィルター選択された統計情報は、[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) ステートメントを [WHERE](../../t-sql/queries/where-transact-sql.md) 句と共に使用してフィルター述語の式を定義することで作成できます。  
  
たとえば、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] を使用する場合、`Production.Product` テーブルの各製品は、`Production.ProductCategory` テーブルの次の 4 つのカテゴリのいずれかに属しています:Bikes、Components、Clothing、Accessories。 各カテゴリでは、重量に関するデータ分布が異なります。自転車の重量は 13.77 ～ 30.0、部品の重量は 2.12 ～ 1050.00 (一部 NULL 値)、衣類の重量はすべて NULL、付属品の重量も NULL です。  
  
たとえば Bikes の場合、自転車のすべての重量についてのフィルター選択された統計情報を使用すると、テーブル全体の統計情報を使用する場合や、Weight 列の統計情報が存在しない場合と比べて、より正確な統計情報がクエリ オプティマイザーに提供され、クエリ プランの品質が向上します。 自転車の重量の列は、フィルター選択された統計情報には適していますが、重量の参照が比較的少ない場合、フィルター選択されたインデックスには必ずしも適しているとは限りません。 フィルター選択されたインデックスを使用することで得られる参照のパフォーマンスの向上よりも、フィルター選択されたインデックスをデータベースに追加するためのメンテナンス コストとストレージ コストの増加の方が大きい場合があります。  
  
次のステートメントでは、Bikes のすべてのサブカテゴリについてのフィルター選択された統計 `BikeWeights` を作成します。 フィルター選択された述語式で、比較 `Production.ProductSubcategoryID IN (1,2,3)`を使用して自転車のすべてのサブカテゴリを列挙することで、自転車を定義しています。 Bikes カテゴリは Production.ProductCategory テーブルに格納されているため、述語でそのカテゴリ名を使用することはできません。フィルター式に含まれるすべての列が、同じテーブル内に存在する必要があります。  
  
[!code-sql[StatisticsDDL#FilteredStats2](../../relational-databases/statistics/codesnippet/tsql/statistics_1.sql)]  
  
クエリ オプティマイザーでは、 `BikeWeights` というフィルター選択された統計情報を使用して、重量が `25`を超えるすべての自転車を選択する次のクエリのクエリ プランを向上させることができます。  
  
```sql  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>統計がないことをクエリで識別する  
クエリ オプティマイザーでは、エラーやその他のイベントによって統計を作成できない場合、統計を使用せずにクエリ プランを作成します。 クエリ オプティマイザーでは存在しない統計をマークし、次回のクエリの実行時に再生成しようとします。  
  
統計が存在しない場合は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してクエリの実行プランをグラフィカルに表示すると、警告 (赤色のテーブル名) が表示されます。 また、 **を使用して** Missing Column Statistics [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] イベント クラスを監視すると、統計がない場合はそのことがわかります。 詳細については、「[Errors and Warnings イベント カテゴリ &#40;データベース エンジン&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md)」を参照してください。  
  
 統計がない場合は、次の手順を実行します。  
  
* [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) と [AUTO_UPDATE_STATISTICS ](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) がオンになっていることを確認します。  
* データベースが読み取り専用ではないことを確認します。 データベースが読み取り専用の場合は、新しい統計オブジェクトを保存できません。  
* 存在しない統計を [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) ステートメントを使用して作成します。  
  
読み取り専用データベースまたは読み取り専用スナップショットに関する統計が欠落しているか、古くなっている場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、 **tempdb** に一時的な統計を作成して維持します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で一時的な統計を作成する場合は、一時的な統計と永続的な統計とを区別するためのサフィックス *_readonly_database_statistic* が統計名に付加されます。 サフィックス *_readonly_database_statistic* は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって生成される統計用に予約されています。 読み書き可能なデータベースでは、一時的な統計用のスクリプトを作成して再現できます。 スクリプトを作成する場合、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、統計名のサフィックスを *_readonly_database_statistic* から *_readonly_database_statistic_scripted* に変更します。  
  
一時的な統計を作成して更新できるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のみです。 ただし、永続的な統計の場合と同じツールを使用すると、一時的な統計を削除して、統計のプロパティを監視できます。  
  
* [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) ステートメントを使用して一時的な統計を削除します。  
* **[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)** カタログ ビューと **[sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)** カタログ ビューを使用して統計を監視します。 **sys_stats** には、どの統計が一時的または永続的なものかを示すための **is_temporary** 列が含まれています。  
  
 一時的な統計は **tempdb** に格納されるので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動すると、一時的な統計はすべてなくなります。  
    
## <a name="when-to-update-statistics"></a><a name="UpdateStatistics"></a>統計を更新する場合  
 クエリ オプティマイザーでは、古くなっている可能性がある統計を判断し、それらがクエリ プランに必要な場合は更新します。 場合によっては、 [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) をオンにした場合より頻繁に統計を更新することで、クエリ プランが向上し、クエリのパフォーマンスが向上することがあります。 統計は、UPDATE STATISTICS ステートメントまたは sp_updatestats ストアド プロシージャを使用して更新できます。  
  
 統計を更新すると、クエリが最新の統計を使用してコンパイルされるようになります。 ただし、統計の更新によりクエリが再コンパイルされます。 パフォーマンスの向上を目的とする場合、クエリ プランの改善とクエリの再コンパイルに要する時間の間にはトレードオフの関係があるため、あまり頻繁に統計を更新しないようにすることをお勧めします。 実際のトレードオフはアプリケーションによって異なります。  
  
 UPDATE STATISTICS または sp_updatestats を使用して統計を更新する場合、AUTO_UPDATE_STATISTICS オプションを ON に設定したままにし、通常の更新がクエリ オプティマイザーによって引き続き行われるようにしておくことをお勧めします。 列、インデックス、テーブル、またはインデックス付きビューの統計を更新する方法については、「[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)」を参照してください。 データベース内のすべてのユーザー定義および内部テーブルの統計を更新する方法については、ストアド プロシージャ [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) の説明を参照してください。  
  
 統計の最終更新日を確認するには、[sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) または [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 関数を使用します。  
  
 次のような場合は、統計を更新することを検討してください。  
  
* クエリの実行に時間がかかる。  
* 昇順または降順のキー列に対して挿入操作を実行する。  
* メンテナンス操作の実行後。  

### <a name="query-execution-times-are-slow"></a>クエリの実行に時間がかかる  
 クエリの応答時間が遅い場合や予測できない場合は、他のトラブルシューティング手順を実行する前に、クエリの統計が最新のものであることを確認してください。  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>昇順または降順のキー列に対して挿入操作を実行する  
 昇順または降順のキー列 (IDENTITY 列や実時間のタイムスタンプ列など) の統計では、クエリ オプティマイザーで実行されるよりも頻繁に統計の更新が必要になる場合があります。 挿入操作によって昇順または降順の列に新しい値が追加された場合に、 追加された行数が少なすぎると、統計の更新が実行されないことがあります。 統計が最新ではない場合に、追加された最新の行から選択するクエリを実行すると、現在の統計にそれらの新しい値のカーディナリティの推定が含まれません。 その結果、カーディナリティの推定が不正確になり、クエリのパフォーマンスが低下することがあります。  
  
 たとえば、最新の販売注文日から選択するクエリで、統計が最新の販売注文日のカーディナリティの推定を含むように更新されていないと、カーディナリティの推定が不正確になります。  
  
### <a name="after-maintenance-operations"></a>メンテナンス操作の実行後  
 テーブルの切り捨てや大部分の行の一括挿入を行うなど、データの分布が変わるメンテナンス操作を実行した後は、統計を更新することを検討してください。 これにより、統計の自動更新を待つことによってクエリ処理で発生する以降の遅延を回避することができます。  
  
 インデックスの再構築、デフラグ、再構成などの操作では、データの分布は変わりません。 そのため、[ALTER INDEX REBUILD](../../t-sql/statements/alter-index-transact-sql.md#rebuilding-indexes)、[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)、[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)、または [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md#reorganizing-indexes) の各操作を実行した後に統計を更新する必要はありません。 ALTER INDEX REBUILD または DBCC DBREINDEX を使用してテーブルまたはビューのインデックスを再構築した場合、クエリ オプティマイザーによって統計が更新されますが、この統計の更新はインデックスを再作成する過程で実行されるものです。 DBCC INDEXDEFRAG 操作または ALTER INDEX REORGANIZE 操作の後は、クエリ オプティマイザーで統計は更新されません。 
 
> [!TIP]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4 以降では、[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) または [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md) の PERSIST_SAMPLE_PERCENT オプションを使用して、サンプリング比率が明確に指定されていない後続の統計情報更新の特定のサンプリング比率を設定し、保持します。

### <a name="automatic-index-and-statistics-management"></a>インデックスと統計の自動管理

[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) のようなソリューションを活用し、1 つまたは複数のデータベースに対するインデックスの最適化と統計更新を自動管理します。 このプロシージャでは、断片化レベルやその他のパラメーターに基づいてインデックスを再構築または再構成するか、線形しきい値で統計を更新するかが自動的に選択されます。
  
##  <a name="queries-that-use-statistics-effectively"></a><a name="DesignStatistics"></a> 統計を効果的に使用するクエリ  
 クエリ述語にローカル変数や複雑な式が含まれている場合など、特定のクエリ実装では、最適なクエリ プランにならないことがあります。 クエリのデザイン ガイドラインに従って統計を効果的に使用することで、この問題を回避できる場合があります。 クエリ述語の詳細については、「[検索条件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)」を参照してください。  
  
 クエリのデザイン ガイドラインを適用して統計を効果的に使用することで、クエリ述語で使用される式、変数、および関数に対する *カーディナリティの推定* を向上させると、クエリ プランを向上させることができます。 クエリ オプティマイザーでは、式、変数、または関数の値が不明な場合、ヒストグラムで参照する値を特定できないため、ヒストグラムから最適なカーディナリティの推定を得ることができません。 その場合、クエリ オプティマイザーでは、ヒストグラム内のサンプリングされたすべての行の値ごとの平均行数に基づいてカーディナリティの推定を行います。 その結果、カーディナリティが適切に推定されず、クエリのパフォーマンスが低下することがあります。 ヒストグラムの詳細については、このページの「[ヒストグラム](#histogram)」のセクション、または「[sys.dm_db_stats_histogram](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)」をご覧ください。
  
 以下のガイドラインでは、カーディナリティの推定を向上させることによってクエリ プランを改善するためのクエリの作成方法について説明します。  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>式に対するカーディナリティの推定を向上させる  
式に対するカーディナリティの推定を向上させるには、次のガイドラインに従います。  
  
* 定数を含む式は可能な限り単純にします。 クエリ オプティマイザーでは、カーディナリティの推定を判断する前に、定数を含むすべての関数および式の評価は行われません。 たとえば、式 `ABS(-100)` を `100` に簡略化します。  
  
* 式で複数の変数を使用している場合は、式の計算列を作成し、その計算列に対する統計またはインデックスを作成することを検討します。 たとえば、クエリ述語 `WHERE PRICE + Tax > 100` のカーディナリティの推定は、式 `Price + Tax` に対する計算列を作成すると向上する可能性があります。  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>変数および関数に対するカーディナリティの推定を向上させる  
変数および関数に対するカーディナリティの推定を向上させるには、次のガイドラインに従います。  
  
* クエリ述語でローカル変数を使用している場合は、ローカル変数の代わりにパラメーターを使用してクエリを書き換えることを検討します。 ローカル変数の値は、クエリ オプティマイザーでのクエリ実行プランの作成時には認識されません。 クエリでパラメーターを使用すると、クエリ オプティマイザーで、ストアド プロシージャに渡される最初の実際のパラメーター値に対するカーディナリティの推定が使用されます。  
  
* 複数ステートメントのテーブル値関数 (mstvf) の結果を格納する場合は、標準のテーブルか一時テーブルを使用することを検討します。 クエリ オプティマイザーでは、複数ステートメントのテーブル値関数の統計は作成されません。 この方法を使用すると、クエリ オプティマイザーでテーブル列の統計を作成できるため、それを使用することでクエリ プランを向上させることができます。  
  
* テーブル変数の代わりに標準のテーブルか一時テーブルを使用することを検討します。 クエリ オプティマイザーでは、テーブル変数の統計は作成されません。 この方法を使用すると、クエリ オプティマイザーでテーブル列の統計を作成できるため、それを使用することでクエリ プランを向上させることができます。 一時テーブルとテーブル変数のどちらを使用するかの判断には、トレードオフの関係があります。ストアド プロシージャでテーブル変数を使用すると、ストアド プロシージャの再コンパイルの回数が、一時テーブルを使用した場合よりも少なくなります。 アプリケーションによっては、テーブル変数の代わりに一時テーブルを使用しても、パフォーマンスが向上しない場合もあります。  
  
* 渡されたパラメーターを使用するクエリがストアド プロシージャに含まれている場合は、パラメーター値がクエリで使用される前にストアド プロシージャ内で変更されないようにします。 クエリに対するカーディナリティの推定は、更新された値ではなく渡されたパラメーターの値に基づいて行われます。 パラメーター値が変更されないようにするには、2 つのストアド プロシージャを使用するようにクエリを書き換えます。  
  
     たとえば、次のストアド プロシージャ `Sales.GetRecentSales` では、`@date` が NULL の場合にパラメーター `@date` の値を変更します。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date IS NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     ストアド プロシージャ `Sales.GetRecentSales` の最初の呼び出しで `@date` パラメーターに NULL が渡された場合、クエリ オプティマイザーでは、クエリ述語が `@date = NULL` で呼び出されていなくても、 `@date = NULL`に対するカーディナリティの推定を使用してストアド プロシージャをコンパイルします。 このカーディナリティの推定は、実際のクエリ結果の行数と大きく異なる場合があります。 そのため、クエリ オプティマイザーにより、最適なクエリ プランが選択されないことがあります。 この問題を回避するには、ストアド プロシージャを次のように 2 つのプロシージャに書き換えます。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>クエリ ヒントを使用してカーディナリティの推定を向上させる  
 ローカル変数に対するカーディナリティの推定を向上させるには、RECOMPILE を指定して `OPTIMIZE FOR <value>` または `OPTIMIZE FOR UNKNOWN` クエリ ヒントを使用します。 詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。  
  
 アプリケーションによっては、クエリを実行するたびに再コンパイルすると時間がかかりすぎる場合がありますが、 `OPTIMIZE FOR` クエリ ヒントは `RECOMPILE` オプションを使用しなくても役立つことがあります。 たとえば、ストアド プロシージャ Sales.GetRecentSales に `OPTIMIZE FOR` オプションを追加して、特定の日付を指定することができます。 Sales.GetRecentSales プロシージャに `OPTIMIZE FOR` オプションを追加する例を次に示します。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>プラン ガイドを使用してカーディナリティの推定を向上させる  
 アプリケーションによっては、クエリを変更できない場合や、RECOMPILE クエリ ヒントを使用すると再コンパイルが多くなりすぎる場合など、クエリのデザイン ガイドラインを適用できないことがあります。 プラン ガイドを使用すると、アプリケーション ベンダーによるアプリケーションの違いを確認しながら、その他のヒント (USE PLAN など) を指定してクエリの動作を制御することができます。 プラン ガイドの詳細については、「 [Plan Guides](../../relational-databases/performance/plan-guides.md)」を参照してください。  
  
  
## <a name="see-also"></a>参照  
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [フィルター選択されたインデックスの作成](../../relational-databases/indexes/create-filtered-indexes.md)   
 [SQL Server で Autostat (AUTO_UPDATE_STATISTICS) 動作を制御する](https://support.microsoft.com/help/2754171)   
 [STATS_DATE &#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)   
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)  
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)  
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)    
 [Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)