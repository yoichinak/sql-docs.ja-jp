---
description: sys.dm_broker_connections (Transact-SQL)
title: dm_broker_connections (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_connections
- dm_broker_connections
- sys.dm_broker_connections_TSQL
- dm_broker_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_connections dynamic management view
ms.assetid: d9e20433-67fe-4fcc-80e3-b94335b2daef
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8ce810ed6014710b6d4a9a3cb61da9fe4e0605cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537697"
---
# <a name="sysdm_broker_connections-transact-sql"></a>sys.dm_broker_connections (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ネットワーク接続ごとに1行の値を返し [!INCLUDE[ssSB](../../includes/sssb-md.md)] ます。 詳細については、次の表を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|接続の識別子。 NULLABLE.|  
|**transport_stream_id**|**uniqueidentifier**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Tcp/ip 通信用にこの接続で使用されるネットワークインターフェイス (SNI) 接続の識別子。 NULLABLE.|  
|**状態**|**smallint**|接続の現在の状態です。 NULLABLE. 指定できる値<br /><br /> 1 = 新規<br /><br /> 2 = 接続中<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = 終了|  
|**state_desc**|**nvarchar(60)**|接続の現在の状態です。 NULLABLE. 指定できる値<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|接続が開いた日付と時刻。 NULLABLE.|  
|**login_time**|**datetime**|接続に対するログインが成功した日付と時刻。 NULLABLE.|  
|**authentication_method**|**nvarchar(128)**|NTLM または KERBEROS など、Windows 認証方法の名前。 値は Windows から取得されます。 NULLABLE.|  
|**principal_name**|**nvarchar(128)**|接続権限が検証されたログインの名前。 Windows 認証の場合、この値はリモートユーザー名になります。 証明書認証の場合、この値は証明書の所有者になります。 NULLABLE.|  
|**remote_user_name**|**nvarchar(128)**|Windows 認証で使用されるもう1つのデータベースのピアユーザーの名前。 NULLABLE.|  
|**last_activity_time**|**datetime**|情報の送受信に接続が最後に使用された日付と時刻。 NULLABLE.|  
|**is_accept**|**bit**|接続がリモート側で発生したかどうかを示します。 NULLABLE.<br /><br /> 1 = 接続は、リモートインスタンスから受け入れられる要求です。<br /><br /> 0 = ローカル インスタンスで開始された接続。|  
|**login_state**|**smallint**|この接続のログインプロセスの状態。 指定できる値<br /><br /> 0 = 初期<br /><br /> 1 = 待機ログインのネゴシエート<br /><br /> 2 = ONE ISC<br /><br /> 3 = 1 ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = 2 ASC<br /><br /> 6 = ISC の確認を待機する<br /><br /> 7 = ASC ASC Confirm<br /><br /> 8 = 拒否の待機<br /><br /> 9 = 事前マスタシークレットを待機する<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = アービトレーションを待機する<br /><br /> 12 = オンライン<br /><br /> 13 = エラー|  
|**login_state_desc**|**nvarchar(60)**|リモートコンピューターからのログインの現在の状態。 指定できる値<br /><br /> 接続ハンドシェイクを初期化しています。<br /><br /> 接続ハンドシェイクは、Login Negotiate メッセージを待機しています。<br /><br /> 接続ハンドシェイクが初期化され、認証のためのセキュリティコンテキストが送信されました。<br /><br /> 接続ハンドシェイクを受信し、認証用のセキュリティ コンテキストを承諾しました。<br /><br /> 接続ハンドシェイクが初期化され、認証のためのセキュリティコンテキストが送信されました。 ピアを認証するために使用できるオプションのメカニズムがあります。<br /><br /> 接続ハンドシェイクを受信し、認証用のセキュリティ コンテキストを送信しました。 ピアを認証するために使用できるオプションのメカニズムがあります。<br /><br /> 接続ハンドシェイクは、セキュリティコンテキストの初期化の確認メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、受け入れセキュリティコンテキスト確認メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、失敗した認証に関する SSPI 拒否メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、マスタシークレットより前のメッセージを待機しています。<br /><br /> 接続ハンドシェイクは、Validation メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、判別メッセージを待機しています。<br /><br /> 接続ハンドシェイクが完了し、メッセージ交換のためにオンライン (準備完了) になっています。<br /><br /> 接続にエラーがあります。|  
|**peer_certificate_id**|**int**|認証でリモート インスタンスによって使用される証明書のローカル オブジェクト ID。 この証明書の所有者は、エンドポイントに対する CONNECT 権限を持っている必要があり [!INCLUDE[ssSB](../../includes/sssb-md.md)] ます。 NULLABLE.|  
|**encryption_algorithm**|**smallint**|接続で使用される暗号化アルゴリズム。 NULLABLE. 指定できる値<br /><br /> **値 &#124; 説明 &#124; 対応する DDL オプション**<br /><br /> 0 &#124; none &#124; 無効<br /><br /> 1 &#124; 署名のみ<br /><br /> 2 &#124; AES、RC4 &#124; 必要 &#124; 必要なアルゴリズム RC4}<br /><br /> 3 &#124; AES &#124;必要なアルゴリズム AES<br /><br /> **注:** RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|暗号化アルゴリズムのテキスト表示。 NULLABLE. 有効値は次のとおりです。<br /><br /> **説明 &#124; 対応する DDL オプション**<br /><br /> NONE &#124; Disabled<br /><br /> RC4 &#124; {必須 &#124; アルゴリズム RC4}<br /><br /> AES &#124; 必要なアルゴリズム AES<br /><br /> なし、RC4 &#124; {サポートされ &#124; アルゴリズム RC4}<br /><br /> NONE、AES &#124; サポートされているアルゴリズム RC4<br /><br /> RC4、AES &#124; 必要なアルゴリズム RC4 AES<br /><br /> AES、RC4 &#124; 必要なアルゴリズム AES RC4<br /><br /> NONE、RC4、AES &#124; サポートされているアルゴリズム RC4 AES<br /><br /> NONE、AES、RC4 &#124; サポートされているアルゴリズム AES RC4|  
|**receives_posted**|**smallint**|この接続でまだ完了していない非同期ネットワーク受信の数。 NULLABLE.|  
|**is_receive_flow_controlled**|**bit**|ネットワークがビジー状態のときに行われたフロー制御が原因で、ネットワーク受信が延期されたかどうか。 NULLABLE.<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|この接続でまだ完了していない非同期ネットワーク送信の数。 NULLABLE.|  
|**is_send_flow_controlled**|**bit**|ネットワークがビジー状態のためネットワークフロー制御のためにネットワーク送信が延期されているかどうか。 NULLABLE.<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|この接続で送信されたバイト数の合計です。 NULLABLE.|  
|**total_bytes_received**|**bigint**|この接続で受信された合計バイト数。 NULLABLE.|  
|**total_fragments_sent**|**bigint**|この接続で送信された [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ フラグメントの合計数。 NULLABLE.|  
|**total_fragments_received**|**bigint**|この接続で受信された [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ フラグメントの合計数。 NULLABLE.|  
|**total_sends**|**bigint**|この接続で発行されたネットワーク送信要求の合計数。 NULLABLE.|  
|**total_receives**|**bigint**|この接続によって発行されたネットワーク受信要求の合計数。 NULLABLE.|  
|**peer_arbitration_id**|**uniqueidentifier**|エンドポイントの内部識別子。 NULLABLE.|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="physical-joins"></a>物理結合  
 ![sys.dm_broker_connections の結合](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-connections-1.gif "sys.dm_broker_connections の結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|終了|リレーションシップ|  
|----------|--------|------------------|  
|**dm_broker_connections.connection_id**|**dm_exec_connections.connection_id**|一対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

