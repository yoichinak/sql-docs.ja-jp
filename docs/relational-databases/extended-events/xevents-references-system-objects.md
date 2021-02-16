---
title: 拡張イベント関連のシステム オブジェクト
description: これらのリソースは拡張イベントに関連します。たとえば、システム オブジェクトによるサポート方法、SQL Server による使用方法、特に Azure SQL Database に対する側面などです。
ms.date: 03/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jukoesma
ms.technology: xevents
ms.topic: reference
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef31edf367eacd41135bb4db9a58cd8ba4950de8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100346720"
---
# <a name="system-objects-that-support-extended-events"></a>拡張イベントをサポートするシステム オブジェクト

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

この記事では、拡張イベントに関連する他の記事へのリンクを提供します。 それらの記事では、次のことが説明されています。

- 拡張イベント機能のサポートを提供するシステム オブジェクト。
- 拡張イベントが使用されている SQL Server 自体の部分。
- クラウドの Azure SQL Database に固有の拡張イベントの部分。

リストは、必ずしも完全ではありません。

## <a name="system-tables"></a>システム テーブル

- [拡張イベント テーブル - trace_xe_action_map](../system-tables/extended-events-tables-trace-xe-action-map.md)

- [拡張イベント テーブル - trace_xe_event_map](../system-tables/extended-events-tables-trace-xe-event-map.md)

## <a name="system-catalog-views"></a>システム カタログ ビュー

- [拡張イベント カタログ ビュー (Transact-SQL)](../system-catalog-views/extended-events-catalog-views-transact-sql.md)

- [sys.server_event_sessions (Transact-SQL)](../system-catalog-views/sys-server-event-sessions-transact-sql.md)

- [sys.server_event_session_actions (Transact-SQL)](../system-catalog-views/sys-server-event-session-actions-transact-sql.md)

- [sys.server_event_session_events (Transact-SQL)](../system-catalog-views/sys-server-event-session-events-transact-sql.md)

- [sys.server_event_session_fields (Transact-SQL)](../system-catalog-views/sys-server-event-session-fields-transact-sql.md)

- [sys.server_event_session_targets (Transact-SQL)](../system-catalog-views/sys-server-event-session-targets-transact-sql.md)

## <a name="other-system-objects"></a>他のシステム オブジェクト

- [拡張イベントの動的管理ビュー](../system-dynamic-management-views/extended-events-dynamic-management-views.md)

## <a name="uses-of-extended-events-by-sql-server-itself"></a>SQL Server 自体による拡張イベントの使用

この一覧は、完全なものではありません。

- [拡張イベント ログの診断情報へのアクセス](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)

- [Always On 可用性グループの拡張イベントを構成する](../../database-engine/availability-groups/windows/always-on-extended-events.md)

- [Stretch Database の拡張イベント](../../sql-server/stretch-database/extended-events-for-stretch-database.md)

## <a name="azure-sql-database-and-extended-events"></a>Azure SQL Database と拡張イベント

- [Azure SQL Database での拡張イベント](/azure/sql-database/sql-database-xevent-db-diff-from-svr)

- [sys.database_event_session_targets (Azure SQL Database)](../system-catalog-views/sys-database-event-session-targets-azure-sql-database.md)

- [sys.database_event_session_fields (Azure SQL Database)](../system-catalog-views/sys-database-event-session-fields-azure-sql-database.md)

- [sys.database_event_session_events (Azure SQL Database)](../system-catalog-views/sys-database-event-session-events-azure-sql-database.md)

- [sys.database_event_session_actions (Azure SQL Database)](../system-catalog-views/sys-database-event-session-actions-azure-sql-database.md)
