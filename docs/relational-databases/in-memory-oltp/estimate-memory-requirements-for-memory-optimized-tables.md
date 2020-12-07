---
title: メモリの要件 - メモリ最適化テーブル
description: すべての行とインデックスに十分なメモリが必要である SQL Server のメモリ最適化テーブルについて、メモリ使用と管理のシナリオについて説明します。
ms.custom: seo-dt-2019
ms.date: 12/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 710554564bf1018c1551fe0e6dbbe065ea395924
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384766"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>メモリ最適化テーブルのメモリ必要量の推定
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

メモリ最適化テーブルでは、すべての行とインデックスをメモリ内に保持するために十分なメモリが必要です。 メモリは有限のリソースであるため、システム上のメモリ使用量を把握して管理することが重要です。 このセクションのトピックでは、一般的なメモリの使用量と管理シナリオについて説明します。

新しいメモリ最適化テーブルを作成するか、既存のディスク ベース テーブルを [!INCLUDE[hek_2](../../includes/hek-2-md.md)] メモリ最適化テーブルに移行するかにかかわりなく、各テーブルのメモリ必要量に関する適切な推定を実施することは重要であり、その結果、サーバーで十分なメモリを準備することができます。 ここでは、メモリ最適化テーブルのデータを保持するために必要とされるメモリの量を推定する方法について説明します。  
  
ディスク ベース テーブルをメモリ最適化テーブルに移行することを検討している場合は、このトピックを読み進める前に、どのテーブルを移行するのが最善であるかを示す「 [テーブルまたはストアド プロシージャをインメモリ OLTP に移植する必要があるかどうかの確認](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 」というトピックを参照してください。 「 [インメモリ OLTP への移行](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md) 」に掲載されているすべてのトピックには、ディスク ベース テーブルからメモリ最適化テーブルへの移行に関するガイダンスが掲載されています。 
  
## <a name="basic-guidance-for-estimating-memory-requirements"></a>メモリ要件を見積もるための基本的なガイダンス

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]より、メモリ最適化テーブルのサイズに制限がなくなりました。ただし、テーブルはメモリ内に収まる必要があります。  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] で SCHEMA_AND_DATA テーブルにサポートされるデータ サイズは 256 GB です。

メモリ最適化テーブルのサイズは、データのサイズに行ヘッダーの一部のオーバーヘッドを加えたものに相当します。 ディスク ベース テーブルをメモリ最適化テーブルに移行する場合、メモリ最適化テーブルのサイズは、大まかには元のディスク ベース テーブルのクラスター化インデックスまたはヒープのサイズに相当します。

メモリ最適化テーブルのインデックスは、ディスク ベース テーブルの非クラスター化インデックスよりも小さくなる傾向があります。 非クラスター化インデックスのサイズは `[primary key size] * [row count]`と同程度です。 ハッシュ インデックスのサイズは `[bucket count] * 8 bytes`です。 

アクティブなワークロードがある場合は、行のバージョン管理およびさまざまな操作を行うために追加のメモリが必要です。 実際にどれくらいのメモリが必要になるかはワークロードによって異なりますが、安全のためには、メモリ最適化テーブルとインデックスの見積もりサイズの 2 倍から始め、メモリ要件が実際にどれくらいになるかを確認することをお勧めします。 行のバージョン管理のオーバーヘッドは、常にワークロードの特性に依存します。特に長時間実行されるトランザクションではオーバーヘッドが増加します。 大規模なデータベース (例: >100 GB) を使用するワークロードのほとんどで、オーバーヘッドが制限される傾向にあります (25% 以内)。

  
## <a name="detailed-computation-of-memory-requirements"></a>メモリ要件の詳細な計算 
  
- [サンプルのメモリ最適化テーブル](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_ExampleTable)  
  
- [テーブルに対応するメモリ](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForTable)  
  
- [インデックスに対応するメモリ](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_IndexMeemory)  
  
- [行のバージョン管理に対応するメモリ](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForRowVersions)  
  
- [テーブル変数に対応するメモリ](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_TableVariables)  
  
- [成長に対応するメモリ](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForGrowth)  
  
###  <a name="example-memory-optimized-table"></a><a name="bkmk_ExampleTable"></a> サンプルのメモリ最適化テーブル  

次のメモリ最適化テーブルのスキーマを考えてみます。
  
```sql  
CREATE TABLE t_hk
(  
  col1 int NOT NULL  PRIMARY KEY NONCLUSTERED,  

  col2 int NOT NULL  INDEX t1c2_index   
      HASH WITH (bucket_count = 5000000),  

  col3 int NOT NULL  INDEX t1c3_index   
      HASH WITH (bucket_count = 5000000),  

  col4 int NOT NULL  INDEX t1c4_index   
      HASH WITH (bucket_count = 5000000),  

  col5 int NOT NULL  INDEX t1c5_index NONCLUSTERED,  

  col6 char (50) NOT NULL,  
  col7 char (50) NOT NULL,   
  col8 char (30) NOT NULL,   
  col9 char (50) NOT NULL  

)   WITH (memory_optimized = on)  ;
GO  
```  

このスキーマを使用して、このメモリ最適化テーブルで必要とされる最小メモリを決定します。  
  
###  <a name="memory-for-the-table"></a><a name="bkmk_MemoryForTable"></a> テーブルに対応するメモリ  

メモリ最適化テーブルの行は、次の 3 つの部分から形成されています。
  
- **タイムスタンプ**   
    行のヘッダー/タイムスタンプ = 24 バイトです。  
  
- **インデックス ポインター**   
    テーブル内の各ハッシュ インデックスにある各行には、インデックス内の次の行を指す 8 バイトのアドレス ポインターが含まれています。  ここでは 4 つのインデックスが存在しているため、各行はインデックス ポインターに 32 バイト (インデックスごとに 8 バイトのポインター) を割り当てます。  
  
- **データ**   
    行のデータ部分のサイズは、各データ列に対応する型サイズの合計によって決まります。  このテーブルには、4 バイトの整数が 5 個、50 バイトの文字列型の列が 3 個、30 バイトの文字列型の列が 1 個あります。  したがって、各行のデータ部分は、4 + 4 + 4 + 4 + 4 + 50 + 50 + 50 + 30、つまり 200 バイトです。  
  
以下は、メモリ最適化テーブル内に存在する 5,000,000 (500 万) 行のサイズの計算です。 データ行で使用される合計メモリは、次のように推定されます。  
  
#### <a name="memory-for-the-tables-rows"></a>テーブルの行に対応するメモリ  
  
上記の計算結果から、メモリ最適化テーブル内にある各行のサイズは 24 + 32 + 200、つまり 256 バイトです。  500 万の行があるため、テーブルは 5,000,000 * 256 バイト、つまり 1,280,000,000 バイト、約 1.28 GB を使用します。  
  
###  <a name="memory-for-indexes"></a><a name="bkmk_IndexMeemory"></a> インデックスに対応するメモリ  

#### <a name="memory-for-each-hash-index"></a>各ハッシュ インデックスに対応するメモリ  
  
各ハッシュ インデックスは、8 バイトのアドレス ポインターから成るハッシュの配列です。  配列のサイズは、そのインデックスの一意のインデックス値の数に基づいて適切に決定できます。たとえば、一意の Col2 の値の数を、t1c2_index の配列サイズを求めるための適切な出発点として使用することができます。 大きすぎるハッシュ配列は、メモリを浪費します。  小さすぎるハッシュ配列を使用する場合は、パフォーマンスが低下します。同じインデックスへとハッシュされるインデックス値が多くなり、非常に多くの競合が発生するためです。  
  
ハッシュ インデックスは、次のように等値参照を実行する場合は非常に高速です。  
  
```sql  
SELECT * FROM t_hk  
   WHERE Col2 = 3;
```  
  
非クラスター化インデックスは、次のように範囲参照を実行する場合はより高速になります。  
  
```sql  
SELECT * FROM t_hk  
   WHERE Col2 >= 3;
```  
  
ディスク ベース テーブルを移行する場合は、t1c2_index インデックスに対応する一意の値の数を決定するために、次を使用できます。  
  
```sql
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk;
```  
  
新しいテーブルを作成する場合は、配列のサイズを推測するか、配置を実行する前にテストからデータを収集する必要があります。  
  
[!INCLUDE[hek_2](../../includes/hek-2-md.md)] メモリ最適化テーブル内でのハッシュ インデックスの動作方法の詳細については、「 [Hash Indexes](/previous-versions/sql/sql-server-2016/dn133190(v=sql.130))」(ハッシュ インデックス) を参照してください。  
  
#### <a name="setting-the-hash-index-array-size"></a>ハッシュ インデックスの配列サイズの設定  
  
ハッシュの配列サイズは `(bucket_count= value)` によって設定されます。ここで、 `value` は、0 より大きい整数値です。 `value` が 2 のべき乗でない場合は、実際の bucket_count は、最も近い 2 のべき乗になるように切り上げられます。  この例のテーブルでは bucket_count = 5,000,000 であり、5,000,000 は 2 のべき乗ではないため、実際のバケット数は 8,388,608 (2^23) に切り上げられます。  ハッシュ配列が必要とするメモリを計算するときは、5,000,000 ではなく、この数値を使用する必要があります。  
  
したがって、この例の各ハッシュ配列で必要とされるメモリは次のようになります。  
  
8,388,608 * 8 = 2^23 \* 8 = 2^23 \* 2^3 = 2^26 = 67,108,864 つまり約 64 MB です。  
  
3 つのハッシュ インデックスが存在するため、ハッシュ インデックスで必要とされるメモリは 3 * 64MB = 192MB です。  
  
#### <a name="memory-for-nonclustered-indexes"></a>非クラスター化インデックスに対応するメモリ  
  
非クラスター化インデックスは BTree として実装されており、内部ノードはインデックス値と、後続のノードを指すポインターを保持しています。  リーフ ノードは、インデックス値と、メモリ内にあるテーブルの行を指すポインターを保持しています。  
  
ハッシュ インデックスとは異なり、非クラスター化インデックスには、固定的なバケット サイズがありません。 インデックスは、データと共に動的に拡張または圧縮されます。  
  
非クラスター化インデックスのメモリ必要量は、次のように計算することができます。  
  
- **非リーフ ノードに割り当てられるメモリ**   
    標準的な構成では、非リーフ ノードに割り当てられるメモリが、インデックスによって取得されるメモリ全体に占める割合は非常に小さいものです。 これは非常に小さい割合であり、無視しても安全です。  
  
- **リーフ ノードに割り当てられるメモリ**   
    リーフ ノードにはテーブル内に存在する一意のキーごとに 1 行のデータがあり、リーフ ノードは、その一意のキーを持つデータ行を指します。  同じキーを持つ複数の行が存在する (つまり、一意ではない非クラスター化インデックスを使用している) 場合は、インデックスのリーフ ノード内にはただ 1 つの行があり、リーフ ノードは 1 つの行を指しており、各行は互いにリンクされています。  したがって、必要とされるメモリ全体は、次のように近似できます。
  - memoryForNonClusteredIndex = (pointerSize + sum(keyColumnDataTypeSizes)) * rowsWithUniqueKeys  
  
 非クラスター化インデックスは、次のクエリで例示する範囲参照の場合に使用するのが最適です。  
  
```sql  
SELECT * FROM t_hk  
   WHERE c2 > 5;  
```  
  
###  <a name="memory-for-row-versioning"></a><a name="bkmk_MemoryForRowVersions"></a> 行のバージョン管理に対応するメモリ

ロックを回避するために、インメモリ OLTP は行を更新または削除するときに、オプティミスティック コンカレンシーを使用します。 これは、行を更新するときに、行の追加バージョンが作成されることを意味します。 さらに、削除は論理的であり、既存の行が削除済みとしてマークされますが、すぐには削除されません。 以前のバージョンを使用する可能性のあるすべてのトランザクションが実行を完了するまで、システムは (削除された行を含む) 古い行バージョンを使用可能な状態に保ちます。 
  
メモリ内にはいつでも多数の追加行が存在している可能性があり、それらの行は自らのメモリを解放するガベージ コレクション サイクルを待機しているため、これらの追加の行を収容するために十分なメモリを用意する必要があります。  
  
追加の行の数を推定するには、1 秒あたりの行の更新と削除に関するピークの数値を求め、その値に、最も長いトランザクションが要する秒数 (最小値は 1) を掛けます。  
  
この積に、行サイズを掛けると、行のバージョン管理に必要とされるバイト数を得ることができます。  
  
`rowVersions = durationOfLongestTransctoinInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
古い行に関するメモリ必要量を推定するには、古い行の数に、メモリ最適化テーブルの行サイズを掛けます (上記の「 [テーブルに対応するメモリ](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md#bkmk_MemoryForTable) 」を参照)。  
  
`memoryForRowVersions = rowVersions * rowSize`  
  
###  <a name="memory-for-table-variables"></a><a name="bkmk_TableVariables"></a> テーブル変数に対応するメモリ
  
テーブル変数に対応するメモリは、テーブル変数がスコープ外になる場合にのみ解放されます。 テーブル変数から削除された行 (更新の一部として削除された行を含む) には、ガベージ コレクションは適用されません。 テーブル変数がスコープを終了するまでメモリは解放されません。  
  
プロシージャ スコープとは対照的に、多くのトランザクションで使用される大きな SQL バッチで定義されるテーブル変数は、多くのメモリを消費することがあります。 ガベージ コレクションの対象ではないため、テーブル変数内にある削除された行は多くのメモリを使用し、パフォーマンスが低下することがあります。読み取り操作では、削除されたこれらの行をスキャンで通過させる必要があるためです。  
  
###  <a name="memory-for-growth"></a><a name="bkmk_MemoryForGrowth"></a> 成長に対応するメモリ

上記の各計算では、現在存在しているテーブルに対応するメモリ必要量を推定しています。 このメモリに加えて、テーブルが成長することを推定し、その成長を収容するために十分なメモリを用意する必要があります。  たとえば、10% の成長を予測している場合は、上記の結果に 1.1 を掛けて、テーブルで必要とされる合計メモリを得ることができます。  
  
## <a name="see-also"></a>参照

[インメモリ OLTP への移行](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)