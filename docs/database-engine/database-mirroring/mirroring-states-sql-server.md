---
title: ミラーリング状態 (SQL Server) | Microsoft Docs
description: SQL Server のデータベース ミラーリング セッションでのデータベースの状態について説明します。 この状態は、通信状態、データ フロー、データの違いを反映します。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- PENDING_FAILOVER state
- mirroring states [SQL Server]
- DISCONNECTED state
- SYNCHRONIZING state
- SYNCHRONIZED state
- SUSPENDED state
- database mirroring [SQL Server], states
ms.assetid: 90062917-74f9-471b-b49e-bc153ae1a468
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9ddea06e3cfb348ef6355f95137ce93ea459dced
ms.sourcegitcommit: f7c9e562d6048f89d203d71685ba86f127d8d241
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2020
ms.locfileid: "90042794"
---
# <a name="mirroring-states-sql-server"></a>ミラーリング状態 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  データベース ミラーリング セッション中、ミラー化されたデータベースは常に特定の状態 ( *ミラーリング状態*) にあります。 データベースの状態は、通信状態、データ フロー、およびパートナー間のデータの違いを反映します。 データベース ミラーリング セッションには、プリンシパル データベースと同じ状態が採用されます。  
  
 各サーバー インスタンスは、データベース ミラーリング セッション全体を通して相互に監視します。 各パートナーは、ミラーリング状態を使用してデータベースを監視します。 プリンシパル データベースとミラー データベースは、フェールオーバー保留中状態の場合を除いて常に同じ状態になります。 ミラーリング監視サーバーがセッションに対して設定されている場合、各パートナーは、それぞれの接続状態 (接続または切断) を使用してミラーリング監視サーバーを監視します。  
  
 次の表に、考えられるミラーリング状態を示します。  
  
|ミラーリング状態|説明|  
|---------------------|-----------------|  
|SYNCHRONIZING|ミラー データベースの内容が、プリンシパル データベースの内容に遅れています。 プリンシパル サーバーからミラー サーバーにログ レコードを送信しています。ミラー サーバーでは、ミラー データベースをロールフォワードするために変更を適用しています。<br /><br /> データベース ミラーリング セッションの開始時、データベースは同期中状態にあります。 プリンシパル サーバーはデータベースとして機能しており、ミラー サーバーは遅延を解消しようとしています。|  
|SYNCHRONIZED|ミラー サーバーがプリンシパル サーバーとの遅延を解消すると、ミラーリング状態が同期状態になります。 プリンシパル サーバーがミラー サーバーに変更を送信し、ミラー サーバーがミラー データベースに変更を適用する、という処理が継続されている限り、データベースはこの状態のままです。<br /><br /> トランザクションの安全性が FULL に設定されている場合、同期状態では自動フェールオーバーと手動フェールオーバーの両方がサポートされます。フェールオーバー後のデータの損失はありません。<br /><br /> トランザクションの安全性が無効な場合は、同期状態の場合でも、一部データの損失の可能性が常にあります。<br /><br /> SQL Server Management Studio で、データベースの状態は [復元中] と表示されます。 実際の状態については、[sys.database_mirroring](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) の `mirroring_state_desc` 列をクエリしてください。 |  
|SUSPENDED|データベースのミラー コピーは使用できない状態です。 プリンシパル データベースがミラー サーバーにログを送信せずに、実行されています。この状態を *不安定な実行*と呼びます。 この状態はフェールオーバー後に発生します。<br /><br /> また、セッションは、再実行エラーの結果として、または管理者がセッションを一時停止した場合、中断状態になることがあります。<br /><br /> 中断状態は持続状態であり、パートナーがシャットダウンや起動を行っても保持されます。|  
|PENDING_FAILOVER|この状態は、フェールオーバーが開始された後、サーバーがまだミラーの役割に移行していない状態であり、プリンシパル サーバーだけで発生します。<br /><br /> フェールオーバーが開始されると、プリンシパル データベースはフェールオーバー保留中状態になり、すべてのユーザー接続をすばやく終了し、その後すぐにミラーの役割を引き継ぎます。|  
|DISCONNECTED|パートナーが、他のパートナーと通信できなくなった状態です。|  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
