---
description: dbo.systargetservers (Transact-sql)
title: dbo.systargetservers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ecf738591688ba3ad25c58f6b77dabec5df73b2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538319"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マルチサーバー操作ドメインに現在参加しているターゲット サーバーを記録します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|サーバー ID。|  
|**server_name**|**sysname**|サーバー名。|  
|**location**|**nvarchar(200)**|指定したターゲット サーバーの場所。|  
|**time_zone_adjustment**|**int**|グリニッジ標準時 (GMT) との時差 (時間数単位)。|  
|**enlist_date**|**datetime**|指定したターゲット サーバーが参加した日付と時刻。|  
|**last_poll_date**|**datetime**|ジョブを実行するために、指定された対象サーバーがマルチサーバーの **sysdownloadlist** システムテーブルを最後に呼び出した日時。|  
|**status**|**int**|対象サーバーの状態:<br /><br /> **1** = 通常<br /><br /> **2** = 再同期の保留中<br /><br /> **4** = オフラインの疑いあり|  
|**local_time_at_last_poll**|**datetime**|対象サーバーがジョブ操作のために最後にポーリングされた日付と時刻。|  
|**enlisted_by_nt_user**|**nvarchar (100)**|対象サーバーで **sp_msx_enlist** を実行しているユーザーのユーザー名。|  
|**poll_internal**|**int**|対象サーバーがマスターサーバーをポーリングして新しいダウンロード命令を行うまでの秒数。|  
  
  
