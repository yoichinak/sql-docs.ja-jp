---
description: sys.dm_pdw_exec_sessions (Transact-sql)
title: sys.dm_pdw_exec_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d155f836abb975b39ef7b2396057a43e59686f9b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035344"
---
# <a name="sysdm_pdw_exec_sessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  アプライアンス上で現在または最近開いているすべてのセッションに関する情報を保持します。 セッションごとに1行が表示されます。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|現在のクエリまたは最後のクエリの id (セッションが終了し、終了時にクエリが実行されていた場合)。 このビューのキー。|システム内のすべてのセッション間で一意です。|  
|status|**nvarchar (10)**|現在のセッションでは、セッションが現在アクティブであるかアイドル状態であるかを識別します。 過去のセッションでは、セッションの状態が [終了] または [強制終了] になっている場合があります (セッションが強制的に閉じられた場合)。|' ACTIVE '、' CLOSED '、' IDLE '、' 終了 '|  
|request_id|**nvarchar(32)**|現在のクエリまたは前回のクエリの実行の id。|システム内のすべての要求間で一意です。 何も実行されていない場合は Null です。|  
|security_id|**varbinary(85)**|セッションを実行しているプリンシパルのセキュリティ ID。||  
|login_name|**nvarchar(128)**|セッションを実行しているプリンシパルのログイン名。|ユーザーの名前付け規則に準拠した任意の文字列。|  
|login_time|**datetime**|ユーザーがログインし、このセッションが作成された日付と時刻。|現在の時刻より前の有効な **日時** 。|  
|query_count|**int**|セッションが作成されてから実行されたクエリ/要求の数をキャプチャします。|0以上。|  
|is_transactional|**bit**|セッションが現在トランザクション内にあるかどうかをキャプチャします。|自動コミットの場合は0、トランザクションの場合は1。|  
|client_id|**nvarchar (255)**|セッションのクライアント情報をキャプチャします。|任意の有効な文字列。|  
|app_name|**nvarchar (255)**|必要に応じて、接続プロセスの一部として設定されたアプリケーション名情報をキャプチャします。|任意の有効な文字列。|  
|sql_spid|**int**|SPID の id 番号。 このセッションを使用し `session_id` ます。 列を使用して `sql_spid` **sys.dm_pdw_nodes_exec_sessions**に結合します。<br /><br /> 警告この列には閉じた spid が含まれています。 ** \* \* \* \* **||  
  
 このビューで保持される最大行数の詳細については、「 [容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」トピックの「メタデータ」セクションを参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 `VIEW SERVER STATE` アクセス許可が必要です。  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
