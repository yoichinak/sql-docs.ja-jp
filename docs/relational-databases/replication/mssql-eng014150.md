---
description: MSSQL_ENG014150
title: MSSQL_ENG014150 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c2587ba9bd9858931be4113d1f4b91df90fd9854
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423576"
---
# <a name="mssql_eng014150"></a>MSSQL_ENG014150
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|属性|値|  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14150|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|レプリケーション-%s: エージェント %s が成功しました。 %s|  
  
## <a name="explanation"></a>説明  
 このメッセージは、レプリケーション エージェントの実行が正常に完了したことを示しています。 レプリケーションでは、次のエージェントを使用します。  
  
-   スナップショット エージェント。 すべてのパブリケーションで使用されます。  
  
-   ログ リーダー エージェント。 すべてのトランザクション パブリケーションで使用されます。  
  
-   キュー リーダー エージェント。 キュー更新サブスクリプションに有効なトランザクション パブリケーションで使用されます。  
  
-   ディストリビューション エージェント。 サブスクリプションをトランザクション パブリケーションおよびスナップショット パブリケーションと同期します。  
  
-   マージ エージェント。 サブスクリプションをマージ パブリケーションと同期します。  
  
-   レプリケーション メンテナンス ジョブ。  
  
## <a name="user-action"></a>ユーザーの操作  
 通常、ログ リーダー エージェント、キュー リーダー エージェント、およびディストリビューション エージェントは連続実行しますが、他のエージェントは、要求時に実行するかスケジュールに合わせて実行します。 エージェントが実行を完了したかどうかわからない場合は、エージェントの状態を確認します。 詳細については、「 [Monitor Replication Agents](../../relational-databases/replication/monitor/monitor-replication-agents.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [レプリケーション キュー リーダー エージェント](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
