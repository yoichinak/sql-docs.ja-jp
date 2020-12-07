---
description: sysmergesubscriptions (Transact-sql)
title: sysmergesubscriptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aef0f508cc4d3c3034fe49c7e46762f3b9bb2645
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537873"
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  既知のサブスクライバーごとに1行のレコードを含み、パブリッシャー側のローカルテーブルです。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|サーバーの ID です。 サブスクリプションデータベースのコピーを別のサーバーに移行するときに、srvid フィールドをサーバー固有の値にマップするために使用します。|  
|db_name|**sysname**|サブスクライブしているデータベースの名前。|  
|pubid|**uniqueidentifier**|現在のサブスクリプションが作成されたパブリケーションの ID です。|  
|datasource_type|**int**|データソースの種類。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br /> **2** = Jet OLE DB。|  
|subid|**uniqueidentifier**|サブスクリプションの一意な ID 番号です。|  
|replnickname|**[バイナリ]**|レプリカの圧縮されたニックネーム。|  
|replicastate|**uniqueidentifier**|パブリッシャーの値とサブスクライバーの値を比較することによって、以前の同期が成功したかどうかを判断するために使用される一意の識別子。|  
|status|**tinyint**|サブスクリプションの状態。<br /><br /> **0** = 非アクティブ。<br /><br /> **1** = アクティブ。<br /><br /> **2** = 削除されました。|  
|subscriber_type|**int**|サブスクライバーの種類。<br /><br /> **1** = グローバル。<br /><br /> **2** = ローカル。<br /><br /> **3** = 匿名。|  
|subscription_type|**int**|サブスクリプションの種類。<br /><br /> **0** = プッシュ。<br /><br /> **1** = プル。<br /><br /> **2** = 匿名。|  
|sync_type|**tinyint**|同期の種類。<br /><br /> **1** = 自動。<br /><br /> **2** = 同期なし。|  
|description|**nvarchar (255)**|サブスクリプションの簡単な説明。|  
|priority|**real**|サブスクリプションの優先度を指定し、優先度に基づく競合解決を実装できるようにします。 すべてのローカルまたは匿名のサブスクリプションの場合は **0.00** と同じです。|  
|recgen|**bigint**|最後に受信した生成の数。|  
|recguid|**uniqueidentifier**|前回受信した generation 値の一意な ID です。|  
|sentgen|**bigint**|最後に送信された生成の数。|  
|文の guid|**uniqueidentifier**|最後に送信された生成の一意の ID。|  
|schemaversion|**int**|最後に受信したスキーマの数。|  
|schemaguid|**uniqueidentifier**|前回受信したスキーマの一意な ID です。|  
|last_validated|**datetime**|サブスクライバーデータが最後に正常に検証された **日時** 。|  
|attempted_validate|**datetime**|サブスクリプションで検証が試行された最後の **日時** 。|  
|last_sync_date|**datetime**|同期の **日時** 。|  
|last_sync_status|**int**|サブスクリプションの状態です。<br /><br /> **0** = すべてのジョブが開始を待機しています。<br /><br /> **1** = 1 つ以上のジョブが開始されています。<br /><br /> **2** = すべてのジョブが正常に実行されました。<br /><br /> **3** = 少なくとも1つのジョブが実行中です。<br /><br /> **4** = すべてのジョブがスケジュールされ、アイドル状態になります。<br /><br /> **5** = 少なくとも1つのジョブが前回のエラーの発生後に実行しようとしています。<br /><br /> **6** = 少なくとも1つのジョブを正常に実行できませんでした。|  
|last_sync_summary|**sysname**|前回の同期の結果の説明。|  
|metadatacleanuptime|**datetime**|有効期限が切れたメタデータがマージレプリケーションシステムテーブルから削除された最後の **日時** 。|  
|partition_id|**int**|サブスクリプションが属する事前計算済みのパーティションを識別します。|  
|cleanedup_unsent_changes|**bit**|未送信の変更のメタデータがサブスクライバーでクリーンアップされたことを示します。|  
|replica_version|**int**|サブスクリプションが所属するサブスクライバー用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンを識別します。次のいずれかの値になります。<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|内部使用のみです。|  
|application_name|**nvarchar(128)**|内部使用のみです。|  
|subscriber_number|**int**|内部使用のみです。|  
|last_makegeneration_datetime|**datetime**|Makegeneration プロセスがパブリッシャーに対して実行した最後の **日時** 。 詳細については、「 [レプリケーションマージエージェント](../../relational-databases/replication/agents/replication-merge-agent.md)」の-MakeGenerationInterval パラメーターを参照してください。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
