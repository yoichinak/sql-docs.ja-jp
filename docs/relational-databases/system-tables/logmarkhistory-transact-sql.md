---
description: logmarkhistory (Transact-SQL)
title: logmarkhistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e5b7a952735485c85c4763937a6448c164e3823b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538292"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  予約されているマークされたトランザクションごとに1行のレコードを格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|マークされたトランザクションが発生したローカルデータベース。|  
|**mark_name**|**nvarchar(128)**|マークされたトランザクションのユーザー指定の名前。|  
|**description**|**nvarchar (255)**|マーク付きのトランザクションに指定されたユーザー定義の説明。 NULL にすることができます。|  
|**user_name**|**nvarchar(128)**|マーク付きのトランザクションを実行したデータベース ユーザー名。 NULL にすることができます。|  
|**lsn**|**numeric(25,0)**|マークが発生したトランザクションレコードのログシーケンス番号。|  
|**mark_time**|**datetime**|マークされたトランザクションのコミット時間 (ローカル時刻)。|  
  
## <a name="see-also"></a>参照  
 [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
