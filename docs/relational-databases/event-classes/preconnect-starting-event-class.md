---
description: PreConnect:Starting イベント クラス
title: PreConnect:Starting イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b5f452391bb263054018bbff5f615e35866b7fd6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181378"
---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting イベント クラス
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  PreConnect:Starting イベント クラスは、LOGON トリガーまたはリソース ガバナーの分類関数が実行を開始したことを示します。  
  
## <a name="preconnectstarting-event-class-data-columns"></a>PreConnect:Starting イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|いいえ|  
|SPID|**int**|このイベントを発生させるサーバー プロセスの ID。|12|はい|  
|EventSubClass|**int**|ユーザー定義の分類子関数の場合は 1。|21|はい|  
|StartTime|**datetime**|ユーザー定義の分類子関数が開始された時刻。|14|はい|  
|ObjectID|**int**|ユーザー定義の分類オブジェクトの ID。|22|はい|  
|ObjectName|**nvarchar (256)**|ユーザー定義の分類子関数の 2 部構成の名前 (dbo.classifier など)。|34|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Completed イベント クラス](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)  
  
  
