---
description: dm_exec_connections (Transact-sql)
title: dm_exec_connections (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_connections_TSQL
- sys.dm_exec_connections_TSQL
- sys.dm_exec_connections
- dm_exec_connections
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_connections dynamic management view
ms.assetid: 6bd46fe1-417d-452d-a9e6-5375ee8690d8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9f9885ce0232b9fc36cbcec48ed17d16b54f4f57
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546652"
---
# <a name="sysdm_exec_connections-transact-sql"></a>dm_exec_connections (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  このインスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との間に確立された接続に関する情報と各接続の詳細を返します。 SQL Server のサーバー全体の接続情報を返します。 SQL Database の現在のデータベース接続情報を返します。  
  
> [!NOTE]
> またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 [dm_pdw_exec_connections &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|session_id|**int**|この接続に関連付けられたセッションの識別子。 NULL 値が許可されます。|  
|most_recent_session_id|**int**|この接続に関連付けられた最新の要求のセッション ID。 (SOAP 接続は別のセッションで再利用できます。)Null 値は許容されます。|  
|connect_time|**datetime**|接続が確立されたタイムスタンプ。 NULL 値は許可されません。|  
|net_transport|**nvarchar(40)**|接続で複数のアクティブな結果セット (MARS) が有効になっている場合は、常に **セッション** を返します。<br /><br /> **注:** この接続で使用される物理トランスポートプロトコルについて説明します。 NULL 値は許可されません。|  
|protocol_type|**nvarchar(40)**|ペイロードのプロトコルの種類。 現在、これによって TDS (TSQL) と SOAP が区別されています。 NULL 値が許可されます。|  
|protocol_version|**int**|この接続に関連付けられているデータアクセスプロトコルのバージョン。 NULL 値が許可されます。|  
|endpoint_id|**int**|この接続の種類を表す識別子。 この endpoint_id は sys.endpoints ビューのクエリに使用できます。 NULL 値が許可されます。|  
|encrypt_option|**nvarchar(40)**|この接続で暗号化が有効かどうかを表すブール値。 NULL 値は許可されません。|  
|auth_scheme|**nvarchar(40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]この接続で使用される/Windows 認証スキームを指定します。 NULL 値は許可されません。|  
|node_affinity|**smallint**|この接続が関係しているメモリ ノード。 NULL 値は許可されません。|  
|num_reads|**int**|この接続で発生したバイト読み取りの数。 NULL 値が許可されます。|  
|num_writes|**int**|この接続で発生したバイトの書き込みの数。 NULL 値が許可されます。|  
|last_read|**datetime**|この接続で最後に読み取られたときのタイムスタンプ。 NULL 値が許可されます。|  
|last_write|**datetime**|この接続で最後に書き込みが行われたときのタイムスタンプ。 NULL 値は許可されません。|  
|net_packet_size|**int**|情報とデータの転送に使用されたネットワーク パケット サイズ。 NULL 値が許可されます。|  
|client_net_address|**varchar(48)**|このサーバーに接続するクライアントのホスト アドレス。 NULL 値が許可されます。<br /><br /> V12 より前ので [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] は、この列は常に NULL を返します。|  
|client_tcp_port|**int**|この接続に関連付けられたクライアント コンピューターのポート番号。 NULL 値が許可されます。<br /><br /> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]の場合、この列は常に NULL を返します。|  
|local_net_address|**varchar(48)**|この接続の対象となったサーバーの IP アドレス。 TCP トランスポート プロバイダーを使用する接続の場合にのみ該当します。 NULL 値が許可されます。<br /><br /> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]の場合、この列は常に NULL を返します。|  
|local_tcp_port|**int**|接続で TCP トランスポートを使用した場合に、この接続の対象となったサーバー TCP ポート。 NULL 値が許可されます。<br /><br /> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]の場合、この列は常に NULL を返します。|  
|connection_id|**uniqueidentifier**|各接続の一意識別子。 NULL 値は許可されません。|  
|parent_connection_id|**uniqueidentifier**|MARS セッションが使用しているプライマリ接続を識別します。 NULL 値が許可されます。|  
|most_recent_sql_handle|**varbinary(64)**|この接続で実行された最新の要求の SQL ハンドル。 most_recent_sql_handle 列は、常に most_recent_session_id 列と同期されます。 NULL 値が許可されます。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="physical-joins"></a>物理結合  
 ![sys.dm_exec_connections の結合](../../relational-databases/system-dynamic-management-views/media/join-dm-exec-connections-1.gif "sys.dm_exec_connections の結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
| 最初の要素 | 2番目の要素 | リレーションシップ |
| --------------| -------------- | ------------ |  
|dm_exec_sessions。 session_id|dm_exec_connections.session_id|一対一|  
|dm_exec_requests.connection_id|dm_exec_connections.connection_id|多対一|  
|dm_broker_connections.connection_id|dm_exec_connections.connection_id|1対1|  
  
## <a name="examples"></a>例  
 クエリ所有の接続に関する情報を収集するための一般的なクエリ。  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>参照  

 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


