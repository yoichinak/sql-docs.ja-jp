---
title: データベース ミラーリング システム オブジェクト リファレンス |Microsoft Docs
description: データベース ミラーリング システム オブジェクト (システム カタログ ビュー、システム動的管理ビュー、およびシステム テーブル) に関する情報を確認します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0bf290bb61cd5e6eb5cbd3715618b5949df87f8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349200"
---
# <a name="database-mirroring-system-object-reference"></a>データベース ミラーリング システム オブジェクト リファレンス
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="system-catalog-views"></a>システム カタログ ビュー

| システム カタログ ビュー | 説明|
| :------ | :----------------------------- |
| [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   | サーバーがデータベース ミラーリング パートナーシップで果たすすべてのミラーリング監視ロールの行を格納します。 |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>システム動的管理ビュー

| システム動的管理ビュー | 説明|
| :------ | :----------------------------- |
| [sys.dm_db_mirroring_auto_page_repair](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)   | サーバー インスタンス上のミラー化されたデータベースに対して試行されたページの自動修復ごとに 1 行を返します。  |
| [sys.dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)    | データベース ミラーリング用に確立された各接続の行を返します。 |
| &nbsp; | &nbsp; |

## <a name="system-tables"></a>システム テーブル

| システム テーブル | 説明|
| :------ | :----------------------------- |
| [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)   | データベース ミラーリング メンテナンス プランに関する情報を返します。 |
| [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)    | データベース ミラーリング メンテナンス プランの履歴に関する情報を返します。 |
| [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)    |データベース ミラーリング メンテナンス プラン ジョブに関する情報を返します。  |
| [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)    | データベース ミラーリング プランに関する情報を返します。  |
| &nbsp; | &nbsp; |


## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   

  
  
