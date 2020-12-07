---
description: sp_describe_cursor_columns (Transact-SQL)
title: sp_describe_cursor_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_columns
- sp_describe_cursor_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_columns
ms.assetid: 6eaa54af-7ba4-4fce-bf6c-6ac67cc1ac94
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 75d0de65b91c41cdaf006e4c56918c3861123b9c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539022"
---
# <a name="sp_describe_cursor_columns-transact-sql"></a>sp_describe_cursor_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバー カーソルの結果セットにある列の属性をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_describe_cursor_columns   
   [ @cursor_return = ] output_cursor_variable OUTPUT   
    { [ , [ @cursor_source = ] N'local' ,   
          [ @cursor_identity = ] N'local_cursor_name' ]   
    | [ , [ @cursor_source = ] N'global' ,   
          [ @cursor_identity = ] N'global_cursor_name' ]   
    | [ , [ @cursor_source = ] N'variable' ,   
          [ @cursor_identity = ] N'input_cursor_variable' ]   
   }  
```  
  
## <a name="arguments"></a>引数  
 [ @cursor_return =] *output_cursor_variable* 出力  
 カーソル出力を受け取るように宣言したカーソル変数の名前です。 *output_cursor_variable* は **カーソル**であり、既定値はありません。 sp_describe_cursor_columns が呼び出されたときに、どのカーソルにも関連付けないでください。 返されるカーソルは、スクロール可能、動的、読み取り専用のカーソルです。  
  
 [ @cursor_source =] {N'local ' |N'global ' |N'variable' }  
 ローカルカーソル、グローバルカーソル、またはカーソル変数の名前を使用して、レポートされるカーソルが指定されているかどうかを指定します。 パラメーターは **nvarchar (30)** です。  
  
 [ @cursor_identity =] N '*local_cursor_name*'  
 LOCAL キーワードを持つ DECLARE CURSOR ステートメントによって作成されたカーソルの名前を指定します。または、LOCAL に既定値を指定します。 *local_cursor_name* は **nvarchar (128)** です。  
  
 [ @cursor_identity =] N '*global_cursor_name*'  
 GLOBAL キーワードを持つ DECLARE CURSOR ステートメントによって作成されたカーソルの名前、またはグローバルに既定値が指定されているカーソルの名前を指定します。 *global_cursor_name* は **nvarchar (128)** です。  
  
 *global_cursor_name* には、ODBC アプリケーションによって開かれ、SQLSetCursorName を呼び出すことによって名前が付けられた API サーバーカーソルの名前を指定することもできます。  
  
 [ @cursor_identity =] N '*input_cursor_variable*'  
 開いているカーソルに関連付けられたカーソル変数の名前です。 *input_cursor_variable* は **nvarchar (128)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 sp_describe_cursor_columns は、そのレポートを、カーソル出力パラメーターとしてカプセル化 [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor**します。 これにより、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ、ストアドプロシージャ、およびトリガーは、一度に1行ずつ出力を処理できます。 これはまた、データベース API 関数からプロシージャを直接呼び出すことができないことを意味します。 **Cursor**出力パラメーターはプログラム変数にバインドする必要がありますが、データベース api では、**カーソル**パラメーターまたは変数のバインドがサポートされていません。  
  
 次の表に、sp_describe_cursor_columns が返すカーソルの形式を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|column_name|**sysname** (null 値を許容)|結果セット列に割り当てられた名前です。 列が、付随する AS 句なしで指定されている場合、この列は NULL になります。|  
|ordinal_position|**int**|結果セットで左端の列を基準とする列の相対位置です。 最初の列は0の位置にあります。|  
|column_characteristics_flags|**int**|OLE DB の DBCOLUMNFLAGS に格納されている情報を示すビットマスク。 次の1つまたは複数の組み合わせを指定できます。<br /><br /> 1 = ブックマーク<br /><br /> 2 = 固定長<br /><br /> 4 = NULL 値を許容<br /><br /> 8 = 行のバージョン管理<br /><br /> 16 = 更新可能な列 (FOR UPDATE 句がないカーソルの射影された列に対して設定されます。このような列がある場合は、カーソルごとに1つしか指定できません)。<br /><br /> ビット値を結合する場合は、組み合わせたビット値の特性が適用されます。 たとえば、ビット値が6の場合、列は固定長 (2)、nullable (4) 列になります。|  
|column_size|**int**|この列で可能な値の最大サイズです。|  
|data_type_sql|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列のデータ型を示す数値。|  
|column_precision|**tinyint**|OLE DB の *Bprecision* 値に対する列の最大有効桁数。|  
|column_scale|**tinyint**|**数値**または**10 進数**のデータ型の小数点の右側の桁数。 OLE DB の*bscale*値に従います。|  
|order_position|**int**|列が結果セットの順序付けに参加している場合は、一番左の列に対する順序キーの列の位置。|  
|order_direction|**varchar (1)**(null 値を許容)|A = 列は順序キーにあり、順序付けは昇順です。<br /><br /> D = 列は順序キーにあり、順序付けは降順です。<br /><br /> NULL = 列は順序付けに関係しません。|  
|hidden_column|**smallint**|0 = この列は選択リストに表示されます。<br /><br /> 1 = 将来使用するために予約されています。|  
|columnid|**int**|基本列の列 ID。 結果セット列が式で構成されている場合、columnid は -1 です。|  
|objectid|**int**|列を提供しているオブジェクトまたはベーステーブルのオブジェクト ID。 結果セット列が式で構成されている場合、objectid は -1 です。|  
|dbid|**int**|列の値を提供するベース テーブルを含むデータベースの ID です。 結果セット列が式で構成されている場合、dbid は -1 です。|  
|dbname|**sysname**<br /><br /> nullable|列を提供しているベーステーブルを含むデータベースの名前。 結果セット列が式で構成されている場合、dbname は NULL です。|  
  
## <a name="remarks"></a>解説  
 sp_describe_cursor_columns は、各カーソルの名前やデータ型など、サーバー カーソルの結果セットにある列の属性を示します。 サーバー カーソルにグローバルな属性の説明が必要な場合は、sp_describe_cursor を使用します。 カーソルが参照するベース テーブルのレポートが必要な場合は、sp_describe_cursor_tables を使用します。 接続時に可視になる [!INCLUDE[tsql](../../includes/tsql-md.md)] Server カーソルのレポートが必要な場合は、sp_cursor_list を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、グローバル カーソルをオープンし、カーソルで使用されている列を `sp_describe_cursor_columns` を使用してレポートします。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person;  
GO  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_columns.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_columns into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_columns  
    @cursor_return = @Report OUTPUT  
    ,@cursor_source = N'global'   
    ,@cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_columns output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_columns.  
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
 [sp_describe_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
