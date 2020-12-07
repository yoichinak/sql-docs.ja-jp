---
description: dm_exec_cursors (Transact-sql)
title: dm_exec_cursors (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cursors_TSQL
- dm_exec_cursors
- dm_exec_cursors_TSQL
- sys.dm_exec_cursors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cursors dynamic management function
ms.assetid: f520b63c-36af-40f1-bf71-6901d6331d3d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 351f97ed08d1a6a79f8611d19842dc93138277ce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543941"
---
# <a name="sysdm_exec_cursors-transact-sql"></a>dm_exec_cursors (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  各種データベースで開いているカーソルに関する情報を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
dm_exec_cursors (session_id | 0 )  
```  
  
## <a name="arguments"></a>引数  
 *session_id* |0  
 セッションの ID。 *Session_id*が指定されている場合、この関数は、指定されたセッションのカーソルに関する情報を返します。  
  
 0 を指定した場合、この関数ではすべてのセッションのすべてのカーソルに関する情報が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|このカーソルを保持するセッションの ID。|  
|**cursor_id**|**int**|カーソルオブジェクトの ID。|  
|**name**|**nvarchar (256)**|ユーザーによって定義されたカーソルの名前。|  
|**properties**|**nvarchar (256)**|カーソルのプロパティ。 次のプロパティの値が連結され、この列の値が形成されます。<br />宣言インターフェイス<br />カーソルの種類 <br />カーソルの同時実行<br />カーソルのスコープ<br />カーソルの入れ子レベル<br /><br /> たとえば、この列で返される値は、"TSQL &#124; Dynamic &#124; オプティミスティック &#124; Global (0)" のようになります。|  
|**sql_handle**|**varbinary(64)**|カーソルを宣言したバッチのテキストを処理します。|  
|**statement_start_offset**|**int**|現在実行中のバッチまたはストアド プロシージャに含まれる、現在実行中のステートメントが開始されるまでの文字数。 **Sql_handle**、 **statement_end_offset**、および[dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)の動的管理関数と共に使用して、要求に対して現在実行中のステートメントを取得できます。|  
|**statement_end_offset**|**int**|現在実行中のバッチまたはストアドプロシージャ内で現在実行中のステートメントが終了するまでの文字数。 **Sql_handle**、 **statement_start_offset**、および**dm_exec_sql_text**の動的管理関数と共に使用して、要求に対して現在実行中のステートメントを取得できます。|  
|**plan_generation_num**|**bigint**|再コンパイル後にプランのインスタンスを区別するために使用できるシーケンス番号。|  
|**creation_time**|**datetime**|カーソルが作成されたタイムスタンプ。|  
|**is_open**|**bit**|カーソルが開いているかどうかを示します。|  
|**is_async_population**|**bit**|バックグラウンドスレッドがキーセットまたは静的カーソルに非同期的に設定するかどうかを指定します。|  
|**is_close_on_commit**|**bit**|カーソルが CURSOR_CLOSE_ON_COMMIT を使用して宣言されたかどうかを指定します。<br /><br /> 1 = カーソルはトランザクションが終了したときに閉じられます。|  
|**fetch_status**|**int**|カーソルの最後のフェッチの状態を返します。 これは、最後に返された @ @FETCH_STATUS value です。|  
|**fetch_buffer_size**|**int**|フェッチ バッファーのサイズに関する情報。<br /><br /> 1 = Transact-SQL カーソル。 これは、API カーソルに対してより高い値に設定できます。|  
|**fetch_buffer_start**|**int**|カーソルが開いていない場合、またはカーソルが最初の行の前に配置されている場合は、FAST_FORWARD および動的カーソルの場合は0を返します。 それ以外のときは -1 が返されます。<br /><br /> 静的カーソルとキーセットカーソルの場合は、カーソルが開いていない場合は0、カーソルが最後の行の次の位置にある場合は-1 を返します。<br /><br /> それ以外の場合は、配置されている行番号を返します。|  
|**ansi_position**|**int**|フェッチバッファー内のカーソル位置。|  
|**worker_time**|**bigint**|このカーソルを実行しているワーカーにかかった時間 (マイクロ秒単位)。|  
|**読ん**|**bigint**|カーソルによって実行された読み取りの数。|  
|**よる**|**bigint**|カーソルによって実行された書き込みの数。|  
|**dormant_duration**|**bigint**|このカーソルで最後のクエリ (open または fetch) が開始されてからのミリ秒数。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 次の表では、cursor 宣言インターフェイスについて説明し、properties 列に使用できる値を示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|API|カーソルは、データアクセス Api (ODBC、OLEDB) のいずれかを使用して宣言されています。|  
|TSQL|カーソルは、Transact-sql DECLARE CURSOR 構文を使用して宣言されています。|  
  
 次の表は、カーソルの種類に関する説明と、プロパティ列に返される値です。  
  
|種類|説明|  
|----------|-----------------|  
|Keyset|カーソルはキーセットとして宣言されています。|  
|動的|カーソルは動的として宣言されました。|  
|スナップショット|カーソルが Snapshot または Static として宣言されました。|  
|Fast_Forward|カーソルは高速順方向として宣言されています。|  
  
 次の表は、カーソルのコンカレンシーに関する説明と、プロパティ列に返される値です。  
  
|コンカレンシー|説明|  
|-----------------|-----------------|  
|[読み取り専用]|カーソルは読み取り専用として宣言されました。|  
|Scroll Locks|カーソルはスクロールロックを使用します。|  
|Optimistic|カーソルはオプティミスティック同時実行制御を使用します。|  
  
 次の表に、カーソルのスコープについて説明し、[プロパティ] 列に使用できる値を示します。  
  
|Scope|説明|  
|-----------|-----------------|  
|ローカル|カーソルのスコープは、カーソルが作成されたバッチ、ストアド プロシージャ、またはトリガーに対してローカルです。|  
|グローバル|カーソルのスコープは、接続に対してグローバルです。|  
  
## <a name="examples"></a>例  
  
### <a name="a-detecting-old-cursors"></a>A. 古いカーソルを検出する  
 この例では、サーバー上で開いているカーソルに関する情報を、指定した時間36時間より長くして返します。  
  
```  
SELECT creation_time, cursor_id, name, c.session_id, login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s ON c.session_id = s.session_id   
WHERE DATEDIFF(hh, c.creation_time, GETDATE()) > 36;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
  

