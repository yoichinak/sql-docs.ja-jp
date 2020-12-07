---
description: sp_cursor_list (Transact-sql)
title: sp_cursor_list (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_list
- sp_cursor_list_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_list
ms.assetid: 7187cfbe-d4d9-4cfa-a3bb-96a544c7c883
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dca9473813bf8e4324f1b7de6fb1a30c38a21148
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536651"
---
# <a name="sp_cursor_list-transact-sql"></a>sp_cursor_list (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  接続に対して現在開いているサーバーカーソルの属性を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursor_list [ @cursor_return = ] cursor_variable_name OUTPUT   
     , [ @cursor_scope = ] cursor_scope  
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @cursor_return =] *cursor_variable_name*出力  
 宣言されたカーソル変数の名前を指定します。 *cursor_variable_name* は **カーソル**,、既定値はありません。 カーソルは、スクロール可能な動的な読み取り専用カーソルです。  
  
 [ @cursor_scope =] *cursor_scope*  
 レポートするカーソルのレベルを指定します。 *cursor_scope* は **int**,、既定値はありませんが、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|1|すべてのローカル カーソルをレポートします。|  
|2|すべてのグローバル カーソルをレポートします。|  
|3|ローカル カーソルとグローバル カーソルの両方をレポートします。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 sp_cursor_list は、結果セットとしてではなく、[!INCLUDE[tsql](../../includes/tsql-md.md)] カーソル出力パラメーターとしてレポートを返します。 これにより、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ、ストアドプロシージャ、およびトリガーは、一度に1行ずつ出力を処理できます。 また、データベース API 関数からプロシージャを直接呼び出すことができなくなります。 Cursor 出力パラメーターはプログラム変数にバインドする必要がありますが、データベース Api では、カーソルパラメーターまたは変数のバインドがサポートされていません。  
  
 以下は、sp_cursor_list から返されるカーソルの形式です。 このカーソルの形式は、sp_describe_cursor から返される形式と同じです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|カーソルを参照するために使用される名前。 DECLARE CURSOR ステートメントで指定された名前を使用してカーソルを参照した場合、参照名はカーソル名と同じになります。 カーソルへの参照が変数を介して行われた場合、参照名はカーソル変数の名前になります。|  
|cursor_name|**sysname**|DECLARE CURSOR ステートメントに指定されたカーソルの名前です。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、カーソル変数をカーソルに設定することによってカーソルが作成された場合、 **cursor_name** はカーソル変数の名前を返します。  以前のリリースでは、この出力列にはシステムによって生成された名前が返されていました。|  
|cursor_scope|**smallint**|1 = ローカル<br /><br /> 2 = GLOBAL|  
|status|**smallint**|CURSOR_STATUS システム関数によって報告されたものと同じ値です。<br /><br /> 1 = カーソル名または変数によって参照されているカーソルが開いています。 カーソルが状態非依存、静的、キーセットのいずれかの場合には、結果セットに少なくとも 1 行が含まれます。 カーソルが動的な場合、結果セットには0個以上の行が含まれます。<br /><br /> 0 = カーソル名または変数によって参照されるカーソルが開かれていますが、行がありません。 動的カーソルがこの値を返すことはありません。<br /><br /> -1 = カーソル名または変数によって参照されたカーソルは閉じています。<br /><br /> -2 = カーソル変数にのみ適用されます。 変数に割り当てられたカーソルがありません。 おそらく、OUTPUT パラメーターによってカーソルを変数に割り当てましたが、戻る前にストアド プロシージャがカーソルを閉じました。<br /><br /> -3 = 指定された名前のカーソルまたはカーソル変数が存在しないか、またはカーソル変数にカーソルが割り当てられていません。|  
|対象となるのは、モデル|**smallint**|1 = 非依存 (または静的)<br /><br /> 2 = キーセット<br /><br /> 3 = 動的<br /><br /> 4 = 高速順方向|  
|concurrency|**smallint**|1 = 読み取り専用<br /><br /> 2 = スクロール ロック<br /><br /> 3 = オプティミスティック|  
|scrollable|**smallint**|0 = 順方向専用<br /><br /> 1 = スクロール可能|  
|open_status|**smallint**|0 = 終了<br /><br /> 1 = 開く|  
|cursor_rows|**int**|結果セット内の条件を満たす行の数。 詳細については、「 [@ @CURSOR_ROWS ](../../t-sql/functions/cursor-rows-transact-sql.md)」を参照してください。|  
|fetch_status|**smallint**|このカーソル上での最後のフェッチの状態です。 詳細については、次を参照してください。 [@ @FETCH_STATUS ](../../t-sql/functions/fetch-status-transact-sql.md):<br /><br /> 0 = フェッチが成功しました。<br /><br /> -1 = フェッチが失敗したか、カーソルの境界を超えています。<br /><br /> -2 = 要求された行がありません。<br /><br /> -9 = カーソル上でフェッチは行われていません。|  
|column_count|**smallint**|カーソル結果セット内の列の数。|  
|row_count|**smallint**|カーソルに対する最後の操作によって影響を受けた行の数。 詳細については、「 [@ @ROWCOUNT ](../../t-sql/functions/rowcount-transact-sql.md)」を参照してください。|  
|last_operation|**smallint**|カーソルに対して最後に実行された操作:<br /><br /> 0 = カーソルに対して操作が実行されていません。<br /><br /> 1 = OPEN <br /><br /> 2 = FETCH <br /><br /> 3 = 挿入<br /><br /> 4 = UPDATE <br /><br /> 5 = 削除<br /><br /> 6 = 閉じる<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|サーバーのスコープ内でカーソルを識別する一意の値です。|  
  
## <a name="remarks"></a>解説  
 sp_cursor_list は、接続によってオープンされた現在のサーバー カーソルの一覧を作成し、カーソルのスクロール機能や更新機能など、各カーソルにとってグローバルな属性を示します。 sp_cursor_list によってレポートされるカーソルは次のとおりです。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバーカーソル。  
  
-   ODBC アプリケーションによってオープンされた API サーバー カーソル。この後、カーソルに名前を付けるために、SQLSetCursorName が呼び出されます。  
  
 カーソルから返された結果セットの属性の説明が必要な場合は、sp_describe_cursor_columns を使用します。 カーソルが参照するベース テーブルのレポートが必要な場合は、sp_describe_cursor_tables を使用します。 sp_describe_cursor は sp_cursor_list と同じ情報をレポートしますが、指定されたカーソルに対してのみ報告します。  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定で public ロールに設定されています。  
  
## <a name="examples"></a>例  
 次の例では、グローバル カーソルを開き、`sp_cursor_list` を使用してカーソルの属性をレポートします。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a keyset-driven cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_cursor_list.  
DECLARE @Report CURSOR;  
  
-- Execute sp_cursor_list into the cursor variable.  
EXEC master.dbo.sp_cursor_list @cursor_return = @Report OUTPUT,  
      @cursor_scope = 2;  
  
-- Fetch all the rows from the sp_cursor_list output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_cursor_list.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
