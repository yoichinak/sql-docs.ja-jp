---
description: fn_get_sql (Transact-sql)
title: fn_get_sql (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_sql
- sys.fn_get_sql_TSQL
- fn_get_sql_TSQL
- sys.fn_get_sql
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_sql function
- text [SQL Server], SQL handles
- sys.fn_get_sql function
- valid SQL handles [SQL Server]
- SQL handles
ms.assetid: d5fe49b5-0813-48f2-9efb-9187716b2fd4
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f5e3f4af1cd1bae33f0a340333cb6afd3268158
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427804"
---
# <a name="sysfn_get_sql-transact-sql"></a>fn_get_sql (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定された SQL ハンドルの SQL ステートメントのテキストを返します。  
  
> [!IMPORTANT]  
>  この機能は、Microsoft SQL Server の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに sys.dm_exec_sql_text を使用してください。 詳細については、「 [sys. dm_exec_sql_text &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)」を参照してください。  
  
 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_get_sql ( SqlHandle )  
```  
  
## <a name="arguments"></a>引数  
 *SqlHandle*  
 ハンドル値を指定します。 *Sqlhandle* は **varbinary (64)** で、既定値はありません。  
  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|dbid|**smallint**|データベース ID。 アドホック SQL ステートメントおよび準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。|  
|objectid|**int**|データベース オブジェクトの ID。 アドホック SQL ステートメントの場合は NULL になります。|  
|number|**smallint**|プロシージャがグループ化されている場合は、グループの番号を示します。<br /><br /> 0 = エントリはプロシージャではありません。<br /><br /> NULL = アドホック SQL ステートメント|  
|encrypted|**bit**|オブジェクトが暗号化されているかどうかを示します。<br /><br /> 0 = 暗号化なし<br /><br /> 1 = 暗号化|  
|text|**text**|SQL ステートメントのテキストを入力します。 暗号化されているオブジェクトの場合は NULL になります。|  
  
## <a name="remarks"></a>解説  
 有効な SQL ハンドルを取得するには、 [dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 動的管理ビューの sql_handle 列を使用します。  
  
 キャッシュに存在しなくなったハンドルを渡すと、fn_get_sq**l** は空の結果セットを返します。 無効なハンドルを渡した場合、バッチは停止し、エラーメッセージが返されます。  
  
 では、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 一括コピーステートメントや、8 KB を超える文字列リテラルを含むステートメントなど、一部のステートメントをキャッシュすることはできません。 このようなステートメントに対するハンドルは、fn_get_sql では取得できません。  
  
 結果セットの **テキスト** 列は、パスワードを含む可能性のあるテキストに対してフィルター処理されます。 監視されていないセキュリティ関連のストアドプロシージャの詳細については、「 [トレースのフィルター選択](../../relational-databases/sql-trace/filter-a-trace.md)」を参照してください。  
  
 Fn_get_sql 関数は、 [DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md) コマンドに似た情報を返します。 次に示すのは、fn_get_sql 関数を使用できる場合の例です。 DBCC INPUTBUFFER を指定することはできません。  
  
-   イベントの文字数が 255 文字を超える場合。  
  
-   ストアドプロシージャの現在の入れ子の最上位レベルを返す必要がある場合。 たとえば、sp_1 と sp_2 という名前の 2 つのストアド プロシージャがある場合に、 sp_1 で sp_2 を呼び出し、sp_2 の実行中に sys.dm_exec_requests 動的管理ビューからハンドルを取得すると、fn_get_sql 関数では sp_2 に関する情報が返されます。 さらに fn_get_sql 関数では、現在の入れ子の最上位レベルにあるストアド プロシージャの完全なテキストが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
 データベース管理者は、次の例のように fn_get_sql 関数を使用して、問題があるプロセスを診断できます。 この場合、まず問題があるセッション ID を特定した後、そのセッションに対する SQL ハンドルを取得します。次にそのハンドルで fn_get_sql を呼び出した後、開始オフセットと終了オフセットを使用して、問題があるセッション ID の SQL ステートメントを確認します。  
  
```  
DECLARE @Handle varbinary(64);  
SELECT @Handle = sql_handle   
FROM sys.dm_exec_requests   
WHERE session_id = 52 and request_id = 0;  
SELECT * FROM sys.fn_get_sql(@Handle);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DBCC INPUTBUFFER &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)   
 [sys.sysプロセス &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
