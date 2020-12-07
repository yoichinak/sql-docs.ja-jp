---
description: レプリケーション モニターを使用したパフォーマンスの監視
title: レプリケーション モニターを使用したパフォーマンスの監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Log Reader Agent, monitoring
- Replication Monitor, performance
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication]
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a881bfd928d8a8d1c84d85ea8d226bc2751126a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498745"
---
# <a name="monitor-performance-with-replication-monitor"></a>レプリケーション モニターを使用したパフォーマンスの監視
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション モニターを使用すると、トランザクション レプリケーションとマージ レプリケーションのパフォーマンスを次の方法で監視できます。  
  
-   警告およびしきい値の設定  
  
-   パフォーマンス測定値の表示  
  
-   トレーサー トークンによる待機時間の判断 (トランザクション レプリケーション)  
  
-   詳細な同期統計情報の表示 (マージ レプリケーション)  
  
-   トランザクションおよび配信時間の表示 (トランザクション レプリケーション)  
  
## <a name="set-warnings-and-thresholds"></a>警告としきい値の設定  
 レプリケーション モニターでは、多くのパフォーマンス条件に対して警告を有効にできます。 警告を有効にする際には、しきい値を指定します。 しきい値に達したり、しきい値を超えると、サブスクリプションおよびそのサブスクリプションが同期しているパブリケーションの **[状態]** 列に警告が表示されます。 しきい値に到達した場合は、レプリケーション モニターに警告を表示でき、さらに通知を発行することができます。 以下のようなパフォーマンス条件について、警告を有効にできます。  
  
-   指定した待機時間 (パブリッシャーでトランザクションがコミットされてから、対応するトランザクションがサブスクライバーでコミットされるまでの経過時間) の超過  
  
     トランザクション レプリケーションに適用できます。 指定したしきい値に達したり、それを超えたりすると、状態が " **パフォーマンス クリティカル**" と表示されます。  
  
-   指定した同期時刻を超えた場合。  
  
     マージ レプリケーションに適用できます。 指定したしきい値に達したり、それを超えたりすると、状態が " **長期マージ**" と表示されます。 ダイヤルアップ接続とローカル エリア ネットワーク (LAN) 接続にそれぞれ別のしきい値を指定できます。  
  
-   指定した数の行を特定の時間内で処理できない場合。  
  
     マージ レプリケーションに適用できます。 指定したしきい値に達したり、それを超えたりすると、状態が " **パフォーマンス クリティカル**" と表示されます。 ダイヤルアップ接続と LAN 接続にそれぞれ別のしきい値を指定できます。  
  
 詳細については、「 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。  
  
## <a name="view-performance-measurements"></a>パフォーマンス測定値の表示  
 レプリケーション モニターでは、パブリケーションの **[現在の平均パフォーマンス]** 列と **[現在の最低パフォーマンス]** 列、およびサブスクリプションの **[パフォーマンス]** 列に、トランザクション レプリケーションおよびマージ レプリケーションのパフォーマンスの品質を示す値が表示されます。 値は次のとおりです。  
  
-   非常に良い  
  
-   良い  
  
-   普通  
  
-   悪い  
  
-   重大 (トランザクション レプリケーションの場合のみ)  
  
 値は、以下のように決定されます。  
  
-   トランザクション レプリケーションの場合、パフォーマンス品質は待機時間のしきい値によって決定されます。 しきい値が設定されていない場合、値は表示されません。 次の表は、しきい値とパフォーマンス品質値の相関関係を示しています。 たとえば、しきい値が 60 秒に設定されている場合に、実際の待機時間が 30 秒であるとすると、待機時間はしきい値の 50% となり、値は [良い] になります。  
  
    |非常に良い|良い|普通|悪い|重要|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   マージ レプリケーションの場合、パフォーマンス品質は、しきい値とは関係ありません (行処理しきい値は、 **[パフォーマンス クリティカル]** の値を **[状態]** 列に表示するかどうかを決定します)。 パフォーマンス品質は、個々のサブスクリプション パフォーマンスを、接続の種類 (ダイヤルアップまたは LAN) が同じパブリケーションのサブスクリプションの平均的な過去のパフォーマンスと比較することで決定されます。 レプリケーション モニターには、50 以上の変更を伴う同期がそれぞれ同じ種類の接続により 5 回行われた後で、値が表示されます。 50 以上の変更に伴う同期が 5 回未満の場合、または最も最近の同期での変更が 50 未満の場合、レプリケーション モニターには値は表示されません。  
  
     次の表は、平均パフォーマンスとパフォーマンス品質値の相関関係を示しています。 たとえば、10 個のサブスクライバーが 1 秒あたり平均 100 行の速度で LAN 接続経由で同期し、サブスクリプションの 1 つが 1 秒あたり 125 行の速度で同期している場合、そのサブスクライバーの同期のパフォーマンスは平均の 125% となり、結果は [良い] となります。  
  
    |非常に良い|良い|普通|悪い|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 サブスクリプション情報の表示に関する詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
## <a name="determine-latency-with-tracer-tokens"></a>トレーサー トークンによる待機時間の判断  
 トランザクション レプリケーションでは、パブリケーション データベースのトランザクション ログにトークン (少量のデータ) を挿入し、それがディストリビューターおよびサブスクライバーに到達するまでにかかった時間を記録することにより、システムの待機時間を計測できます。 このトークンを使用すると、データがディストリビューターまたはサブスクライバーに到達しているかどうかを識別することもできます。 詳細については、「 [トランザクション レプリケーションの待機時間の計測および接続の検証](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)」を参照してください。  
  
## <a name="view-detailed-synchronization-performance-for-merge-replication"></a>マージ レプリケーションの詳細な同期パフォーマンスの表示  
 マージ レプリケーションの場合、レプリケーション モニターには、同期中に処理される各アーティクルの詳細な統計情報が表示されます。この統計には、各処理フェーズ (変更のアップロードやダウンロードなど) にかかる時間などが含まれます。 この情報によって、速度低下の原因となっているテーブルを特定することができます。マージ サブスクリプションのパフォーマンスに関するトラブルシューティングを、この情報から開始することをお勧めします。 詳細な統計情報を表示する方法について詳しくは、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
## <a name="view-transactions-and-delivery-time-for-transactional-replication"></a>トランザクション レプリケーションのトランザクションおよび配信時間の表示  
 トランザクション レプリケーションの場合、レプリケーション モニターには、サブスクライバーにまだ配布されていないディストリビューション データベース内のトランザクションの数と、これらのトランザクションの予測配布時間が表示されます。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーションの監視](../../../relational-databases/replication/monitor/monitoring-replication.md)   
 [レプリケーション モニターのしきい値と警告の設定](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
