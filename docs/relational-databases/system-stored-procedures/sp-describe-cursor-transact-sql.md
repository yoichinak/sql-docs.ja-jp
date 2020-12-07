---
description: sp_describe_cursor (Transact-SQL)
title: sp_describe_cursor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c2e24c729dce92d05827466d9931916a9002adc1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548124"
---
# <a name="sp_describe_cursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーカーソルの属性をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
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
 [ @cursor_return =] *output_cursor_variable* 出力  
 カーソル出力を受け取るように宣言したカーソル変数の名前です。 *output_cursor_variable* は **カーソル**であり、既定値はありません。 sp_describe_cursor が呼び出されたときに、どのカーソルにも関連付けないでください。 返されるカーソルは、スクロール可能、動的、読み取り専用のカーソルです。  
  
 [ @cursor_source =] {N'local ' |N'global ' |N'variable' }  
 ローカルカーソル、グローバルカーソル、またはカーソル変数の名前を使用して、レポートされるカーソルが指定されているかどうかを指定します。 パラメーターは **nvarchar (30)** です。  
  
 [ @cursor_identity =] N '*local_cursor_name*']  
 LOCAL キーワードを持つ DECLARE CURSOR ステートメントによって作成されたカーソルの名前を指定します。または、LOCAL に既定値を指定します。 *local_cursor_name* は **nvarchar (128)** です。  
  
 [ @cursor_identity =] N '*global_cursor_name*']  
 GLOBAL キーワードを持つ DECLARE CURSOR ステートメントによって作成されたカーソルの名前、またはグローバルに既定値が指定されているカーソルの名前を指定します。 *global_cursor_name* は **nvarchar (128)** です。  
  
 *global_cursor_name* には、SQLSetCursorName を呼び出して名前を付けた ODBC アプリケーションによって開かれる API サーバーカーソルの名前を指定することもできます。  
  
 [ @cursor_identity =] N '*input_cursor_variable*']  
 開いているカーソルに関連付けられたカーソル変数の名前です。 *input_cursor_variable* は **nvarchar (128)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 sp_describe_cursor は、カーソル出力パラメーターに結果セットをカプセル化 [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor**します。 これにより、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ、ストアドプロシージャ、およびトリガーは、一度に1行ずつ出力を処理できます。 これはまた、データベース API 関数からプロシージャを直接呼び出すことができないことを意味します。 **Cursor**出力パラメーターはプログラム変数にバインドする必要がありますが、データベース api では、**カーソル**パラメーターまたは変数のバインドがサポートされていません。  
  
 次の表に、sp_describe_cursor が返すカーソルの形式を示します。 カーソルの形式は、sp_cursor_list を使用した場合に返される形式と同じです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|カーソルを参照するために使用される名前です。 DECLARE CURSOR ステートメントに指定された名前を介してカーソルを参照すると、参照名はカーソル名と同じになります。 カーソルへの参照が変数を介して行われた場合、参照名は変数の名前になります。|  
|cursor_name|**sysname**|DECLARE CURSOR ステートメントからのカーソルの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、カーソルがカーソル変数を設定して作成されると、cursor_name にカーソル変数の名前が返されます。 以前のバージョンのでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この出力列にはシステムによって生成された名前が返されていました。|  
|cursor_scope|**tinyint**|1 = ローカル<br /><br /> 2 = GLOBAL|  
|status|**int**|CURSOR_STATUS システム関数によって報告されたものと同じ値:<br /><br /> 1 = カーソル名または変数によって参照されているカーソルが開いています。 カーソルが状態非依存、静的、キーセットのいずれかの場合には、結果セットに少なくとも 1 行が含まれます。 カーソルが動的な場合、結果セットには0個以上の行が含まれます。<br /><br /> 0 = カーソル名または変数によって参照されるカーソルが開かれていますが、行がありません。 動的カーソルがこの値を返すことはありません。<br /><br /> -1 = カーソル名または変数によって参照されたカーソルは閉じています。<br /><br /> -2 = カーソル変数にのみ適用されます。 変数に割り当てられたカーソルがありません。 おそらく、OUTPUT パラメーターによってカーソルを変数に割り当てましたが、戻る前にストアド プロシージャがカーソルを閉じました。<br /><br /> -3 = 指定された名前のカーソルまたはカーソル変数が存在しないか、またはカーソル変数にカーソルが割り当てられていません。|  
|対象となるのは、モデル|**tinyint**|1 = 非依存 (または静的)<br /><br /> 2 = キーセット<br /><br /> 3 = 動的<br /><br /> 4 = 高速順方向|  
|concurrency|**tinyint**|1 = 読み取り専用<br /><br /> 2 = スクロール ロック<br /><br /> 3 = オプティミスティック|  
|scrollable|**tinyint**|0 = 順方向専用<br /><br /> 1 = スクロール可能|  
|open_status|**tinyint**|0 = 終了<br /><br /> 1 = 開く|  
|cursor_rows|**decimal (10, 0)**|結果セット内の条件を満たす行の数。 詳細については、「[@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)」を参照してください。|  
|fetch_status|**smallint**|このカーソルの最後のフェッチの状態。 詳細については、「[@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)」を参照してください。<br /><br /> 0 = フェッチが成功しました。<br /><br /> -1 = フェッチが失敗したか、カーソルの境界を超えています。<br /><br /> -2 = 要求された行がありません。<br /><br /> -9 = カーソル上でフェッチは行われていません。|  
|column_count|**smallint**|カーソル結果セット内の列の数。|  
|row_count|**decimal (10, 0)**|カーソルに対する最後の操作によって影響を受けた行の数。 詳細については、「[@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)」を参照してください。|  
|last_operation|**tinyint**|カーソルに対して最後に実行された操作:<br /><br /> 0 = カーソルに対して操作が実行されていません。<br /><br /> 1 = OPEN <br /><br /> 2 = FETCH <br /><br /> 3 = 挿入<br /><br /> 4 = UPDATE <br /><br /> 5 = 削除<br /><br /> 6 = 閉じる<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|サーバーのスコープ内のカーソルの一意の値。|  
  
## <a name="remarks"></a>解説  
 sp_describe_cursor は、カーソルがスクロール可能かどうか、更新可能かどうかなど、サーバー カーソルのグローバルな属性を説明します。 カーソルから返された結果セットの属性の説明が必要な場合は、sp_describe_cursor_columns を使用します。 カーソルが参照するベース テーブルのレポートが必要な場合は、sp_describe_cursor_tables を使用します。 接続時に可視になる [!INCLUDE[tsql](../../includes/tsql-md.md)] Server カーソルのレポートが必要な場合は、sp_cursor_list を使用します。  
  
 Declare cursor ステートメントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DECLARE cursor に含まれる SELECT ステートメントの使用をサポートできないカーソルの種類を要求する場合があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT ステートメントを使用して、サポートできる型にカーソルを暗黙的に変換します。 DECLARE CURSOR ステートメントで TYPE_WARNING が指定されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換が完了したことを示す情報メッセージがアプリケーションに送信されます。 その後、sp_describe_cursor を呼び出して、実装されているカーソルの種類を判断できます。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、グローバル カーソルを開き、`sp_describe_cursor` を使用してカーソルの属性をレポートします。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
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
 [sp_describe_cursor_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
