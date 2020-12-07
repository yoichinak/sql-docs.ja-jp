---
title: インメモリ OLTP ガベージ コレクション | Microsoft Docs
description: SQL Server におけるインメモリ OLTP のガベージ コレクションについて説明します。 アクティブでなくなったトランザクションが行を削除すると、ガベージ コレクションの対象となります。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 940140a7-4785-46fc-8bf4-151435dccd3c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 92a1137dd1fa20ad2a6748be9309d812fdfc38f6
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866760"
---
# <a name="in-memory-oltp-garbage-collection"></a>インメモリ OLTP ガベージ コレクション
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  アクティブでなくなったトランザクションで削除されたデータ行は古いと見なされます。 古い行は、ガベージ コレクションに適しています。 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]のガベージ コレクションには、次のような特性があります。  
  
-   非ブロッキング。 ガベージ コレクションは、ワークロードへの影響を最小限に抑えながら、時間的に分散されます。  
  
-   協調。 ユーザー トランザクションは、garbage-collection のメイン スレッドと共にガベージ コレクションに参加します。  
  
-   効率的。 ユーザー トランザクションにより、使用されているアクセス パス (インデックス) の古い行とのリンクが解除されます。 これにより、行が最終的に削除されるときに必要な作業が少なくなります。  
  
-   応答性。 メモリが不足すると積極的にガベージ コレクションが実行されます。  
  
-   スケーラブル。 コミット後、ユーザー トランザクションによりガベージ コレクションの作業の一部が実行されます。 トランザクション アクティビティが多くなるほど、古い行とのリンクを解除するトランザクションが多くなります。  
  
 ガベージ コレクションは、ガベージ コレクションのメイン スレッドによって制御されます。 ガベージ コレクションのメイン スレッドは、1 分ごとに、またはコミット済みトランザクションの数が内部しきい値を超えたときに実行されます。 ガベージ コレクターのタスクを次に示します。  
  
-   最も古いアクティブなトランザクションより前に、行セットを削除または更新し、コミットしたトランザクションを特定します。  
  
-   これらの古いトランザクションによって作成された行バージョンを特定します。  
  
-   古い行を 16 行ごとの 1 つ以上の単位にグループ化します。 その目的は、ガベージ コレクターの作業を小さな単位に分散することです。  
  
-   各スケジューラに 1 つずつ、これらの作業単位をガベージ コレクション キューに移動します。 これらのガベージ コレクター DMV の詳細については、「[sys.dm_xtp_gc_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md)」、「[sys.dm_db_xtp_gc_cycle_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md)」、および「[sys.dm_xtp_gc_queue_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)」を参照してください。  
  
 ユーザー トランザクションは、コミット後に、そのトランザクションが実行されているスケジューラに関連付けられたすべてのキュー項目を特定し、メモリを解放します。 スケジューラのガベージ コレクションのキューが空の場合は、現在の NUMA ノードの空でないキューを検索します。 トランザクション アクティビティが低レベルで、メモリに負荷がかかっている場合、ガベージ コレクターのメイン スレッドは、任意のキューからガベージ コレクト行にアクセスできます。 (たとえば) 大量の行を削除したため、トランザクション アクティビティがなく、メモリにも負荷がかかっていない場合は、トランザクション アクティビティが再開されるか、メモリに負荷がかかってくるまで、削除された行のガベージ コレクションは実行されません。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP のメモリ管理](/previous-versions/sql/sql-server-2016/dn465872(v=sql.130))  
  
