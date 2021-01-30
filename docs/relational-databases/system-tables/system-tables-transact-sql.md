---
description: システム テーブル (Transact-SQL)
title: システムテーブル (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
author: cawrites
ms.author: chadam
ms.openlocfilehash: a6ab9da1443f2ce4e6b51e7d6bc995bbb9591a2b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203590"
---
# <a name="system-tables-transact-sql"></a>システム テーブル (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このセクションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内のシステム テーブルについて説明します。  
  
 システムテーブルは、ユーザーが直接変更することはできません。 たとえば、システム テーブルを DELETE、UPDATE、INSERT ステートメント、またはユーザー定義のトリガーで変更しないでください。  
  
 システム テーブル内の列で、このドキュメントに記載されている列の参照は許可されています。 ただし、システム テーブルの列の多くは記載されていません。 ドキュメントに記載されていない列を直接照会するようにアプリケーションを作成することはできません。 代わりに、システム テーブル内に保存されている情報を取得するには、アプリケーションでは次のコンポーネントのいずれかを使用します。  
  
-   システム ストアド プロシージャ  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと関数  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO)  
  
-   レプリケーション管理オブジェクト (RMO)  
  
-   データベース API カタログ関数  
  
 これらのコンポーネントは、からシステム情報を取得するための公開された API を構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、これらのコンポーネントとリリース間の互換性が維持されます。 システム テーブルの形式は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部アーキテクチャに依存し、リリースごとに変化する可能性があります。 このため、ドキュメントに記載されていないシステム テーブルの列に直接アクセスするアプリケーションを作成すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最新バージョンにアクセスするために変更を余儀なくされることがあります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 システムテーブルのトピックは、次の機能領域によって整理されています。  

:::row:::
    :::column:::
        [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)

        [変更データ キャプチャのテーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)

        [データベースメンテナンスプランテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)

        [SQL Server 拡張イベント テーブル &#40;Transact-SQL&#41;](../../relational-databases/extended-events/xevents-references-system-objects.md#system-tables)

        [Integration Services テーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)
    :::column-end:::
    :::column:::
        [ログ配布テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)

        [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)

        [SQL Server エージェントテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)

        [sys.sysoledbusers &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)

        [systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [互換性ビュー &#40;Transact-sql&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
