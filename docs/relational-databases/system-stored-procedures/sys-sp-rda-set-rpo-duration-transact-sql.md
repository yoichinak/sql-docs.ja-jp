---
title: sys.sp_rda_set_rpo_duration (Transact-sql) |Microsoft Docs
description: Sys.sp_rda_set_rpo_duration について説明します。 このストアドプロシージャを使用して、ステージングテーブルに保持 SQL Server 移行されるデータの時間数を設定します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cc7bbf5ddcde440bb359616201602a9c463d87e6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99186628"
---
# <a name="syssp_rda_set_rpo_duration-transact-sql"></a>sys.sp_rda_set_rpo_duration (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  特定の時点への復元が必要な場合に、リモートの Azure データベースの完全な復元を確実に行うために、ステージングテーブルに保持 SQL Server れる移行データの時間数を設定します。    
    
 詳細については、「Stretch Database」を参照してください。移行され [た行を一時的に保持することで、Azure データのデータ損失のリスクが軽減](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)されます。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>構文    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>引数    
 [ @duration_hrs =] *duration_hrs*    
 現在の Stretch が有効なデータベースについて SQL Server 保持する移行データの時間数 (null 以外の整数値) を指定します。 既定値と最小値は8時間です。    
 
 > [!NOTE]
 > 値が大きいほど、SQL Server により多くの記憶領域が必要になります。
    
## <a name="permissions"></a>アクセス許可    
 db_owner のアクセス許可が必要です。    
    
## <a name="remarks"></a>コメント    
 [Transact-sql&#41;&#40;sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)を実行して、現在の値を取得します。    
    
## <a name="see-also"></a>参照    
 [sys.sp_rda_get_rpo_duration &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [Stretch 対応データベースの復元 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
