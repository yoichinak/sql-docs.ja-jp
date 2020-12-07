---
title: 一部の可用性データベースのデータ同期状態が正常ではない
description: Always On 可用性グループのデータベースのデータ同期状態が正常でない理由の考えられる原因を特定します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: end-user-help
f1_keywords:
- sql13.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
author: cawrites
ms.author: chadam
ms.openlocfilehash: b95864974db04a3ce32c2e86b48680b24955d88d
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584403"
---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>一部の可用性データベースのデータ同期状態が正常ではない
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>はじめに  
  
|||  
|-|-|  
|**ポリシー名**|可用性レプリカのデータの同期状態|  
|**問題点**|一部の可用性データベースのデータ同期状態が正常ではありません。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性レプリカ|  
  
## <a name="description"></a>説明  
 このポリシーは、可用性データベース ("データベース レプリカ" とも呼ばれます) のデータの同期状態をチェックします。 データの同期状態が NOT SYNCHRONIZING である (同期コミット データベース レプリカでは、状態が SYNCHRONIZED 以外である) 場合、ポリシーは異常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [可用性データベースのデータ同期状態が正常でない](https://go.microsoft.com/fwlink/p/?LinkId=220863) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 データの同期状態に異常の見られる可用性データベースがレプリカに少なくとも 1 つ存在します。 これが非同期コミット可用性レプリカである場合は、すべての可用性データベースが SYNCHRONIZING 状態である必要があります。 同期コミットの可用性レプリカである場合、すべての可用性データベースが SYNCHRONIZED 状態であることが必要です。 この問題は、次の状況で発生する可能性があります。  
  
-   可用性レプリカが切断されている。  
  
-   データの移動が中断されている。  
  
-   データベースにアクセスできない。  
  
-   ネットワークの待機時間やプライマリ/セカンダリ レプリカへの負荷が原因で一時的に遅延の問題が生じている。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 接続の問題やデータの移動の中断が見られるようであればすべて解決します。 SQL Server Management Studio を使用してこの問題に対応するイベントをチェックし、データベース エラーを見つけます。 特定のエラーのトラブルシューティングの手順を実行します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
