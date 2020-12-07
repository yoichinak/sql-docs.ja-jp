---
description: restorehistory (Transact-SQL)
title: restorehistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 03b5887ee905d5a39bce5ef9e73e78e27b581972
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540842"
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  復元操作ごとに 1 行のデータを格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|各復元操作を識別する一意の識別番号。 Id、主キー。|  
|**restore_date**|**datetime**|復元操作が開始された日付と時刻。 NULL にすることができます。|  
|**destination_database_name**|**nvarchar(128)**|復元操作の対象となるデータベースの名前。 NULL にすることができます。|  
|**user_name**|**nvarchar(128)**|復元操作を実行したユーザーの名前。 NULL にすることができます。|  
|**backup_set_id**|**int**|復元されるバックアップ セットを識別する一意な識別番号。 **Backupset (backup_set_id)** を参照します。|  
|**restore_type**|**char(1)**|復元操作の種類。<br /><br /> D = データベース<br /><br /> F = ファイル<br /><br /> G = ファイル グループ<br /><br /> I = 差分<br /><br /> L = ログ<br /><br /> V = Verifyonly<br /><br /> NULL にすることができます。|  
|**replace**|**bit**|復元操作に REPLACE オプションが指定されているかどうかを示します。<br /><br /> 1 = 指定<br /><br /> 0 = 指定なし<br /><br /> NULL にすることができます。<br /><br /> データベースをデータベーススナップショットに戻す場合、唯一のオプションは0です。|  
|**復旧 (recovery)**|**bit**|復元操作に RECOVERY または NORECOVERY オプションが指定されたかどうか。<br /><br /> 1 = 回復<br /><br /> NULL にすることができます。<br /><br /> データベースをデータベーススナップショットに戻す場合、唯一のオプションは1です。<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|復元操作に RESTART オプションが指定されているかどうかを示します。<br /><br /> 1 = 指定<br /><br /> 0 = 指定なし<br /><br /> NULL にすることができます。<br /><br /> データベースをデータベーススナップショットに戻す場合、唯一のオプションは0です。|  
|**stop_at**|**datetime**|データベースが復旧された時点。 NULL にすることができます。|  
|**device_count**|**tinyint**|復元操作に関係したデバイスの数。 この数は、バックアップのメディアファミリの数よりも少なくなる場合があります。 NULL にすることができます。<br /><br /> データベースをデータベーススナップショットに戻すと、その数は常に1になります。|  
|**stop_at_mark_name**|**nvarchar(128)**|名前付きマークを含むトランザクションへの復旧。 NULL にすることができます。<br /><br /> データベースをデータベース スナップショットに戻す場合、この値は NULL になります。|  
|**stop_before**|**bit**|名前付きマークを含むトランザクションが復旧に含まれていたかどうかを示します。<br /><br /> 0 = マークされたトランザクションの前に復旧が停止しました。<br /><br /> 1 = マーク付きのトランザクションも復旧された。<br /><br /> NULL にすることができます。<br /><br /> データベースをデータベース スナップショットに戻す場合、この値は NULL になります。|  
  
## <a name="remarks"></a>解説  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
