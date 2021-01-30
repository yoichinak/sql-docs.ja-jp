---
title: backupmediafamily (Transact-sql) |Microsoft Docs
description: Backupmediafamily のリファレンス。各メディアファミリの1行が含まれています。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
author: cawrites
ms.author: chadam
ms.openlocfilehash: df687040bf73fb1d78f15d7cca18cc0fc092ee1f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198682"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-sql)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

メディア ファミリごとに 1 行のデータを格納します。 メディア ファミリがミラー化されたメディア セット内にある場合は、メディア セット内のミラーごとに個別の行が格納されます。 このテーブルは、 **msdb** データベースに格納されます。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|このファミリがメンバーとなっているメディアセットを識別する一意の識別番号。 **Backupmediaset (media_set_id)** を参照します|  
|**family_sequence_number**|**tinyint**|メディアセット内のこのメディアファミリの位置。|  
|**media_family_id**|**uniqueidentifier**|メディアファミリを識別する一意の識別番号。 NULL にすることができます。|  
|**media_count**|**int**|メディアファミリ内のメディアの数。 NULL にすることができます。|  
|**logical_device_name**|**nvarchar(128)**|**Sys.backup_devices** にあるこのバックアップデバイスの名前。 これが ( **sys.backup_devices** に存在するパーマネントバックアップデバイスではなく) 一時的なバックアップデバイスの場合、 **logical_device_name** の値は NULL になります。|  
|**physical_device_name**|**nvarchar(260)**|バックアップデバイスの物理名。 NULL にすることができます。 このフィールドは、バックアップと復元のプロセス間で共有されます。 元のバックアップ先のパスまたは元の復元元のパスが含まれている場合があります。 データベースのサーバーでバックアップまたは復元が最初に実行されたかどうかによって異なります。 同じバックアップファイルからの連続した復元では、復元時の場所に関係なく、パスが更新されないことに注意してください。 このため、使用されている復元パスを確認するために **physical_device_name** フィールドを使用することはできません。|  
|**device_type**|**tinyint**|バックアップ デバイスの種類。<br /><br /> 2 = ディスク<br /><br /> 5 = テープ<br /><br /> 7 = 仮想デバイス<br /><br /> 9 = Azure Storage<br /><br /> 105 = パーマネントなバックアップ デバイス。<br /><br /> NULL にすることができます。<br /><br /> 永続的なデバイス名とデバイス番号はすべて **sys.backup_devices** にあります。|  
|**physical_block_size**|**int**|メディアファミリの書き込みに使用される物理ブロックサイズ。 NULL にすることができます。|  
|**mirror**|**tinyint**|ミラー数 (0 ～ 3)。|  
  
## <a name="remarks"></a>コメント  
 LOADHISTORY を使用した *backup_device* からの RESTORE verifyonly は、 **backupmediaset** テーブルの列に、メディアセットヘッダーからの適切な値を設定します。  
  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
