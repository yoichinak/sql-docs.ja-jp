---
description: dm_db_xtp_gc_cycle_stats (Transact-sql)
title: dm_db_xtp_gc_cycle_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_gc_cycle_stats_TSQL
- dm_db_xtp_gc_cycle_stats
- sys.dm_db_xtp_gc_cycle_stats_TSQL
- sys.dm_db_xtp_gc_cycle_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_gc_cycle_stats dynamic management view
ms.assetid: bbc9704e-158e-4d32-b693-f00dce31cd2f
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7cd3e4fef0d6d02508ff8b6cd917b1a02a08585e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542254"
---
# <a name="sysdm_db_xtp_gc_cycle_stats-transact-sql"></a>dm_db_xtp_gc_cycle_stats (Transact-sql)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  1 つ以上の行を削除したコミット済みトランザクションの現在の状態を出力します。 アイドル状態のガベージコレクションスレッドは、最後のガベージコレクションサイクル以降にコミットされた DML トランザクションの数が内部しきい値を超えたときに、1分ごとに起動されます。 ガベージ コレクション サイクルの一環として、コミット済みトランザクションは、generation と関連付けられている 1 つ以上のキューに移動されます。 古いバージョンを生成したトランザクションは、次のようにして、16 の generation にわたり 16 トランザクションごとの単位にグループ化されます。  
  
-   generation 0: 最も古いアクティブなトランザクションより前にコミットされたトランザクションがすべて格納されます。 これらのトランザクションによって生成される行バージョンは、すぐにガベージコレクションに使用できます。  
  
-   Generation 1-14: 最も古いアクティブなトランザクションを超えるタイムスタンプを持つトランザクションを格納します。 行バージョンに対してガベージ コレクションを実行することはできません。 各世代には、最大16のトランザクションを保持できます。 これらのジェネレーションには合計 224 (14 * 16) トランザクションが存在する可能性があります。  
  
-   generation 15: 最も古いアクティブなトランザクションより後のタイムスタンプを持つ、残りのトランザクションは generation 15 に格納されます。 generation 0 と同様、generation 15 にもトランザクション数の制限はありません。  
  
 メモリが不足している場合、ガベージ コレクション スレッドは、最も古いアクティブなトランザクションのヒントを積極的に更新します。これにより、ガベージ コレクションが強制されます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|cycle_id|**bigint**|ガベージコレクションサイクルの一意の識別子。|  
|ticks_at_cycle_start|**bigint**|サイクルが開始されたときのタイマー刻み。|  
|ticks_at_cycle_end|**bigint**|サイクルが終了したときのタイマー刻み。|  
|base_generation|**bigint**|データベース内の現在の基本生成値。 これは、ガベージコレクションのトランザクションを識別するために使用される最も古いアクティブなトランザクションのタイムスタンプを表します。 最も古いアクティブなトランザクション id は、16の増分で更新されます。 たとえば、トランザクション id が124、125、126の場合、139,、値は124になります。 また、たとえばトランザクション 140 を追加した場合、この値は 140 になります。|  
|xacts_copied_to_local|**bigint**|トランザクションのパイプラインからデータベースの generation 配列にコピーされたトランザクションの数|  
|xacts_in_gen_0-xacts_in_gen_15|**bigint**|generation ごとのトランザクションの数|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="usage-scenario"></a>使用シナリオ  
 次に示すのは、27世代を示す列のサブセットを含む出力サンプルです。  
  
```  
cycle_id   ticks_at_cycle_start ticks_at_cycle_end   base_generation  xacts_in_gen_0    xacts_in_gen_1  
  
1          123160509            123160509            1                    0                    0  
2          123176822            123176822            1                    0                    1  
3          123236826            123236826            1                    0                    1  
4          123296829            123296829            1                    0                    1  
5          123356832            123356941            129                  0                    0  
6          123357473            123357473            129                  0                    0  
7          123417486            123417486            129                  0                    0  
8          123477489            123477489            129                  0                    0  
9          123537492            123537492            129                  0                    0  
10         123597500            123597500            129                  0                    0  
11         123657504            123657504            129                  0                    0  
12         123717507            123717507            129                  0                    0  
13         123777510            123777510            129                  0                    0  
14         123837513            123837513            129                  0                    0  
15         123897516            123897516            129                  0                    0  
16         123957516            123957516            129                  0                    0  
17         124017516            124017516            129                  0                    0  
18         124077517            124077517            129                  0                    0  
19         124137517            124137517            129                  0                    0  
20         124197518            124197518            129                  0                    0  
21         124257518            124257518            129                  0                    0  
22         124317523            124317523            129                  0                    0  
23         124377526            124377526            129                  0                    0  
24         124437529            124437529            129                  0                    0  
25         124497533            124497533            129                  0                    0  
26         124557536            124557536            129                  0                    0  
27         124617539            124617539            129                  0                    0  
  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
