---
description: sp_describe_cursor_tables (Transact-SQL)
title: sp_describe_cursor_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_tables_TSQL
- sp_describe_cursor_tables
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_tables
ms.assetid: 02c0f81a-54ed-4ca4-aa4f-bb7463a9ab9a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eec1a0d9d8e61613558e0f34b13080a67ba5335b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539002"
---
# <a name="sp_describe_cursor_tables-transact-sql"></a>sp_describe_cursor_tables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーカーソルによって参照されるオブジェクトまたはベーステーブルを報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_describe_cursor_tables   
     [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
     , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
     , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @cursor_return =] *output_cursor_variable*出力  
 カーソル出力を受け取るように宣言したカーソル変数の名前です。 *output_cursor_variable* は **カーソル**であり、既定値はありません。 sp_describe_cursor_tables が呼び出されたときに、どのカーソルにも関連付けないでください。 返されるカーソルは、スクロール可能、動的、読み取り専用のカーソルです。  
  
 [ @cursor_source =] {N'local ' |N'global ' |N'variable' }  
 ローカルカーソル、グローバルカーソル、またはカーソル変数の名前を使用して、レポートされるカーソルが指定されているかどうかを指定します。 パラメーターは **nvarchar (30)** です。  
  
 [ @cursor_identity =] N '*local_cursor_name*'  
 DECLARE CURSOR ステートメントによって作成されたカーソルの名前を指定します。 DECLARE CURSOR ステートメントは、LOCAL キーワードを持つか、既定値は LOCAL になります。 *local_cursor_name* は **nvarchar (128)** です。  
  
 [ @cursor_identity =] N '*global_cursor_name*'  
 DECLARE CURSOR ステートメントによって作成されたカーソルの名前を指定します。 GLOBAL キーワードを持つか、またはグローバルに既定値が指定されています。 *global_cursor_name* には、ODBC アプリケーションによって開かれた API サーバーカーソルの名前を指定することもできます。その後、SQLSetCursorName を呼び出してカーソルに名前を付けます。*global_cursor_name* は **nvarchar (128)** です。  
  
 [ @cursor_identity =] N '*input_cursor_variable*'  
 開いているカーソルに関連付けられたカーソル変数の名前です。 *input_cursor_variable* は **nvarchar (128)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 sp_describe_cursor_tables は、そのレポートを、カーソル出力パラメーターとしてカプセル化 [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor**します。 これにより、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ、ストアドプロシージャ、およびトリガーは、一度に1行ずつ出力を処理できます。 これは、このプロシージャを API 関数から直接呼び出すことができないことも意味します。 **Cursor**出力パラメーターはプログラム変数にバインドする必要がありますが、api では**カーソル**パラメーターまたは変数のバインドがサポートされていません。  
  
 次の表に、sp_describe_cursor_tables が返すカーソルの形式を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|テーブルの所有者|**sysname**|テーブル所有者のユーザー ID。|  
|Table_name|**sysname**|オブジェクトまたはベース テーブルの名前。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、サーバーカーソルは常に、ベーステーブルではなく、ユーザーが指定したオブジェクトを返します。|  
|optimizer_hints|**smallint**|次の1つ以上で構成されるビットマップ。<br /><br /> 1 = 行レベルのロック (ROWLOCK)<br /><br /> 4 = ページレベルのロック (PAGELOCK)<br /><br /> 8 = テーブルロック (TABLOCK)<br /><br /> 16 = 排他テーブルロック (TABLOCKX)<br /><br /> 32 = 更新ロック (UPDLOCK)<br /><br /> 64 = ロックなし (NOLOCK)<br /><br /> 128 = 高速順方向参照 (FASTFIRST)<br /><br /> 4096 = DECLARE CURSOR で使用する場合、反復可能セマンティックの読み取り (HOLDLOCK)<br /><br /> 複数のオプションを指定する場合、システムは最も限定的なオプションを使用します。 ただし、sp_describe_cursor_tables は、クエリに指定されているフラグを表示します。|  
|lock_type|**smallint**|このカーソルの基になる各ベーステーブルに対して、明示的または暗黙的に要求されたスクロールロックの種類。 値は次のいずれかになります。<br /><br /> 0 = なし<br /><br /> 1 = 共有<br /><br /> 3 = 更新|  
|server_name|**sysname、nullable**|テーブルが存在するリンクサーバーの名前。 OPENQUERY または OPENROWSET が使用されている場合は NULL です。|  
|Objectid|**int**|テーブルのオブジェクト ID。 OPENQUERY または OPENROWSET が使用されている場合は0です。|  
|dbid|**int**|テーブルが存在するデータベースの ID。 OPENQUERY または OPENROWSET が使用されている場合は0です。|  
|dbname|**sysname**、 **nullable**|テーブルが存在するデータベースの名前。 OPENQUERY または OPENROWSET が使用されている場合は NULL です。|  
  
## <a name="remarks"></a>解説  
 sp_describe_cursor_tables は、サーバー カーソルが参照するベース テーブルを説明します。 カーソルから返された結果セットの属性の説明が必要な場合は、sp_describe_cursor_columns を使用します。 スクロール可能かどうか、更新可能かどうかなど、カーソルの総体的な特性の説明が必要な場合は、sp_describe_cursor を使用します。 接続時に可視である [!INCLUDE[tsql](../../includes/tsql-md.md)] Server カーソルに関するレポートが必要な場合は、sp_cursor_list を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、グローバルカーソルを開き、を使用し `sp_describe_cursor_tables` て、カーソルによって参照されているテーブルに関するレポートを作成します。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
  
OPEN abc;  
GO  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_tables.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_tables into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_tables  
      @cursor_return = @Report OUTPUT,  
      @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_tables output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_tables.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [カーソル](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;Transact-sql&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
