---
description: sp_replmonitorhelpmergesession (Transact-sql)
title: sp_replmonitorhelpmergesession (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9544a1d11efbd3d956821784257619bb45b7a5cc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526200"
---
# <a name="sp_replmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたレプリケーションマージエージェントの過去のセッションに関する情報を返します。フィルターの条件に一致する各セッションに対して1行のデータが返されます。 このストアドプロシージャは、マージレプリケーションの監視に使用され、ディストリビューター側のディストリビューションデータベースまたはサブスクライバー側でサブスクリプションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @agent_name = ] 'agent_name'` エージェントの名前を指定します。 *agent_name* は **nvarchar (100)** で、既定値はありません。  
  
`[ @hours = ] hours` 履歴エージェントセッション情報を返す時間の範囲を時間単位で指定します。 *時間* は **int**で、次のいずれかの範囲を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|< **0**|過去のエージェント実行に関する情報を返します。最大で100の実行が実行されます。|  
|**0** (既定値)|過去のすべてのエージェント実行に関する情報を返します。|  
|> **0**|*過去数時間以内*に発生したエージェントの実行に関する情報を返します。|  
  
`[ @session_type = ] session_type` セッションの終了結果に基づいて結果セットをフィルター処理します。 *session_type* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1** (既定値)|再試行されたか成功したエージェント セッション。|  
|**0**|障害が発生したエージェントセッション。|  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値は NULL です。 このパラメーターは、サブスクライバーで **sp_replmonitorhelpmergesession** を実行するときに使用されます。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname**,、既定値は NULL です。 このパラメーターは、サブスクライバーで **sp_replmonitorhelpmergesession** を実行するときに使用されます。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は NULL です。 このパラメーターは、サブスクライバーで **sp_replmonitorhelpmergesession** を実行するときに使用されます。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|エージェント ジョブ セッションの ID。|  
|**状態**|**int**|エージェントの実行状態:<br /><br /> **1** = 開始<br /><br /> **2** = 成功<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル<br /><br /> **5** = 再試行<br /><br /> **6** = 失敗|  
|**StartTime**|**datetime**|エージェントジョブセッションが開始した時刻。|  
|**EndTime**|**datetime**|エージェントジョブセッションが完了しました。|  
|**期間**|**int**|このジョブセッションの累積時間 (秒単位)。|  
|**UploadedCommands**|**int**|エージェントセッション中にアップロードされたコマンドの数。|  
|**ダウンロードコマンド**|**int**|エージェントセッション中にダウンロードされたコマンドの数。|  
|**ErrorMessages**|**int**|エージェント セッション中に生成されたエラー メッセージ数。|  
|**ErrorID**|**int**|発生したエラーの ID です。|  
|**PercentageDone**|**decimal**|アクティブなセッションで既に配信されている変更の合計の推定割合。|  
|**TimeRemaining**|**int**|アクティブなセッションの残りの秒数。|  
|**CurrentPhase**|**int**|アクティブなセッションの現在のフェーズ。次のいずれかになります。<br /><br /> **1** = アップロード<br /><br /> **2** = ダウンロード|  
|**LastMessage**|**nvarchar (500)**|セッション中にマージ エージェントによってログに記録された最後のメッセージです。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_replmonitorhelpmergesession** は、マージレプリケーションの監視に使用されます。  
  
 サブスクライバーで実行された場合、 **sp_replmonitorhelpmergesession** は、最後の5つのマージエージェントセッションに関する情報のみを返します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorhelpmergesession**を実行できるのは、ディストリビューター側のディストリビューションデータベースまたはサブスクライバー側のサブスクリプションデータベースで、 **db_owner**または**replmonitor**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
