---
description: Deadlock Graph イベント クラス
title: Deadlock Graph イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Deadlock Graph event class
ms.assetid: 20f92233-c912-4382-8993-8e2e23d03fbe
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1a2f0ff2d9798534358e57f56c5952d6b4746807
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428534"
---
# <a name="deadlock-graph-event-class"></a>Deadlock Graph イベント クラス
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **Deadlock Graph** イベント クラスでは、デッドロックの XML 表記の説明が提供されます。 このクラスは **Lock:Deadlock** イベント クラスと同時に発生します。  
  
## <a name="deadlock-graph-event-class-data-columns"></a>Deadlock Graph イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|イベントの種類 = 148。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。 このイベントでは、この値は常に 1 です。|60|はい|  
|**LoginName**|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログイン、または DOMAIN\username の形式で表された [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。 このイベントでは、この値は常にシステム ユーザーです。|11|はい|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。 このイベントでは、この値は常にシステム ユーザーの SID です。|41|はい|  
|**ServerName**|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|デッドロックが検出された時刻。|14|はい|  
|**TextData**|**ntext**|デッドロックの XML 表記による説明。|1|はい|  
|**TransactionID**|**bigint**|使用しません。|4|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Lock:Deadlock イベント クラス](../../relational-databases/event-classes/lock-deadlock-event-class.md)  
  
  
