---
description: dm_exec_input_buffer (Transact-sql)
title: dm_exec_input_buffer (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4fecdc698dc7015ab47e5a8c97b3990c7e5bf1f4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536956"
---
# <a name="sysdm_exec_input_buffer-transact-sql"></a>dm_exec_input_buffer (Transact-sql)

[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

のインスタンスに送信されたステートメントに関する情報を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

## <a name="syntax"></a>構文

```
sys.dm_exec_input_buffer ( session_id , request_id )
```

## <a name="arguments"></a>引数

*session_id* 検索するバッチを実行するセッション ID を指定します。 *session_id* は **smallint**です。 *session_id* は、次の動的管理オブジェクトから取得できます。

- [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
- [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)
- [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)

*request_id*[Dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)からの request_id。 *request_id* は **int**です。

## <a name="table-returned"></a>返されるテーブル

|列名|データ型|説明|
|-----------------|---------------|-----------------|
|**event_type**|**nvarchar (256)**|指定された spid の入力バッファー内のイベントの種類。|
|**parameters**|**smallint**|ステートメントに対して指定されたすべてのパラメーター。|
|**event_info**|**nvarchar(max)**|指定された spid の入力バッファー内のステートメントのテキスト。|

## <a name="permissions"></a>アクセス許可

では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ユーザーが VIEW SERVER STATE 権限を持っている場合、のインスタンスで実行中のすべてのセッションが表示されます [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。それ以外の場合、ユーザーには現在のセッションのみが表示されます。

> [!IMPORTANT]
> VIEW SERVER STATE 権限を持たない SQL Server (トリガー、ストアドプロシージャ、関数など) に対してこの DMV を SQL Server Management Studio 以外で実行すると、master データベースで権限エラーがスローされます。

では、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ユーザーがデータベースの所有者である場合、ユーザーに対して実行中のすべてのセッションが表示されます。それ以外の場合、ユーザーには [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 現在のセッションのみが表示されます。

> [!IMPORTANT]
> 所有者権限を持たない Azure SQL Database (トリガー、ストアドプロシージャ、関数など) に対してこの DMV を SQL Server Management Studio 以外で実行すると、master データベースで権限エラーがスローされます。

## <a name="remarks"></a>解説

この動的管理関数は、 **クロス適用**を行うことによって、dm_exec_sessions または sys. dm_exec_requests と組み合わせて使用できます。

## <a name="examples"></a>例

### <a name="a-simple-example"></a>A. 簡単な例

次の例は、セッション ID (SPID) と要求 ID を関数に渡す方法を示しています。

```sql
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```

### <a name="b-using-cross-apply-to-additional-information"></a>B. クロス適用を追加情報に使用する

次の例では、セッション ID が50より大きいセッションの入力バッファーを一覧表示します。

```sql
SELECT es.session_id, ib.event_info
FROM sys.dm_exec_sessions AS es
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib
WHERE es.session_id > 50;
GO
```

## <a name="see-also"></a>参照

- [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
- [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)
- [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
- [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)
