---
description: syssubscriptions (Transact-sql)
title: syssubscriptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
author: cawrites
ms.author: chadam
ms.openlocfilehash: 724627c394fa495eaed2a5d42ea8b16de4f491fd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197594"
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース内のサブスクリプションごとに1行のデータを格納します。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクルの一意な ID。|  
|**srvid**|**smallint**|サブスクライバーのサーバー ID。|  
|**dest_db**|**sysname**|転送先データベースの名前。|  
|**status**|**tinyint**|サブスクリプションの状態。<br /><br /> **0** = 非アクティブ。<br /><br /> **1** = サブスクライブ済み。<br /><br /> **2** = アクティブ。|  
|**sync_type**|**tinyint**|初期同期の種類。<br /><br /> **1** = 自動。<br /><br /> **2** = なし|  
|**login_name**|**sysname**|サブスクリプションを追加するときに使用されるログイン名です。|  
|**subscription_type**|**int**|サブスクリプションの種類。<br /><br /> 0 = プッシュ。ディストリビューション エージェントはディストリビューター側で実行されます。<br /><br /> 1 = プル。ディストリビューション エージェントはサブスクライバー側で実行されます。|  
|**distribution_jobid**|**binary(16)**|ディストリビューションエージェントのジョブ ID。|  
|**timestamp**|**timestamp**|タイムスタンプです。|  
|**update_mode**|**tinyint**|更新モード:<br /><br /> **0** = 読み取り専用。<br /><br /> **1** = 即時更新。|  
|**loopback_detection**|**bit**|双方向トランザクションレプリケーショントポロジの一部であるサブスクリプションに適用されます。 ディストリビューション エージェントが、サブスクライバーで発生したトランザクションをサブスクライバーに戻すかどうかを示します。<br /><br /> **0** = 返送します。<br /><br /> **1** = を返しません。|  
|**queued_reinit**|**bit**|アーティクルに初期化または再初期化のマークを付けるかどうかを指定します。 値 **1** は、サブスクライブされたアーティクルが初期化または再初期化のマークが付けられることを示します。|  
|**nosync_type**|**tinyint**|サブスクリプションの初期化の種類。<br /><br /> **0** = 自動 (スナップショット)<br /><br /> **1** = レプリケーションのサポートのみ<br /><br /> **2** = バックアップを使用した初期化<br /><br /> **3** = ログシーケンス番号 (LSN) からの初期化<br /><br /> 詳細については、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の **\@ sync_type** パラメーターを参照してください。|  
|**srvname**|**sysname**|サブスクライバーの名前です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
