---
title: ポーリング間隔の決定
description: この記事では、Analytics Platform System appliance alerts のポーリング頻度を確認する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafd18a7701ed5de5018a3e8dc23bc8d5d9640fa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767041"
---
# <a name="determine-polling-frequency"></a>ポーリング頻度を決定する
この記事では、Analytics Platform System appliance alerts のポーリング頻度を確認する方法について説明します。  
  
## <a name="to-determine-the-polling-frequency"></a>ポーリング頻度を確認するには  
PDW では、アラートが発生したときにプロアクティブ通知が現在サポートされていないため、監視ソリューションはアプライアンス Dll を継続的にポーリングする必要があります。  内部では、PDW がさまざまな間隔でコンポーネントをポーリングします。  
  
-   クラスター-60 秒  
  
-   ハートビート-60 秒  
  
-   その他すべてのコンポーネント-5 分  
  
-   パフォーマンスカウンター-3 秒  
  
アラートをポーリングする一般的な間隔は、System Center でも使用されます。これは、 **15 分ごと**に行われます。  当然ながら、クエリをより頻繁に実行することもできますが、ポーリングは6時間ごとに行わないことをお勧めします。  
  
ポーリングの頻度は高くなりますが、ポーリングが頻繁に実行されると、 [sys. dm_pdw_nodes_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md?view=sql-server-ver15) DMV が煩雑になる可能性があります。  ポーリングが頻繁に行われると、ユーザーがクエリのパフォーマンスに関する問題を簡単に表示できなくなる可能性があります。  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[アプライアンス監視 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
