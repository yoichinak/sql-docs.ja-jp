---
title: PolyBase スケールアウト グループ | Microsoft Docs
description: PolyBase グループ機能を使用し、SQL Server インスタンスのクラスターを作成します。 これにより、外部ソースからの大規模なデータ セットのクエリ パフォーマンスが向上します。
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sql13.swb.polybasescaleoutcluster.page.f1
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 11462e9c55f22e16fb3e20920c104bf1047d8991
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523857"
---
# <a name="polybase-scale-out-groups"></a>PolyBase スケールアウト グループ

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

PolyBase を使用するスタンドアロンの SQL Server インスタンスは、Hadoop または Azure BLOB ストレージの大量のデータ セットを処理する場合、パフォーマンス ボトルネックになる可能性があります。 PolyBase グループ機能では、Hadoop や Azure BLOB ストレージなどの外部データ ソースからの大量のデータ セットを、クエリ パフォーマンスの向上のためにスケールアウト形式で処理するために、SQL Server インスタンス クラスターを作成することができます。 これで、ワークロードで要求されるパフォーマンスを満たすように、お使いの SQL Server のコンピューティングをスケーリングできます。 SQL Server インスタンスのグループの PolyBase スケールアウト グループでは、並列処理アーキテクチャで大規模な外部データ セットを処理できます。 このグループに、SQL Server インスタンスを追加するほど、データの読み込みおよびクエリのパフォーマンスは線形に増加します。 
  
「 [PolyBase の概要](./polybase-guide.md) 」および「 [PolyBase ガイド](../../relational-databases/polybase/polybase-guide.md)」を参照してください。
  
![PolyBase スケールアウト グループを示す図。](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase スケールアウト グループ")  
  
## <a name="head-node"></a>ヘッド ノード  

ヘッド ノードには、PolyBase クエリの送信先の SQL Server インスタンスが含まれています。 各 PolyBase グループは、ヘッド ノードを 1 つだけ保持できます。 ヘッド ノードは、SQL Server インスタンス上の SQL データベース エンジン、PolyBase エンジン、および PolyBase データ移動サービスの論理グループです。
  
## <a name="compute-node"></a>コンピューティング ノード  

コンピューティング ノードには、外部データに対するスケールアウト クエリ処理を支援する SQL Server インスタンスが含まれています。 コンピューティング ノードは、SQL Server インスタンス上の SQL Server と PolyBase データ移動サービスの論理グループです。 PolyBase グループは、複数のコンピューティング ノードを保持できます。 ヘッド ノードとコンピューティング ノードはすべて、同じバージョンの SQL Server を実行する必要があります。

## <a name="scale-out-reads"></a>スケールアウト読み取り

外部の SQL Server に対してクエリを実行する場合、Oracle インスタンスまたは Teradata インスタンス、パーティション分割されたテーブルには、読み取りスケールアウトのメリットがあります。 PolyBase スケールアウト グループの各ノードは、外部データを読み取るのに、最大 8 つのリーダーにスピンできます。 そして各リーダーには、読み取る外部テーブルのパーティションが 1 つ割り当てられます。 

たとえば、SQL Server の外部テーブルに月ごとに 12 のパーティションがあり、3 つのノードの PolyBase スケールアウト グループがあるとします。各ノードは、12 のそれぞれのパーティションの処理に 4 つの PolyBase リーダーを使用します。 これを次の図で示します。 

> [!NOTE]
>  これは Hadoop を介したスケールアウト読み取りとは異なります。 

![PolyBase スケールアウト読み取り](../../relational-databases/polybase/media/polybase-scale-out-groups2.png "PolyBase スケールアウト グループ")
  
## <a name="distributed-query-processing"></a>分散クエリ処理  

PolyBase クエリは、ヘッド ノード上の SQL Server に送信されます。 外部テーブルを参照するクエリの一部は、PolyBase エンジンに渡されます。
  
PolyBase エンジンは、PolyBase クエリの背後にある重要なコンポーネントです。 外部データに対するクエリを解析し、クエリ プランを生成して、作業を実行するためにコンピューティング ノード上のデータ移動サービスに配布します。 作業が完了すると、コンピューティング ノードから結果を受信し、この結果を処理してクライアントに返すために SQL Server に送信します。
  
PolyBase データ移動サービスは、PolyBase エンジンから指示を受信し、HDFS と SQL Server の間、およびヘッド ノードとコンピューティング ノード上の SQL Server インスタンス間でデータを転送します。
  
## <a name="next-steps"></a>次のステップ

PolyBase スケールアウト グループを構成するには、次のガイドを参照してください。

[Windows で PolyBase スケールアウト グループを改善する](configure-scale-out-groups-windows.md)

## <a name="see-also"></a>参照

 [sys-dm-exec-compute-nodes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)   
 [sys-dm-exec-compute-node-status](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)   
 [sys.dm_exec_compute_node_errors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)