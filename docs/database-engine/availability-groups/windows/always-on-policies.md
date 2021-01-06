---
title: 可用性グループの正常性に対するグループ ポリシーの使用
description: Always On ダッシュ ボードで、可用性グループの正常性の情報の提供に使用される、グループ システム ポリシーを表示する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: how-to
ms.assetid: 26bf8f71-c2b8-45ef-b3a3-372b96c9e6e3
author: rothja
ms.author: jroth
ms.openlocfilehash: f2f6357e434e4a8d4d6385de10cac58c7bd6f2d0
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641439"
---
# <a name="evaluate-health-of-the-always-on-availability-group-using-group-policies"></a>グループ ポリシーを使用した Always On 可用性グループの正常性の評価
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Always On 可用性グループのシステム ポリシーは、ユーザーに可用性グループの正常性に関する情報を提供するために Always On ダッシュボードで使用されます。 それらは、可用性グループの運用上の問題の初期のトラブルシューティングに役立ちます。 これらのポリシーは、拡張して Always On ダッシュボードをカスタマイズするために使用したり、目的の正常性に関する情報をレポートするためにすぐに実行したりすることができます。  
  
 可用性グループに 14 のシステム ポリシーがあります。 各ポリシーの詳細については、「[AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)」を参照してください。  
  
## <a name="view-or-evaluate-availability-groups-system-policies"></a>可用性グループのシステム ポリシーの表示または評価  
 SQL Server Management Studio (SSMS) で可用性グループのシステム ポリシーを表示または実行するには、次の操作を行います。  
  
1.  **オブジェクト エクスプローラー** で、 **[管理]** 、 **[ポリシー管理]** 、 **[ポリシー]** 、 **[システム ポリシー]** の順に展開します。  
  
2.  ポリシーのいずれかを右クリックし、 **[評価]** をクリックします。 選択したポリシーを評価する場合は、これで終了です。 **[対象の詳細]** ボックスで、 **[表示]** をクリックして、評価の結果の詳細を表示することができます。  
  
3.  すべての可用性グループのシステム ポリシーを表示するには、 **[ページの選択]** ウィンドウで **[ポリシーの選択]** をクリックします。  
  
## <a name="next-steps"></a>次のステップ  
 [AlwaysOn の正常性モデル: パート 2: 正常性モデルの拡張](/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model)   
  
