---
title: 中断された復元の再開 (Transact-SQL)
description: この例では、Transact-SQL を使用して SQL Server で中断された復元操作を再開する方法について示します。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
author: cawrites
ms.author: chadam
ms.openlocfilehash: f2c70762e4e68081fc63930b1140ba904a5ca565
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129144"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>中断された復元操作の再開 (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、中断された復元操作を再開する方法について説明します。  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>中断された復元操作を再開するには  
  
1.  次の項目を指定して、中断された RESTORE ステートメントを再実行します。  
  
    -   元の RESTORE ステートメントで使用したものと同じ句  
  
    -   RESTART 句  
  
## <a name="example"></a>例  
 この例では、中断された復元操作を再開します。  
  
```sql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベースの全体復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
