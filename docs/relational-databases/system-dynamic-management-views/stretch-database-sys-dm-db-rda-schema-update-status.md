---
title: sys.dm_db_rda_schema_update_status (Transact-sql) |Microsoft Docs
description: データベース内の各 Stretch 対応テーブルのリモートデータアーカイブのスキーマ更新タスクごとに1行のデータを格納 sys.dm_db_rda_schema_update_status 方法について説明します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 955f06ba0a7ad991ffe979fc927dfabe6e5a8dd0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202419"
---
# <a name="stretch-database---sysdm_db_rda_schema_update_status"></a>Stretch Database-sys.dm_db_rda_schema_update_status
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  現在のデータベース内の各 Stretch 対応テーブルのリモートデータアーカイブのスキーマ更新タスクごとに1行のデータを格納します。 タスクは、タスク id によって識別されます。  
  
 **dm_db_rda_schema_update_status** は、現在のデータベースコンテキストにスコープが設定されています。 スキーマの更新状態を確認する Stretch が有効なテーブルのデータベースコンテキストを使用していることを確認します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|リモートデータアーカイブスキーマを更新するローカル Stretch 対応テーブルの ID。|  
|**database_id**|**int**|ローカル Stretch が有効なテーブルを含むデータベースの ID。|  
|**task_id**|**bigint**|リモートデータアーカイブスキーマ更新タスクの ID です。|  
|**task_type**|**int**|リモートデータアーカイブスキーマ更新タスクの種類。|  
|**task_type_desc**|**nvarchar**|リモートデータアーカイブスキーマ更新タスクの種類の説明です。|  
|**task_state**|**int**|リモートデータアーカイブスキーマ更新タスクの状態です。|  
|**task_state_des**|**nvarchar**|リモートデータアーカイブスキーマ更新タスクの状態の説明です。|  
|**start_time_utc**|**datetime**|リモートデータアーカイブのスキーマの更新が開始された UTC 時刻。|  
|**end_time_utc**|**datetime**|リモートデータアーカイブスキーマの更新が完了した UTC 時刻。|  
|**error_number**|**int**|リモートデータアーカイブのスキーマの更新が失敗した場合は、発生したエラーのエラー番号。それ以外の場合は null。|  
|**error_severity**|**int**|リモートデータアーカイブのスキーマの更新が失敗した場合、発生したエラーの重大度。それ以外の場合は null。|  
|**error_state**|**int**|リモートデータアーカイブのスキーマの更新が失敗した場合、発生したエラーの状態。それ以外の場合は null。 Error_state は、エラーが発生した条件または場所を示します。|  
  
## <a name="see-also"></a>参照  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
