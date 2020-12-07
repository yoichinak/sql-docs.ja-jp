---
title: sp_rda_get_rpo_duration (Transact-sql) |Microsoft Docs
description: Sp_rda_get_rpo_duration を使用して、リモートの Azure データベースを完全に復元するためにステージングテーブルに保持 SQL Server れる、移行されたデータの時間数を取得します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b3b52298861da031dc5eab6b3a32135eec9d26cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538466"
---
# <a name="syssp_rda_get_rpo_duration-transact-sql"></a>sp_rda_get_rpo_duration (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  特定の時点への復元が必要な場合に、リモートの Azure データベースの完全な復元を確実に行うために、ステージングテーブルに保持 SQL Server れる、移行されたデータの時間数を取得します。 
  
  詳細については、「Stretch Database」を参照してください。移行され [た行を一時的に保持することで、Azure データのデータ損失のリスクが軽減](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)されます。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>構文    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>出力パラメーター    
 *\@durationinhours*    
  現在の Stretch が有効なデータベースについて SQL Server 保持する、移行されたデータの時間数 (null 以外の整数値) を指定します。    
    
## <a name="permissions"></a>アクセス許可    
 Db_owner のアクセス許可が必要です。    
    
## <a name="remarks"></a>解説    
 [Transact-sql&#41;&#40;sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)を実行して値を変更します。    
    
## <a name="see-also"></a>参照    
 [sp_rda_set_rpo_duration &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Stretch 対応データベースの復元 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
