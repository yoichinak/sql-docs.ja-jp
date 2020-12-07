---
title: 実行プラン | Microsoft Docs
description: SQL Server データベース エンジンでクエリを実行する目的でクエリ オプティマイザーによって作成される実行プランまたはクエリ プランについて説明します。
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- execution plan [SQL Server]
- query plan [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9b0f95a4afa1397783547f2804d92dd3fc37b357
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126616"
---
# <a name="execution-plans"></a>実行プラン
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

クエリを実行するには、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] はステートメントを分析し、必要なデータにアクセスする最も効率的な方法を判断する必要があります。 この分析は、クエリ オプティマイザーと呼ばれているコンポーネントによって処理されます。 クエリ オプティマイザーへの入力は、クエリ、データベース スキーマ (テーブル定義やインデックスの定義)、およびデータベース統計で構成されます。 クエリ オプティマイザーの出力がクエリ実行プランです。これは、クエリ プランや実行プランと呼ばれることもあります。   

クエリ実行プランは、次の事項を定義しています。 

- **基になるテーブルにアクセスする順序。**  
  通常、データベース サーバーからベース テーブルにアクセスして結果セットを構築する順序は何とおりもあります。 たとえば、`SELECT` ステートメントが 3 つのテーブルを参照している場合、データベース サーバーは最初に `TableA` にアクセスし、`TableA` のデータを使用して `TableB` から一致する行を抽出します。次に、`TableB` のデータを使用して `TableC` のデータを抽出することができます。 データベースがテーブルにアクセスする際に可能な順序には、次の組み合わせがあります。  
  `TableC`、 `TableB`、 `TableA`、または  
  `TableB`、 `TableA`、 `TableC`、または  
  `TableB`、 `TableC`、 `TableA`、または  
  `TableC`, `TableA`, `TableB`  

- **各テーブルからデータを取り出すための方法。**  
  通常、各テーブルのデータにアクセスする方法にも何とおりかあります。 特定のキー値を持つ数行だけが必要な場合、データベース サーバーではインデックスを使用できます。 テーブル内のすべての行が必要な場合は、インデックスを無視してテーブル スキャンを実行できます。 テーブル内のすべての行が必要で、 `ORDER BY`で指定されたキー列のインデックスがある場合、テーブル スキャンではなくインデックス スキャンを行うと、結果セットの並べ替えを個別に行わずに済みます。 テーブルが非常に小さい場合は、テーブルにどのようにアクセスするときでもテーブル スキャンが最も効率的な方法です。
  
- **計算に使用される方法と、各テーブルのデータのフィルター処理、集計、並べ替えを行う方法。**  
  テーブルのデータにアクセスするときは、データに対して計算を実行するためのさまざまな方法が存在します (スカラー値の計算など)。また、クエリ テキストで定義されているようにデータの集計や並べ替えを行ったり (`GROUP BY` 句や `ORDER BY` 句を使う場合など)、データをフィルター処理したり (`WHERE` 句や `HAVING` 句を使う場合など) するための方法も多数存在します。

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、実行プランを表示するための 3 つのオプションがあります。        
> -  "**_[推定実行プラン](../../relational-databases/performance/display-the-estimated-execution-plan.md)_* _" は、見積もりに基づいてクエリ オプティマイザーによって生成された、コンパイル済みプランです。 これは、プラン キャッシュに格納されているクエリ プランです。        
> -  " _*_ [実際の実行プラン](../../relational-databases/performance/display-an-actual-execution-plan.md) _*_ " は、コンパイル済みプランにその[実行コンテキスト](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)を加えたものです。 これは、_*クエリの実行が完了した後に** 使用できるようになります。 これには、実際のランタイム情報 (実行に関する警告など)、または実行中に使用された経過時間および CPU 時間 (新しいバージョンの [!INCLUDE[ssde_md](../../includes/ssde_md.md)] の場合) が含まれます。         
> -  "**_[ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)_ *_" は、コンパイル済みプランにその実行コンテキストを加えたものです。これは _* 使用中のクエリ実行** に対して使用でき、1 秒ごとに更新されます。 これには、[演算子](../../relational-databases/showplan-logical-and-physical-operators-reference.md)を通過する実際の行数、経過時間、およびクエリの推定進行状況などのランタイム情報が含まれます。

> [!TIP]
> クエリ処理およびクエリ実行プランの詳細については、「クエリ処理アーキテクチャ ガイド」の「[SELECT ステートメントの最適化](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements)」と「[実行プランのキャッシュと再利用](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)」のセクションを参照してください。

## <a name="in-this-section"></a>このセクションの内容  
[クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)     
[実行プランの表示と保存](../../relational-databases/performance/display-and-save-execution-plans.md)     
[実行プランの比較と分析](../../relational-databases/performance/compare-and-analyze-execution-plans.md)     
[プラン ガイド](../../relational-databases/performance/plan-guides.md)     

## <a name="see-also"></a>参照  
[パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
[パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)    
[ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)     
[利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)     
[クエリのストアを使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
[sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
[トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
[プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
