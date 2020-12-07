---
title: SQL Server、Availability Replica | Microsoft Docs
description: Always On 可用性グループの可用性レプリカに関するパフォーマンス カウンターが含まれる SQLServer:Availability Replica パフォーマンス オブジェクトについて説明します。
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: cb04f9a626c63e5e65f73b3de0810a2869ee9841
ms.sourcegitcommit: 2bf83972036bdbe6a039fb2d1fc7b5f9ca9589d3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674158"
---
# <a name="sql-server-availability-replica"></a>SQL Server、Availability Replica

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **SQLServer:Availability Replica** パフォーマンス オブジェクトには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の AlwaysOn 可用性グループの可用性レプリカに関する情報を報告するパフォーマンス カウンターが含まれています。 可用性レプリカのパフォーマンス カウンターはすべてプライマリ レプリカとセカンダリ レプリカの両方に適用され、送信/受信カウンターによってローカル レプリカの状態が示されます。 ほとんどの場合、プライマリ レプリカがデータの大部分を送信し、セカンダリ レプリカがデータを受信します。 ただし、セカンダリ レプリカは、ACK と他のバックグラウンド トラフィックをプライマリ レプリカに送信します。 可用性レプリカでは、ローカル レプリカの現在のロール (プライマリまたはセカンダリ) に応じて一部のカウンターが値 0 を示します。  
  
|カウンター名|説明|  
|------------------|-----------------|  
|**レプリカからの受信バイト数/秒**|**SQL Server 2012 と 2014:** 可用性レプリカから 1 秒あたりに受信した実際のバイト数 (圧縮) (同期または非同期)。 ユーザーによる更新のないデータベースでも、ping と状態の更新でネットワーク トラフィックが発生します。 <BR/> <BR/> **SQL Server 2016 以降:** 可用性レプリカから 1 秒あたりに受信した実際のバイト数 (非同期の場合は圧縮、同期の場合は非圧縮)。|  
|**レプリカへの送信バイト数/秒**|**SQL Server 2012 と 2014:** リモート可用性レプリカにネットワーク経由で 1 秒あたりに送信された実際のバイト数 (圧縮) (同期または非同期)。 同期と非同期どちらのレプリカについても、既定で圧縮が有効になっています。 <BR/> <BR/> **SQL Server 2016 以降:** リモート可用性レプリカに 1 秒あたりに送信されたバイト数。 非同期レプリカの場合は圧縮前。 (圧縮されていない同期レプリカの実際のバイト数)|  
|**トランスポートへの送信バイト数/秒**|**SQL Server 2012 と 2014:** リモート可用性レプリカにネットワーク経由で 1 秒あたりに送信された実際のバイト数 (圧縮) (同期または非同期)。 同期と非同期どちらのレプリカについても、既定で圧縮が有効になっています。 <BR/> <BR/> **SQL Server 2016 以降:** リモート可用性レプリカに 1 秒あたりに送信されたバイト数。非同期レプリカの場合は圧縮前。 (圧縮されていない同期レプリカの実際のバイト数)|  
|**Flow Control Time (ms/sec)**|最後の 1 秒間にログ ストリーム メッセージが送信フロー制御を待機した時間のミリ秒数。|  
|**フロー制御/秒**|最後の 1 秒間に開始されたフロー制御の回数。 **Flow Control Time (ms/sec)** を **Flow Control/sec** で除算すると、平均待機時間が算出されます。|  
|**レプリカからの受信/秒**|レプリカから 1 秒あたりに受信した AlwaysOn メッセージの数。|  
|**再送信メッセージ/秒**|最後の 1 秒間に再送された AlwaysOn メッセージの数。|  
|**レプリカへの送信/秒**|この可用性レプリカに 1 秒あたりに送信された AlwaysOn メッセージの数。|  
|**トランスポートへの送信/秒**|リモート可用性レプリカにネットワーク経由で 1 秒あたりに送信された実際の AlwaysOn メッセージ数。 プライマリ レプリカの場合、これはセカンダリ レプリカに送信されたメッセージ数です。 セカンダリ レプリカの場合、これはプライマリ レプリカに送信されたメッセージ数です。|  
  
## <a name="see-also"></a>参照 
 
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、Database Replica](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Always On 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
