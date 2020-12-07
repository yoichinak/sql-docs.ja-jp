---
title: いくつかの同期のレプリカが同期されていません
description: 同期のレプリカが Always On 可用性グループで同期されていない場合に考えられるいくつかの原因と解決策について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp5synchronized.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: e58ed56e-4c30-42e6-a9fc-a8c401620e02
author: cawrites
ms.author: chadam
ms.openlocfilehash: a8e5fc7b3aa708acc3542082ece0d980c938eb34
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583848"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>いくつかの同期のレプリカが同期されていません
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>はじめに  
  
|||  
|-|-|  
|**ポリシー名**|同期レプリカのデータの同期状態|  
|**問題点**|一部の同期レプリカが同期されていません。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性グループ|  
  
## <a name="description"></a>説明  
 このポリシーは、すべての可用性レプリカのデータ同期状態をロール アップし、期待される状態とは異なる可用性レプリカがないかどうかを確認します。 非同期レプリカが SYNCHRONIZING 状態ではない場合、および同期レプリカが SYNCHRONIZED 状態ではない場合、ポリシーは異常な状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [Some synchronous replicas are not synchronized (一部の同期レプリカが同期されていない)](https://go.microsoft.com/fwlink/p/?LinkId=220853) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この可用性グループには、現在同期されていない同期レプリカが少なくとも 1 つ存在します。 レプリカの同期状態は、SYNCHRONIZING と NOT SYNCHRONIZING のいずれかになります。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 可用性レプリカのポリシーの状態を検索条件として、同期状態が不適切な可用性レプリカを探し、問題を解決してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
