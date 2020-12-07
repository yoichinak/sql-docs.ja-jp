---
description: Database イベント カテゴリ
title: Database イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9bf211c6028f24d84a6281d31c29df94b814239e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494344"
---
# <a name="database-event-category"></a>Database イベント カテゴリ
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Database** イベント カテゴリには、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]を監視するためのイベント クラスが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Data File Auto Grow イベント クラス](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)|データ ファイルが自動的に拡張されたことを示します。 データ ファイルが ALTER DATABASE により明示的に拡張された場合、このイベントはトリガーされません。|  
|[Data File Auto Shrink イベント クラス](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)|データ ファイルが圧縮されたことを示します。|  
|[Database Mirroring Connection イベント クラス](../../relational-databases/event-classes/database-mirroring-connection-event-class.md)|データベース ミラーリングのトランスポート接続のステータスをレポートするために生成されるイベントです。|  
|[Database Mirroring State Change イベント クラス](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)|ミラー化されたデータベースの状態が変更された時点を示します。|  
|[Database Suspect Data Page イベント クラス](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)|**msdb** データベースの **suspect_pages** テーブルにページが加わった時点を示します。|  
|[Log File Auto Grow イベント クラス](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)|ログ ファイルが自動的に拡張されたことを示します。 ログ ファイルが ALTER DATABASE により明示的に拡張された場合、このイベントはトリガーされません。|  
|[Log File Auto Shrink イベント クラス](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|ログ ファイルが自動的に拡張されたことを示します。 ログ ファイルが ALTER DATABASE により明示的に圧縮された場合、このイベントはトリガーされません。|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
