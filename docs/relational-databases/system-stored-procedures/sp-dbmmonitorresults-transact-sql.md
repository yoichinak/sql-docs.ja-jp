---
description: sp_dbmmonitorresults (Transact-SQL)
title: sp_dbmmonitorresults (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f623f377bf850f5c247c770f7cc38358cf4dabb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543566"
---
# <a name="sp_dbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース ミラーリング監視履歴が格納されている状態テーブルから、監視対象データベースの状態行を返します。事前に、このプロシージャで最新の状態を取得するかどうかを選択できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 ミラーリングの状態を返すデータベースを指定します。  
  
 *rows_to_return*  
 返す行の量を指定します。  
  
 0 = 最後の行  
  
 1 = 過去 2 時間の行  
  
 2 = 過去4時間の行  
  
 3 = 過去 8 時間の行  
  
 4 = 過去1日間の行  
  
 5 = 過去 2 日間の行  
  
 6 = 最後の100行  
  
 7 = 最後の500行  
  
 8 = 最後の1000行  
  
 9 = 最新 1,000,000 行  
  
 *update_status*  
 結果を返す前にプロシージャを指定することを指定します。  
  
 0 = データベースの状態を更新しません。 結果は最新 2 行のみから計算されます。行の古さは状態テーブルが更新された日時を基に判断されます。  
  
 1 = 結果を計算する前に **sp_dbmmonitorupdate** を呼び出すことによって、データベースの状態を更新します。 ただし、状態テーブルが過去15秒以内に更新された場合、またはユーザーが **sysadmin** 固定サーバーロールのメンバーでない場合、 **sp_dbmmonitorresults** は状態を更新せずに実行します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 指定されたデータベースについて、要求された履歴の状態の行数を返します。 各行には、次の情報が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|ミラー化されたデータベースの名前。|  
|**role**|**int**|サーバーインスタンスの現在のミラーリングロール:<br /><br /> 1 = プリンシパル<br /><br /> 2 = ミラー|  
|**mirroring_state**|**int**|データベースの状態。<br /><br /> 0 = 中断<br /><br /> 1 = 切断<br /><br /> 2 = 同期中<br /><br /> 3 = フェールオーバー保留中<br /><br /> 4 = 同期済み|  
|**witness_status**|**int**|データベースのデータベースミラーリングセッションにおけるミラーリング監視サーバーの接続状態は次のようになります。<br /><br /> 0 = 不明<br /><br /> 1 = 接続済み<br /><br /> 2 = 切断|  
|**log_generation_rate**|**int**|このデータベースのミラーリング状態の前回の更新以降に生成されたログの量 (kb/秒単位)。|  
|**unsent_log**|**int**|プリンシパルの送信キューにある未送信のログのサイズ (kb 単位)。|  
|**send_rate**|**int**|プリンシパルからミラーへのログの送信速度 (kb/秒単位)。|  
|**unrestored_log**|**int**|ミラー上の再実行キューのサイズ (kb 単位)。|  
|**recovery_rate**|**int**|ミラーの再実行率 (KB/秒単位)。|  
|**transaction_delay**|**int**|すべてのトランザクションの合計遅延時間 (ミリ秒単位)。|  
|**transactions_per_sec**|**int**|プリンシパルサーバーインスタンスで1秒間に発生しているトランザクションの数。|  
|**average_delay**|**int**|データベースミラーリングが原因で、各トランザクションのプリンシパルサーバーインスタンスの平均遅延時間。 高パフォーマンスモード (安全性プロパティが OFF に設定されている場合) では、通常、この値は0です。|  
|**time_recorded**|**datetime**|データベース ミラーリング監視で行が記録された時間。 これは、プリンシパルのシステムクロック時間です。|  
|**time_behind**|**datetime**|ミラーデータベースが現在キャッチされているプリンシパルのおおよそのシステムクロック時間。 この値はプリンシパル サーバー インスタンスでのみ意味を持ちます。|  
|**local_time**|**datetime**|この行が更新されたときのローカル サーバー インスタンスのシステム クロック時間。|  
  
## <a name="remarks"></a>解説  
 **sp_dbmmonitorresults** は、 **msdb** データベースのコンテキストでのみ実行できます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップ、または**msdb**データベースの**dbm_monitor**固定データベースロールのメンバーシップが必要です。 **Dbm_monitor**ロールを使用すると、そのメンバーはデータベースミラーリングの状態を表示できますが、更新はできませんが、データベースミラーリングイベントを表示または構成することはできません。  
  
> [!NOTE]  
>  **Sp_dbmmonitorupdate**を初めて実行すると、 **dbm_monitor**の固定データベースロールが**msdb**データベースに作成されます。 **Sysadmin**固定サーバーロールのメンバーは、任意のユーザーを**dbm_monitor**固定データベースロールに追加できます。  
  
## <a name="examples"></a>例  
 次の例では、データベースの状態を更新せずに、前の2時間に記録された行を返します。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
