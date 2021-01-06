---
title: 'データベース ミラーリング: 相互運用性と共存'
description: SQL Server データベース ミラーリングと他の SQL Server 機能 (フルテキスト カタログやデータベース スナップショットなど) との相互運用性および共存について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9c53b98e4c355348233a4bac050a91ba7d3812f6
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97642047"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>データベース ミラーリング: 相互運用性と共存 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  データベース ミラーリングは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の次の機能またはコンポーネントと共に使用できます。  
  
-   [Always On フェールオーバー クラスター インスタンス (SQL Server フェールオーバー クラスタリング)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [変更データ キャプチャと変更の追跡](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [データベース スナップショット](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [フルテキスト カタログ](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [ログ配布](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [レプリケーション](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 データベース ミラーリングは、次の機能との相互運用はできません。  
  
-   複数データベースにまたがるトランザクション/分散トランザクション  
  
     このようなトランザクションがサポートされない理由の詳細については、「[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
