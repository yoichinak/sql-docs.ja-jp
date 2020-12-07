---
description: データベースミラーリング-sys. dm_db_mirroring_connections
title: dm_db_mirroring_connections (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_mirroring_connections
- dm_db_mirroring_connections
- sys.dm_db_mirroring_connections_TSQL
- dm_db_mirroring_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_mirroring_connections dynamic management view
ms.assetid: e4df91b6-0240-45d0-ae22-cb2c0d52e0b3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a9f7b7d1cb6f3c3f9af3dcb9f64b42fa48af78c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551331"
---
# <a name="database-mirroring---sysdm_db_mirroring_connections"></a>データベースミラーリング-sys. dm_db_mirroring_connections
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース ミラーリング用に確立された各接続の行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|接続の識別子。|  
|**transport_stream_id**|**uniqueidentifier**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Tcp/ip 通信用にこの接続で使用されるネットワークインターフェイス (SNI) 接続の識別子。|  
|**状態**|**smallint**|接続の現在の状態です。 指定できる値<br /><br /> 1 = 新規<br /><br /> 2 = 接続中<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = 終了|  
|**state_desc**|**nvarchar(60)**|接続の現在の状態です。 指定できる値<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|接続が開いた日付と時刻。|  
|**login_time**|**datetime**|接続に対するログインが成功した日付と時刻。|  
|**authentication_method**|**nvarchar(128)**|NTLM または KERBEROS など、Windows 認証方法の名前。 値は Windows から取得されます。|  
|**principal_name**|**nvarchar(128)**|接続権限が検証されたログインの名前。 Windows 認証の場合、この値はリモートユーザー名になります。 証明書認証の場合、この値は証明書の所有者になります。|  
|**remote_user_name**|**nvarchar(128)**|Windows 認証で使用されるもう1つのデータベースのピアユーザーの名前。|  
|**last_activity_time**|**datetime**|情報の送受信に接続が最後に使用された日付と時刻。|  
|**is_accept**|**bit**|接続がリモート側で発生したかどうかを示します。<br /><br /> 1 = 接続は、リモートインスタンスから受け入れられる要求です。<br /><br /> 0 = ローカル インスタンスで開始された接続。|  
|**login_state**|**smallint**|この接続のログインプロセスの状態。 指定できる値<br /><br /> 0 = 初期<br /><br /> 1 = 待機ログインのネゴシエート<br /><br /> 2 = ONE ISC<br /><br /> 3 = 1 ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = 2 ASC<br /><br /> 6 = ISC の確認を待機する<br /><br /> 7 = ASC ASC Confirm<br /><br /> 8 = 拒否の待機<br /><br /> 9 = 事前マスタシークレットを待機する<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = アービトレーションを待機する<br /><br /> 12 = オンライン<br /><br /> 13 = エラー|  
|**login_state_desc**|**nvarchar(60)**|リモートコンピューターからのログインの現在の状態。 指定できる値<br /><br /> 接続ハンドシェイクを初期化しています。<br /><br /> 接続ハンドシェイクは、Login Negotiate メッセージを待機しています。<br /><br /> 接続ハンドシェイクが初期化され、認証のためのセキュリティコンテキストが送信されました。<br /><br /> 接続ハンドシェイクを受信し、認証用のセキュリティ コンテキストを承諾しました。<br /><br /> 接続ハンドシェイクが初期化され、認証のためのセキュリティコンテキストが送信されました。 ピアを認証するために使用できるオプションのメカニズムがあります。<br /><br /> 接続ハンドシェイクを受信し、認証用のセキュリティ コンテキストを送信しました。 ピアを認証するために使用できるオプションのメカニズムがあります。<br /><br /> 接続ハンドシェイクは、セキュリティコンテキストの初期化の確認メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、受け入れセキュリティコンテキスト確認メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、失敗した認証に関する SSPI 拒否メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、マスタシークレットより前のメッセージを待機しています。<br /><br /> 接続ハンドシェイクは、Validation メッセージを待機しています。<br /><br /> 接続ハンドシェイクは、判別メッセージを待機しています。<br /><br /> 接続ハンドシェイクが完了し、メッセージ交換のためにオンライン (準備完了) になっています。<br /><br /> 接続にエラーがあります。|  
|**peer_certificate_id**|**int**|リモートインスタンスによって認証に使用される証明書のローカルオブジェクト ID。 この証明書の所有者には、データベース ミラーリング エンドポイントへの CONNECT 権限が必要です。|  
|**encryption_algorithm**|**smallint**|接続で使用される暗号化アルゴリズム。 NULLABLE. 指定できる値<br /><br /> **値:** 0<br /><br /> **説明:** 存在<br /><br /> **DDL オプション:** 無効に<br /><br /> **値:** 1<br /><br /> **説明:** RC4<br /><br /> **DDL オプション:** {必須 &#124; アルゴリズム RC4}<br /><br /> **値:** 2<br /><br /> **説明:** AES<br /><br /> **DDL オプション:** アルゴリズム AES が必要<br /><br /> **値:** 3<br /><br /> **説明:** なし、RC4<br /><br /> **DDL オプション:** {Supported &#124; サポートされているアルゴリズム RC4}<br /><br /> **値:** 4<br /><br /> **説明:** なし、AES<br /><br /> **DDL オプション:** サポートされているアルゴリズム RC4<br /><br /> **値:** 5<br /><br /> **説明:** RC4、AES<br /><br /> **DDL オプション:** アルゴリズム RC4 AES が必要です<br /><br /> **値:** 6<br /><br /> **説明:** AES、RC4<br /><br /> **DDL オプション:** アルゴリズム AES RC4 が必要<br /><br /> **値:** 7<br /><br /> **説明:** NONE、RC4、AES<br /><br /> **DDL オプション:** サポートされているアルゴリズム RC4 AES<br /><br /> **値:** 8<br /><br /> **説明:** NONE、AES、RC4<br /><br /> **DDL オプション:** サポートされているアルゴリズム AES RC4<br /><br /> **注:** RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 以降の [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] バージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材の暗号化を解除できます。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|暗号化アルゴリズムのテキスト表示。 NULLABLE. 有効値は次のとおりです。<br /><br /> **説明:** 存在<br /><br /> **DDL オプション:** 無効に<br /><br /> **説明:** RC4<br /><br /> **DDL オプション:** {必須 &#124; アルゴリズム RC4}<br /><br /> **説明:** AES<br /><br /> **DDL オプション:** アルゴリズム AES が必要<br /><br /> **説明:** なし、RC4<br /><br /> **DDL オプション:** {Supported &#124; サポートされているアルゴリズム RC4}<br /><br /> **説明:** NONE、AES<br /><br /> **DDL オプション:** サポートされているアルゴリズム RC4<br /><br /> **説明:** RC4、AES<br /><br /> **DDL オプション:** アルゴリズム RC4 AES が必要です<br /><br /> **説明:** AES、RC4<br /><br /> **DDL オプション:** アルゴリズム AES RC4 が必要<br /><br /> **説明:** NONE、RC4、AES<br /><br /> **DDL オプション:** サポートされているアルゴリズム RC4 AES<br /><br /> **説明:** NONE、AES、RC4<br /><br /> **DDL オプション:** サポートされているアルゴリズム AES RC4|  
|**receives_posted**|**smallint**|この接続でまだ完了していない非同期ネットワーク受信の数。|  
|**is_receive_flow_controlled**|**bit**|ネットワークがビジー状態のときに行われたフロー制御が原因で、ネットワーク受信が延期されたかどうか。<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|この接続でまだ完了していない非同期ネットワーク送信の数。|  
|**is_send_flow_controlled**|**bit**|ネットワークがビジー状態のためネットワークフロー制御のためにネットワーク送信が延期されているかどうか。<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|この接続で送信された合計バイト数。|  
|**total_bytes_received**|**bigint**|この接続で受信した合計バイト数。|  
|**total_fragments_sent**|**bigint**|この接続で送信されたデータベース ミラーリング メッセージ フラグメントの合計数。|  
|**total_fragments_received**|**bigint**|この接続で受信されたデータベース ミラーリング メッセージ フラグメントの合計数。|  
|**total_sends**|**bigint**|この接続によって発行されたネットワーク送信要求の合計数。|  
|**total_receives**|**bigint**|この接続によって発行されたネットワーク受信要求の合計数。|  
|**peer_arbitration_id**|**uniqueidentifier**|エンドポイントの内部識別子。 NULLABLE.|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="physical-joins"></a>物理結合  
 ![sys.join_dm_db_mirroring_connections の結合](../../relational-databases/system-dynamic-management-views/media/join-dm-db-mirroring-connections.gif "sys.join_dm_db_mirroring_connections の結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|終了|リレーションシップ|  
|----------|--------|------------------|  
|**dm_db_mirroring_connections.connection_id**|**dm_exec_connections.connection_id**|一対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
