---
title: 可用性グループで可用性レプリカの参加が解除されている
description: Always On 可用性グループ内でレプリカの参加が解除されている理由を特定します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: troubleshooting
f1_keywords:
- sql13.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
author: cawrites
ms.author: chadam
ms.openlocfilehash: 371a4e1e76cfeb79eeb83f2dabd159927e044008
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100343881"
---
# <a name="availability-replica-is-disconnected-within-an-always-on-availability-group"></a>Always On 可用性グループ内で可用性レプリカの参加が解除されている
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>はじめに  
  
|||  
|-|-|  
|**ポリシー名**|可用性レプリカの接続状態|  
|**問題点**|可用性レプリカの接続が解除されます。|  
|**カテゴリ**|**重大**|  
|**ファセット**|可用性レプリカ|  
  
## <a name="description"></a>説明  
 このポリシーは、可用性レプリカ間の接続状態を確認します。 可用性レプリカ間の接続状態が DISCONNECTED の場合、ポリシーは通常とは異なる状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
## <a name="possible-causes"></a>考えられる原因  
 セカンダリ レプリカがプライマリ レプリカに接続されていません。 接続状態は DISCONNECTED です。 この問題は、次の状況で発生する可能性があります。  
  
-   接続ポートが他のアプリケーションと競合状態にある。  
  
-   暗号化の種類またはアルゴリズムが一致しない。  
  
-   接続エンドポイントが削除されているか、開始されていない。  
  
-   トランスポートが切断されている。  
  
## <a name="possible-solutions"></a>考えられる解決策  
 この問題に対して考えられる解決策を次に示します。  
  
-   プライマリ レプリカおよびセカンダリ レプリカのインスタンスのデータベース ミラーリング エンドポイントの構成を確認し、対応していない構成を更新します。  
  
-   ポートが競合しているかどうかを確認し、競合している場合はポート番号を変更します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
