---
description: dbo.sysdownloadlist (Transact-SQL)
title: dbo.sysdownloadlist (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 34e0ba69d668cd25b902f9decdf75c0039a74fc9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551065"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  すべてのターゲット サーバーに対するダウンロード命令のキューを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|行の自然な挿入シーケンスを提供する id 列。|  
|**source_server**|**sysname**|ソース サーバーの名前。|  
|**operation_code**|**tinyint**|ジョブの操作コード:<br /><br /> **1** = INS (挿入)<br /><br /> **2** = UPD (更新)<br /><br /> **3** = DEL (delete)<br /><br /> **4** = 開始<br /><br /> **5** = 停止|  
|**object_type**|**tinyint**|オブジェクトの種類のコード。|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|オブジェクト ID 番号。|  
|**target_server**|**sysname**|対象サーバーの名前。|  
|**error_message**|**nvarchar(1024)**|ターゲット サーバーが特定の行を処理しているときにエラーが発生した場合のエラー メッセージ。|  
|**date_posted**|**datetime**|ジョブがターゲット サーバーに通知された日付と時刻。|  
|**date_downloaded**|**datetime**|ジョブが最後にダウンロードされた日付と時刻。|  
|**status**|**tinyint**|ジョブの状態:<br /><br /> **0** = まだダウンロードされていません<br /><br /> **1** = 正常にダウンロードされました|  
|**deleted_object_name**|**sysname**|削除されたオブジェクトの名前。|  
  
 <sup>1</sup> **object_id** 列の値には **-1**を指定できます。この値は、 **operation_code** 列の値が DELETE の場合に ALL の値に対応します。  
  
  
