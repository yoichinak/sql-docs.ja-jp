---
description: sys.conversation_endpoints (Transact-SQL)
title: conversation_endpoints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_endpoints_TSQL
- conversation_endpoints
- sys.conversation_endpoints
- sys.conversation_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_endpoints catalog view
ms.assetid: 2ed758bc-2a9d-4831-8da2-4b80e218f3ea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ef8bc8087811e25c8fde893a251e77d25661b5ea
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537485"
---
# <a name="sysconversation_endpoints-transact-sql"></a>sys.conversation_endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  メッセージ交換の各側 [!INCLUDE[ssSB](../../includes/sssb-md.md)] は、メッセージ交換のエンドポイントによって表されます。 このカタログビューには、データベース内のメッセージ交換エンドポイントごとに1行のデータが含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|conversation_handle|**uniqueidentifier**|このメッセージ交換エンドポイントの識別子。 NULL 値は許容されません。|  
|conversation_id|**uniqueidentifier**|メッセージ交換の識別子。 この識別子はメッセージ交換の両側で共有されます。 この識別子と is_initiator 列はデータベース内で一意です。 NULL 値は許容されません。|  
|is_initiator|**tinyint**|このエンドポイントが、メッセージ交換の発信側と発信先のどちらであるかを示します。  NULL 値は許容されません。<br /><br /> 1 = 発信側<br /><br /> 0 = ターゲット|  
|service_contract_id|**int**|このメッセージ交換のコントラクトの識別子。 NULL 値は許容されません。|  
|conversation_group_id|**uniqueidentifier**|このメッセージ交換が属しているメッセージ交換グループの識別子。 NULL 値は許容されません。|  
|service_id|**int**|メッセージ交換の一方 (このビューを現在使用している側) で使用するサービスの識別子。 NULL 値は許容されません。|  
|有効期間|**datetime**|メッセージ交換の有効期限 (日付と時刻)。 NULL 値は許容されません。|  
|状態|**char(2)**|メッセージ交換の現在の状態。 NULL 値は許容されません。 つぎのいずれかです。<br /><br /> 送信が開始されました。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このメッセージ交換の開始メッセージ交換を処理しましたが、メッセージはまだ送信されていません。<br /><br /> SI   受信開始。 別のインスタンスがとの新しいメッセージ交換を開始し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ましたが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最初のメッセージをまだ完全に受信していません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最初のメッセージが断片化されている場合、またはメッセージを順不同で受信した場合に、この状態のメッセージ交換を作成することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ただし、メッセージ交換で受信された最初の転送データに最初のメッセージ全体が含まれている場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で CO (メッセージ交換確立) 状態のメッセージ交換が作成されることがあります。<br /><br /> CO   メッセージ交換確立。 メッセージ交換が確立され、メッセージ交換の両側でメッセージを送信できます。 通常のサービスでのメッセージ交換の大半は、メッセージ交換がこの状態のときに行われます。<br /><br /> DI 受信が切断されました。 メッセージ交換のリモート側で END CONVERSATION が発行されました。 メッセージ交換のローカル側で END CONVERSATION が発行されるまで、メッセージ交換はこの状態になります。 アプリケーションがメッセージ交換のメッセージを受信する場合もあります。 メッセージ交換のリモート側ではメッセージ交換が終了しているので、このメッセージ交換でアプリケーションからメッセージを送信することはできません。 アプリケーションがメッセージ交換を終了すると、メッセージ交換は CD (Closed) 状態に移動します。<br /><br /> 送信を切断します。 メッセージ交換のローカル側で END CONVERSATION が発行されました。 メッセージ交換のリモート側で END CONVERSATION が承認されるまで、メッセージ交換はこの状態になります。 アプリケーションはこのメッセージ交換でメッセージを送受信することはできません。 メッセージ交換のリモート側がメッセージ交換の終了を確認すると、メッセージ交換は CD (Closed) 状態に移動します。<br /><br /> ER エラーです。 このエンドポイントでエラーが発生しました。 エラーメッセージはアプリケーションキューに格納されます。 アプリケーションキューが空の場合は、アプリケーションが既にエラーメッセージを使用していることを示します。<br /><br /> CD を閉じました。 メッセージ交換のエンドポイントは解放されました。|  
|state_desc|**nvarchar(60)**|エンドポイントのメッセージ交換の状態の説明。 この列は NULL 値を許容します。 つぎのいずれかです。<br /><br /> **STARTED_OUTBOUND**<br /><br /> **STARTED_INBOUND**<br /><br /> **会話**<br /><br /> **DISCONNECTED_INBOUND**<br /><br /> **DISCONNECTED_OUTBOUND**<br /><br /> **開閉**<br /><br /> **ERROR**|  
|far_service|**nvarchar (256)**|メッセージ交換のリモート側で使用されるサービスの名前。 NULL 値は許容されません。|  
|far_broker_instance|**nvarchar(128)**|メッセージ交換のリモート側のブローカーインスタンス。 NULLABLE.|  
|principal_id|**int**|ダイアログのローカル側で使用される証明書を持つプリンシパルの識別子。 NULL 値は許容されません。|  
|far_principal_id|**int**|ダイアログのリモート側で使用される証明書を持つユーザーの識別子。 NULL 値は許容されません。|  
|outbound_session_key_identifier|**uniqueidentifier**|このダイアログの送信暗号化キーの識別子。 NULL 値は許容されません。|  
|inbound_session_key_identifier|**uniqueidentifier**|ダイアログで使用される受信暗号化キーの識別子。 NULL 値は許容されません。|  
|security_timestamp|**datetime**|ローカルのセッション キーが作成された時刻。 NULL 値は許容されません。|  
|dialog_timer|**datetime**|このダイアログのメッセージ交換タイマーによって、表示タイマーメッセージが送信される時刻。 NULL 値は許容されません。|  
|send_sequence|**bigint**|送信シーケンスの次のメッセージ番号。 NULL 値は許容されません。|  
|last_send_tran_id|**binary(6)**|メッセージを送信する最後のトランザクションの内部トランザクション ID。 NULL 値は許容されません。|  
|end_dialog_sequence|**bigint**|終了ダイアログ メッセージのシーケンス番号。 NULL 値は許容されません。|  
|receive_sequence|**bigint**|メッセージ受信シーケンスで予測される次のメッセージ番号。 NULL 値は許容されません。|  
|receive_sequence_frag|**int**|メッセージ受信シーケンスで予測される次のメッセージ フラグメント番号。 NULL 値は許容されません。|  
|system_sequence|**bigint**|ダイアログの最後のシステム メッセージのシーケンス番号。 NULL 値は許容されません。|  
|first_out_of_order_sequence|**bigint**|このダイアログの順不同メッセージ内の最初のメッセージのシーケンス番号。 NULL 値は許容されません。|  
|last_out_of_order_sequence|**bigint**|ダイアログの、順序どおりでないメッセージのうち最後のメッセージのシーケンス番号。 NULL 値は許容されません。|  
|last_out_of_order_frag|**int**|このダイアログの順序が不足しているフラグメント内の最後のメッセージのシーケンス番号。 NULL 値は許容されません。|  
|is_system|**bit**|システムダイアログの場合は1。 NULL 値は許容されません。|  
|priority|**tinyint**|このメッセージ交換のエンドポイントに割り当てられているメッセージ交換の優先度。 NULL 値は許容されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
