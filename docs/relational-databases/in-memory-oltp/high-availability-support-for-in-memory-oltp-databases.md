---
title: 高可用性 - インメモリ OLTP データベース
description: メモリ最適化テーブルを含んだ SQL Server データベースは、ネイティブ コンパイル ストアド プロシージャの有無に関係なく、AlwaysOn 可用性グループで完全にサポートされます。
ms.custom: seo-dt-2019
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 92a09ac4702cae987c4fa5f4ccd420819c29073a
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529433"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>インメモリ OLTP データベースにおける高可用性のサポート
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  メモリ最適化テーブルを含んだデータベースは、ネイティブ コンパイル ストアド プロシージャの有無に関係なく、AlwaysOn 可用性グループで完全にサポートされます。  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] オブジェクトが含まれている場合とそうでない場合とで、データベースの構成とサポートに違いはありません。  

 プライマリ レプリカ上のメモリ最適化テーブルに対する変更は、再実行の間にセカンダリ レプリカのテーブルに適用されます。 これにより、データが既にメモリ内にあるため、セカンダリ レプリカへの迅速なフェールオーバーが可能になります。 テーブルは、読み取りアクセス用に構成されているレプリカのセカンダリに対する読み取りクエリに利用できます。  

  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>AlwaysOn 可用性グループとインメモリ OLTP データベース  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] のコンポーネントを使ってデータベースを構成する場合、次の利点があります。  
  
-   **完全に統合された環境**   
    メモリ最適化テーブルを含んだデータベースは、同期と非同期のどちらのセカンダリ レプリカに対しても同じウィザードを使用して構成でき、同じサポート レベルが適用されます。 加えて、使い慣れた SQL Server Management Studio の AlwaysOn ダッシュボードを使用して、正常性の監視を行うことができます。  
  
-   **同等のフェールオーバー時間**   
    持続性のあるメモリ最適化テーブルのインメモリ状態がセカンダリ レプリカで維持されます。 自動フェールオーバーまたは強制フェールオーバーが発生した場合に復旧の必要がないため、新しいプライマリへのフェールオーバーにかかる時間はディスク ベースのテーブルと変わりありません。 この構成では、SCHEMA_ONLY として作成されたメモリ最適化テーブルがサポートされます。 ただし、これらのテーブルに対する変更はログに記録されないため、セカンダリ レプリカ上のこれらのテーブルにはデータはありません。  
  
-   **[読み取り可能セカンダリ]**    
    セカンダリ レプリカが読み取りアクセス用に構成されている場合、セカンダリ レプリカ上のメモリ最適化テーブルにアクセスしてクエリを実行することができます。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]では、セカンダリ レプリカ上の読み取りタイムスタンプは、プライマリ レプリカ上の読み取りタイムスタンプと同期に近い状態で保たれます。そのため、プライマリ レプリカへの変更はセカンダリにすばやく反映されます。 この同期に近い動作は、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のインメモリ OLTP とは異なります。  

### <a name="considerations"></a>考慮事項

- SQL Server 2019 では、メモリ最適化可用性グループ データベースに対する並列再実行が導入されました。 SQL Server 2016 と 2017 では、可用性グループ内のデータベースがメモリ最適化もされている場合、ディスク ベースのテーブルで並列再実行は使用されません。 
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>フェールオーバー クラスタリング インスタンス (FCI) とインメモリ OLTP データベース  
 共有記憶域構成で高可用性を実現するには、メモリ最適化テーブルを使用するデータベースでフェールオーバー クラスター インスタンスを設定できます。 FCI を設定する場合、次の要素を考慮してください。  
  
-   **目標復旧時間**   
    データベースを使用可能にするには、メモリ最適化テーブルをメモリに読み込む必要があるため、フェールオーバーの所要時間は長くなる可能性があります。  
  
-   **SCHEMA_ONLY テーブル**   
    フェールオーバー後、SCHEMA_ONLY テーブルは、データ行の存在しない空の状態になるので注意してください。 これは仕様であり、アプリケーションで定義された動作です。 1 つ以上の SCHEMA_ONLY テーブルを含む [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースを再起動したときもまったく同じ動作となります。  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>インメモリ OLTP におけるトランザクション レプリケーションのサポート  
 トランザクション レプリケーションのサブスクライバーとして機能するテーブルは、ピア ツー ピア トランザクション レプリケーションを除き、メモリ最適化テーブルとして構成できます。 その他のレプリケーション構成はメモリ最適化テーブルとは互換性がありません。  詳細については、「[メモリ最適化テーブル サブスクライバーへのレプリケーション](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ (AlwaysOn 可用性グループ)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [メモリ最適化テーブル サブスクライバーへのレプリケーション](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
