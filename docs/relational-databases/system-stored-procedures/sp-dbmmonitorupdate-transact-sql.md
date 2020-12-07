---
description: sp_dbmmonitorupdate (Transact-sql)
title: sp_dbmmonitorupdate (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorupdate
- sp_dbmmonitorupdate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorupdate
- database mirroring [SQL Server], monitoring
ms.assetid: 9ceb9611-4929-44ee-a406-c39ba2720fd5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e8d150c2b45cd3556b47bef9cb2b2f882156f355
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536566"
---
# <a name="sp_dbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース ミラーリング監視の状態テーブルにミラー化されたデータベースごとの新しい行を挿入し、現在の保有期間より古い行を切り捨てます。 既定の保有期間は7日 (168 時間) です。 テーブルを更新すると、 **sp_dbmmonitorupdate** によってパフォーマンスメトリックが評価されます。  
  
> [!NOTE]  
>  **sp_dbmmonitorupdate** 初回実行時には、 msdb データベース内に **データベース ミラーリングの状態** テーブルと固定データベース ロール **dbm_monitor** が作成されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 ミラーリングの状態を更新するデータベースの名前を指定します。 *Database_name*が指定されていない場合、プロシージャは、サーバーインスタンス上のミラー化されたすべてのデータベースの状態テーブルを更新します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_dbmmonitorupdate** は、 **msdb** データベースのコンテキストでのみ実行できます。  
  
 状態テーブルの列がパートナーのロールに該当しない場合、そのパートナーについて、値は NULL になります。 フェールオーバーまたはサーバーの再起動中など、関連する情報が使用できない場合は、列の値も NULL になります。  
  
 **Sp_dbmmonitorupdate**によって**msdb**データベースに**dbm_monitor**固定データベースロールが作成された後、 **sysadmin**固定サーバーロールのメンバーは、 **dbm_monitor**固定データベースロールに任意のユーザーを追加できます。 **Dbm_monitor**ロールを使用すると、そのメンバーはデータベースミラーリングの状態を表示できますが、更新はできませんが、データベースミラーリングイベントを表示または構成することはできません。  
  
 データベースのミラーリング状態を更新すると、 **sp_dbmmonitorupdate** は、警告しきい値が指定されているミラーリングパフォーマンスメトリックの最新の値を検査します。 値がしきい値を超えている場合は情報イベントをイベント ログに追加します。 すべてのレートは、前回の更新以降の平均値です。 詳細については、「 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに対してのみ、ミラーリングの状態を更新します。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorhelpalert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
