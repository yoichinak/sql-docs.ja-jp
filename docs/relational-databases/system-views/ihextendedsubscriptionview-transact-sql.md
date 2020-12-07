---
description: IHextendedSubscriptionView (Transact-SQL)
title: IHextendedSubscriptionView (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
author: stevestein
ms.author: sstein
ms.openlocfilehash: aca2ddea9625b5b2a40fea6ef27d6f218a71cda0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485437"
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHextendedSubscriptionView**ビューでは、非 SQL Server パブリケーションのサブスクリプションに関する情報が公開されます。 このビューは、 **ディストリビューション** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|アーティクルの一意識別子。|  
|**dest_db**|**sysname**|転送先データベースの名前。|  
|**srvid**|**smallint**|サブスクライバーの一意の識別子です。|  
|**login_name**|**sysname**|サブスクライバーへの接続に使用されるログインです。|  
|**distribution_jobid**|**[バイナリ]**|ディストリビューションエージェントジョブを識別します。|  
|**publisher_database_id**|**int**|パブリケーションデータベースを識別します。|  
|**subscription_type**|**int**|サブスクリプションの種類。<br /><br /> **0** = プッシュ-ディストリビューションエージェントはサブスクライバーで実行されます。<br /><br /> **1** = プル-ディストリビューションエージェントはディストリビューターで実行されます。|  
|**sync_type**|**tinyint**|初期同期の種類。<br /><br /> **1** = 自動<br /><br /> **2** = なし|  
|**status**|**tinyint**|サブスクリプションの状態。<br /><br /> **0** = 非アクティブ<br /><br /> **1** = サブスクライブ済み<br /><br /> **2** = アクティブ|  
|**snapshot_seqno_flag**|**bit**|スナップショットシーケンス番号が使用されているかどうかを示します。|  
|**independent_agent**|**bit**|このパブリケーションに対して、スタンドアロンのディストリビューション エージェントがあるかどうかを示します。<br /><br /> **0** = パブリケーションは共有ディストリビューションエージェントを使用し、各パブリッシャーデータベース/サブスクライバーデータベースのペアには1つの共有エージェントがあります。<br /><br /> **1** = このパブリケーションには、スタンドアロンのディストリビューションエージェントがあります。|  
|**subscription_time**|**datetime**|内部使用のみです。|  
|**loopback_detection**|**bit**|双方向トランザクションレプリケーショントポロジの一部であるサブスクリプションに適用されます。 ディストリビューション エージェントが、サブスクライバーで発生したトランザクションをサブスクライバーに戻すかどうかを示します。<br /><br /> **1** = を返しません。<br /><br /> **0** = 返送します。|  
|**agent_id**|**int**|ディストリビューションエージェントの一意の識別子。|  
|**update_mode**|**tinyint**|更新モードの種類を示します。以下のいずれかを指定できます。<br /><br /> **0** = 読み取り専用。<br /><br /> **1** = 即時更新。<br /><br /> **2** = メッセージキューを使用した更新がキューに登録されました。<br /><br /> **3** = メッセージキューを使用して、フェールオーバーとしてキュー更新を使用する即時更新。<br /><br /> **4** = SQL Server キューを使用したキュー更新。<br /><br /> **5** = キュー更新フェールオーバーを使用した即時更新。 SQL Server キューを使用します。|  
|**publisher_seqno**|**varbinary(16)**|このサブスクリプションに対するパブリッシャー側のトランザクションのシーケンス番号。|  
|**ss_cplt_seqno**|**varbinary(16)**|同時実行スナップショット処理の完了を示すために使用するシーケンス番号。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
