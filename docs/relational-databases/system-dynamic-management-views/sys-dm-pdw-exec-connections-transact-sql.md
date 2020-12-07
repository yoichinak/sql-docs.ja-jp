---
description: sys.dm_pdw_exec_connections (Transact-sql)
title: sys.dm_pdw_exec_connections (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 507853f50ede1c652e81b24d60121deadad239d3
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035385"
---
# <a name="sysdm_pdw_exec_connections-transact-sql"></a>sys.dm_pdw_exec_connections (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  このインスタンスの [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] との間に確立された接続に関する情報と各接続の詳細を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|session_id|**int**|この接続に関連付けられたセッションの識別子。 `SESSION_ID()`現在の接続のを返すには、を使用し `session_id` ます。|  
|connect_time|**datetime**|接続が確立されたタイムスタンプ。 NULL 値は許可されません。|  
|encrypt_option|**nvarchar(40)**|TRUE (接続が暗号化されている) または FALSE (接続が暗号化されていない赤) を示します。|  
|auth_scheme|**nvarchar(40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]この接続で使用される/Windows 認証スキームを指定します。 NULL 値は許可されません。|  
|client_id|**varchar(48)**|このサーバーに接続しているクライアントの IP アドレス。 NULL 値が許可されます。|  
|sql_spid|**int**|接続のサーバープロセス ID。 `@@SPID`現在の接続のを返すには、を使用し `sql_spid` ます。ほとんどの遂行では、代わりにを使用し `session_id` ます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する **VIEW SERVER STATE** 権限が必要です。  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
| ソース | 終了 | Relationship |
| ---- | -- | ------------ |
|dm_pdw_exec_sessions dm_pdw_exec_sessions.session_id|dm_pdw_exec_connections dm_pdw_exec_connections.session_id|一対一|  
|dm_pdw_exec_requests dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections dm_pdw_exec_connections.connection_id|多対一|  
  
## <a name="examples-sssdwfull-and-sspdw"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 クエリ所有の接続に関する情報を収集するための一般的なクエリ。  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

