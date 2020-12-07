---
title: ログ配布レポートの表示 (SSMS)
description: SQL Server Management Studio のトランザクション ログの配布の状態レポートを表示します。 監視サーバー、プライマリ サーバー、またはセカンダリ サーバーで状態レポートを実行します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- viewing log shipping reports
- displaying log shipping reports
- log shipping [SQL Server], monitoring
- log shipping [SQL Server], viewing reports
ms.assetid: 3b549f2f-3683-45e5-b8e8-8095276c41ab
author: cawrites
ms.author: chadam
ms.openlocfilehash: 4ee1de4f9d231c2fa3be91cab2010eb1aad358f8
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130734"
---
# <a name="view-the-log-shipping-report-sql-server-management-studio"></a>ログ配布レポートの表示 (SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でトランザクション ログの配布の状態レポートを表示する方法について説明します。 状態レポートは、監視サーバー、プライマリ サーバー、またはセカンダリ サーバーで実行できます。 ログ配布構成に関する完全な情報を表示するには、監視サーバーのインスタンスでレポートを表示します。  
  
 このレポートには、接続先のサーバー インスタンスから使用できるログ配布の利用状況の状態が表示されます。 接続先のサーバー インスタンスが複数の構成に関与しており、それぞれ異なる役割が与えられている場合 (あるデータベースでは監視サーバーとして機能し、別のデータベースではセカンダリ サーバーとして機能する場合など) は、それぞれの役割から見た各構成の情報が表示されます。 ストアド プロシージャから特定のログ配布構成の監視サーバー インスタンスに接続できる場合、レポートにはその構成の状態がさらに多く表示されます。  
  
 現在のサーバー インスタンスによって実行される役割ごとに、次の情報を表示できます。  
  
|Role|表示される情報|  
|----------|---------------------------|  
|モニター|このサーバー インスタンスを監視サーバーとして使用するすべてのプライマリ サーバーとセカンダリ サーバーの名前と状態。|  
|プライマリ|プライマリ データベースごとの、現在のサーバー インスタンスの (プライマリ サーバーとしての) 状態と名前、およびプライマリ データベース名。 このレポートには、(プライマリ サーバーのローカルに格納された) バックアップ ジョブの状態が表示されます。<br /><br /> また、このレポートには、対応するセカンダリ サーバーごとに 1 行のデータが含まれます。 構成に監視サーバーを使用していて、ストアド プロシージャからそのモニターに接続できる場合は、これらの行に最新のログ バックアップのコピー状態と復元状態が表示されます。|  
|セカンダリ|セカンダリ データベースごとの、現在のサーバー インスタンスの (セカンダリ サーバーとしての) 状態と名前、およびセカンダリ データベース名。<br /><br /> このレポートには、セカンダリ サーバーでのコピー ジョブと復元ジョブの状態が表示されます。<br /><br /> また、このレポートには、対応するプライマリ サーバーのデータが 1 行含まれます。 構成に監視サーバーを使用していて、ストアド プロシージャからそのモニターに接続できる場合は、この行に最新のログ バックアップの状態が表示されます。|  
  
 表示される情報は、サーバー インスタンスが監視サーバー、プライマリ サーバー、セカンダリ サーバーのいずれであるかによって異なります。 使用できる情報がない場合は、対応するセルがグレーで表示されます。  
  
 レポートでは、**sp_help_log_shipping_monitor** を呼び出してデータを取得します。 必要なアクセス許可については、「[sp_help_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)」を参照してください。  
  
### <a name="to-display-the-transaction-log-shipping-status-report-on-a-server-instance"></a>サーバー インスタンスでのトランザクション ログの配布の状態レポートを表示するには  
  
1.  監視サーバー、プライマリ サーバー、またはセカンダリ サーバーのいずれかに接続します。  
  
2.  オブジェクト エクスプローラーで、サーバー インスタンスを右クリックして **[レポート]** をポイントし、 **[標準レポート]** をクリックします。  
  
3.  **[トランザクション ログの配布の状態]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ログ配布の監視 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
  
