---
description: sp_create_plan_guide (Transact-SQL)
title: sp_create_plan_guide (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide
- sp_create_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide
ms.assetid: 5a8c8040-4f96-4c74-93ab-15bdefd132f0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0e7cc07a0878eefdb6f8c0cdf33cf6e063651afb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539060"
---
# <a name="sp_create_plan_guide-transact-sql"></a>sp_create_plan_guide (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  クエリヒントまたは実際のクエリプランをデータベース内のクエリに関連付けるためのプランガイドを作成します。 プラン ガイドの詳細については、「 [Plan Guides](../../relational-databases/performance/plan-guides.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_create_plan_guide [ @name = ] N'plan_guide_name'  
    , [ @stmt = ] N'statement_text'  
    , [ @type = ] N'{ OBJECT | SQL | TEMPLATE }'  
    , [ @module_or_batch = ]  
      {   
                    N'[ schema_name. ] object_name'  
        | N'batch_text'  
        | NULL  
      }  
    , [ @params = ] { N'@parameter_name data_type [ ,...n ]' | NULL }   
    , [ @hints = ] { N'OPTION ( query_hint [ ,...n ] )'   
                 | N'XML_showplan'  
                 | NULL }  
```  
  
## <a name="arguments"></a>引数  
 [ \@ name =] N '*plan_guide_name*'  
 プランガイドの名前を指定します。 プラン ガイド名は現在のデータベースに対して有効です。 *plan_guide_name* は、 [識別子](../../relational-databases/databases/database-identifiers.md) の規則に従っている必要があり、番号記号 (#) で始めることはできません。 *Plan_guide_name*の最大長は124文字です。  
  
 [ \@ stmt =] N '*statement_text*'  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]プランガイドを作成するステートメントを指定します。 Statement_text に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一致するクエリがクエリオプティマイザーに*statement_text*よって認識されると、 *plan_guide_name*が有効になります。 プランガイドの作成を成功させるには*statement_text* 、 \@ type、 \@ module_or_batch、および params パラメーターで指定されたコンテキストに statement_text が指定されている必要があり \@ ます。  
  
 *statement_text* は、クエリオプティマイザーが、module_or_batch および params で識別されるバッチまたはモジュール内で指定された対応するステートメントと照合できるように指定する必要があり \@ \@ ます。 詳細については、「解説」を参照してください。 *Statement_text*のサイズは、サーバーの使用可能なメモリによってのみ制限されます。  
  
 [ \@ type =] N ' {OBJECT |SQL |テンプレート} '  
 *Statement_text*が表示されるエンティティの種類を指定します。 これにより、一致する *statement_text* のコンテキストが *plan_guide_name*に指定されます。  
  
 OBJECT  
 現在*statement_text*の [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースのストアドプロシージャ、スカラー関数、複数ステートメントのテーブル値関数、または DML トリガーのコンテキストで statement_text が表示されることを示し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
 SQL  
 任意のメカニズムを通じてに送信できるスタンドアロンのステートメントまたはバッチのコンテキストで *statement_text* 表示されることを示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 共通言語ランタイム (CLR) オブジェクト、拡張ストアドプロシージャ、または EXEC N '*sql_string*' を使用して送信されたステートメントは、サーバー上でバッチとして処理されるため、 \@ 型 ' sql ' として識別される必要があり **=** ます。 SQL が指定されている場合、クエリヒントのパラメーター化 {FORCED |SIMPLE} をヒントパラメーターに指定することはできません \@ 。  
  
 テンプレート  
 *Statement_text*に示されている形式にパラメーター化されるクエリに対して、プランガイドが適用されることを示します。 TEMPLATE が指定されている場合は、パラメーター化 {FORCED |SIMPLE} クエリヒントは、hint パラメーターで指定でき \@ ます。 テンプレートプランガイドの詳細については、「 [プランガイドを使用してクエリのパラメーター化の動作を指定](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)する」を参照してください。  
  
 [ \@ module_or_batch =] {N ' [ *schema_name*。 ] *object_name*' |N '*batch_text*' |空白  
 *Statement_text*が表示されるオブジェクトの名前、または*statement_text*が表示されるバッチテキストのいずれかを指定します。 バッチテキストに USE*database* ステートメントを含めることはできません。  
  
 アプリケーションから送信されたバッチと一致するプランガイドについては、 *batch_tex*t をに送信するときと同じ形式の文字文字で指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 この適合を容易にするために内部変換は実行されません。 詳細については、「解説」を参照してください。  
  
 [*schema_name*]*object_name*には、statement_text を [!INCLUDE[tsql](../../includes/tsql-md.md)] 含むストアドプロシージャ、スカラー関数、複数ステートメントのテーブル値関数、または DML トリガーの名前を指定し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 *statement_text* *Schema_name*が指定されていない場合、 *schema_name*は現在のユーザーのスキーマを使用します。 NULL が指定されていて、 \@ type = ' SQL ' の場合、module_or_batch の値 \@ は stmt の値に設定され \@ ます。 \@Type = ' TEMPLATE **\'** の場合、MODULE_OR_BATCH は \@ NULL である必要があります。  
  
 [ \@ params =] {N '* \@ parameter_name data_type* [,*...n* ] ' |空白  
 *Statement_text*に埋め込まれているすべてのパラメーターの定義を指定します。 \@params は、次のいずれかに該当する場合にのみ適用されます。  
  
-   \@「= ' SQL ' または ' TEMPLATE '」と入力します。 ' TEMPLATE ' の場合、params を NULL にすることはでき \@ ません。  
  
-   *statement_text* は sp_executesql を使用して送信され、 \@ params パラメーターの値が指定されているか、または内部でステートメントをパラメーター化し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] た後に送信します。 データベース API (ODBC、OLE DB、ADO.NET など) からのパラメーター化クエリの送信は、sp_executesql または API サーバー カーソル ルーチンの呼び出しとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に示されるため、SQL または TEMPLATE プラン ガイドでも適合させることができます。  
  
 * \@ parameter_name data_type*は、sp_executesql を使用するか、パラメーター化し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] た後に内部で送信されるのとまったく同じ形式で指定する必要があります。 詳細については、「解説」を参照してください。 バッチにパラメーターが含まれていない場合は、NULL を指定する必要があります。 Params のサイズ \@ は、使用可能なサーバーメモリによってのみ制限されます。  
  
 [ \@ ヒント =] {N'OPTION (*query_hint* [,*...n* ]) ' |N '*XML_showplan*' |空白  
 N'OPTION (*query_hint* [,*...n* ])  
 Stmt に一致するクエリにアタッチする OPTION 句を指定し \@ ます。 \@ヒントは、SELECT ステートメントの OPTION 句と構文的に同じである必要があり、任意の有効な一連のクエリヒントを含めることができます。  
  
 N '*XML_showplan*'  
 ヒントとして適用する XML 形式のクエリ プランを指定します。  
  
 XML プラン表示を変数に割り当てることをお勧めします。それ以外の場合は、Showplan で1つの引用符をもう1つの単一引用符で囲んでエスケープする必要があります。 例 E を参照してください。  
  
 NULL  
 クエリの OPTION 句で指定した既存のヒントがクエリに適用されないことを示します。 詳細については、「 [OPTION 句 &#40;transact-sql&#41;](../../t-sql/queries/option-clause-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 sp_create_plan_guide の引数は、表示される順序で指定する必要があります。 **sp_create_plan_guide**のパラメーターに値を指定する場合、パラメーター名はすべて明示的に指定するか、すべて指定しないかのいずれかにする必要があります。 たとえば、 ** \@ name =** が指定されている場合は、 ** \@ stmt =** 、 ** \@ type =** なども指定する必要があります。 同様に、 ** \@ name =** を省略し、パラメーター値だけを指定した場合は、残りのパラメーター名も省略し、値だけを指定する必要があります。 引数の名前は、構文を理解しやすくするための説明目的のものです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、指定したパラメーター名と、その名前が使用されている位置にあるパラメーターの名前が一致しているかどうかは確認されません。  
  
 同一のクエリとバッチまたはモジュールに対し、複数の OBJECT または SQL プラン ガイドを作成できます。 ただし、有効にできるプラン ガイドは常に 1 つだけです。  
  
 \@WITH ENCRYPTION 句を指定するストアドプロシージャ、関数、または DML トリガー、または一時的なを参照する module_or_batch 値に対して、OBJECT 型のプランガイドを作成することはできません。  
  
 有効、無効にする場合のどちらでも、そのプラン ガイドで参照されている関数、ストアド プロシージャ、または DML トリガーを削除または変更しようとすると、エラーが発生します。 プラン ガイドで参照され、トリガーが定義されているテーブルを削除しようとする場合もエラーが発生します。  
  
> [!NOTE]
> プラン ガイドは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。 プラン ガイドはどのエディションでも表示できます。 また、プラン ガイドを含むデータベースは、どのエディションに対してもアタッチできます。 アップグレード済みのバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にデータベースを復元またはアタッチした場合、プラン ガイドはまったく影響を受けません。 サーバーのアップグレードを実行した後、各データベースのプランガイドの魅力を確認する必要があります。  
  
## <a name="plan-guide-matching-requirements"></a>プランガイドの照合要件  
 \@Type = ' SQL ' または type = ' TEMPLATE ' を指定するプランガイドで \@ は、クエリと正常に一致させるために*batch_text*および parameter_name の値* \@ data_type* [,*...n* ] は、アプリケーションによって送信された対応する形式とまったく同じ形式で指定する必要があります。 つまり、バッチ テキストを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンパイラが受信したときとまったく同じように指定する必要があります。 実際のバッチとパラメーターのテキストをキャプチャするには、を使用し [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ます。 詳細については、「 [SQL Server プロファイラー使用したプランガイドの作成とテスト」を](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)参照してください。  
  
 \@Type = ' SQL ' と \@ MODULE_OR_BATCH が NULL に設定されている場合、module_or_batch の値 \@ は stmt の値に設定され \@ ます。これは、 *statement_text*の値は、に送信されるときとまったく同じ形式の文字文字で指定する必要があることを意味し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 この適合を容易にするために内部変換は実行されません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Statement_text*の値が*batch_text*に一致し、 * \@ parameter_name data_type* [,*...n* ]、または \@ type = **\'** OBJECT ' の場合、 *object_name*内の対応するクエリのテキストに対して、次の文字列要素は考慮されません。  
  
-   文字列内の空白文字 (タブ、スペース、キャリッジリターン、またはラインフィード)。  
  
-   コメント ( **--** または **/\*   \*/** )。  
  
-   末尾のセミコロン  
  
 たとえば、は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *statement_text* 文字列を `N'SELECT * FROM T WHERE a = 10'` 次の *batch_text*に一致させることができます。  
  
 ```
 N'SELECT *
 FROM T
 WHERE a = 10' 
 ```
 
 ただし、同じ文字列がこの *batch_text*と一致しません。  
  
 `N'SELECT * FROM T WHERE b = 10'`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最初のクエリ内のキャリッジリターン、改行、および空白文字を無視します。 2 つ目のクエリのシーケンス `WHERE b = 10` は、`WHERE a = 10` とは異なるものと解釈されます。 照合では大文字と小文字が区別されます (データベースの照合順序で大文字と小文字が区別されない場合でも)。ただし、キーワードの場合を除き、大文字小文字は区別されません。 キーワードの省略形は区別されません。 たとえば、キーワード `EXECUTE`、`EXEC`、および `execute` は同じものと解釈されます。  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>プランキャッシュに対するプランガイドの効果  
 モジュールにプラン ガイドを作成すると、そのモジュールのクエリ プランがプラン キャッシュから削除されます。 バッチに OBJECT 型または SQL 型のプラン ガイドを作成すると、同じハッシュ値を持つバッチのクエリ プランが削除されます。 TEMPLATE 型のプラン ガイドを作成すると、単一ステートメントのバッチがデータベース内のプラン キャッシュからすべて削除されます。  
  
## <a name="permissions"></a>アクセス許可  
 OBJECT 型のプランガイドを作成するには、 `ALTER` 参照先オブジェクトに対する権限が必要です。 SQL または TEMPLATE 型のプランガイドを作成するには、 `ALTER` 現在のデータベースに対する権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-plan-guide-of-type-object-for-a-query-in-a-stored-procedure"></a>A. ストアドプロシージャ内のクエリに対して OBJECT 型のプランガイドを作成する  
 次の例では、アプリケーションベースのストアド プロシージャのコンテキストで実行されるクエリに適合するプラン ガイドを作成し、`OPTIMIZE FOR` ヒントをクエリに適用します。  
  
 ストアドプロシージャを次に示します。  
  
```sql  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t   
        ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country_region;  
END  
GO  
```  
  
 ストアド プロシージャのクエリに対して作成されるプラン ガイドは次のようになります。  
  
```sql  
EXEC sp_create_plan_guide   
    @name =  N'Guide1',  
    @stmt = N'SELECT *  
              FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.Customer AS c   
                 ON h.CustomerID = c.CustomerID  
              INNER JOIN Sales.SalesTerritory AS t   
                 ON c.TerritoryID = t.TerritoryID  
              WHERE t.CountryRegionCode = @Country_region',  
    @type = N'OBJECT',  
    @module_or_batch = N'Sales.GetSalesOrderByCountry',  
    @params = NULL,  
    @hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
### <a name="b-creating-a-plan-guide-of-type-sql-for-a-stand-alone-query"></a>B. スタンドアロン クエリに対する SQL タイプのプラン ガイドを作成する  
 次の例では、sp_executesql システム ストアド プロシージャを使用するアプリケーションで送信されるバッチ内のクエリに適合するプラン ガイドを作成します。  
  
 バッチは、次のようになります。  
  
```sql  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 このクエリに対して並列実行プランが生成されないようにするには、次のプラン ガイドを作成します。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT TOP 1 *   
              FROM Sales.SalesOrderHeader   
              ORDER BY OrderDate DESC',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (MAXDOP 1)';  
```  
  
### <a name="c-creating-a-plan-guide-of-type-template-for-the-parameterized-form-of-a-query"></a>C. パラメーター化された形式のクエリ用に TEMPLATE 型のプランガイドを作成する  
 次の例では、指定されたフォームにパラメーター化されるクエリに適合するプラン ガイドを作成し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対してクエリのパラメーター化を強制的に実行させます。 次の 2 つのクエリは構文的には同じですが、定数リテラル値のみが異なります。  
  
```sql  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 パラメーター化形式のクエリに対するプラン ガイドは次のようになります。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 この例では、 `@stmt` パラメーターの値は、パラメーター化形式のクエリになっています。 この値を取得して sp_create_plan_guide で使用できるようにするには、 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) システム ストアド プロシージャを使用するのが唯一信頼できる方法です。 次のスクリプトを使用すると、パラメーター化クエリを取得してそのクエリに対してプラン ガイドを作成することができます。  
  
```sql  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  sp_get_query_template に渡される `@stmt` パラメーターの定数リテラルの値は、リテラルを置き換えるパラメーターで選択されるデータ型に影響する場合があります。 この値は、プラン ガイドの適合にも影響します。 場合によっては、異なるパラメーター値範囲に対応する複数のプラン ガイドを作成する必要があります。  
  
### <a name="d-creating-a-plan-guide-on-a-query-submitted-by-using-an-api-cursor-request"></a>D. API カーソル要求を使用して送信されたクエリに対してプランガイドを作成する  
 プランガイドは、API サーバーカーソルルーチンから送信されるクエリと一致することができます。 これらのルーチンには、sp_cursorprepare、sp_cursorprepexec、および sp_cursoropen があります。 ADO、OLE DB、および ODBC API を使用するアプリケーションは、API サーバー カーソルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と頻繁に対話します。 RPC:Starting プロファイラー トレース イベントを表示して、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレース内の API サーバー カーソル ルーチンの呼び出しを参照できます。  
  
 たとえば、次のデータが、プラン ガイドに合わせて調整するクエリの RPC:Starting プロファイル トレース イベントに示されているものとします。  
  
```sql  
DECLARE @p1 int;  
SET @p1=-1;  
DECLARE @p2 int;  
SET @p2=0;  
DECLARE @p5 int;  
SET @p5=4104;  
DECLARE @p6 int;  
SET @p6=8193;  
DECLARE @p7 int;  
SET @p7=0;  
EXEC sp_cursorprepexec @p1 output,@p2 output,N'@P1 varchar(255),@P2 varchar(255)',N'SELECT * FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID WHERE h.OrderDate BETWEEN @P1 AND @P2',@p5 OUTPUT,@p6 OUTPUT,@p7 OUTPUT,'20040101','20050101'  
SELECT @p1, @p2, @p5, @p6, @p7;  
```  
  
 このデータを見ると、`SELECT` の呼び出しの `sp_cursorprepexec` クエリに対するプランでマージ結合を使用していることがわかりますが、ハッシュ結合を使用するとします。 を使用して送信されたクエリ `sp_cursorprepexec` は、クエリ文字列とパラメーター文字列の両方を含むパラメーター化されます。 `sp_cursorprepexec` の呼び出しで、表示されているとおり完全に同じであるクエリ文字列とパラメーター文字列を使用して、次のプラン ガイドを作成し、プランの選択を変更できます。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'APICursorGuide',  
    @stmt = N'SELECT * FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.SalesOrderDetail AS d   
                ON h.SalesOrderID = d.SalesOrderID   
              WHERE h.OrderDate BETWEEN @P1 AND @P2',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = N'@P1 varchar(255),@P2 varchar(255)',  
    @hints = N'OPTION(HASH JOIN)';  
```  
  
 アプリケーションによるこのクエリの実行は、このプランガイドによって影響を受けます。ハッシュ結合はクエリの処理に使用されます。  
  
### <a name="e-creating-a-plan-guide-by-obtaining-the-xml-showplan-from-a-cached-plan"></a>E. キャッシュされたプランから XML プラン表示を取得してプランガイドを作成する  
 次の例では、単純なアドホック SQL ステートメントのプラン ガイドを作成します。 このステートメントの目的のクエリ プランは、クエリの XML プラン表示を `@hints` パラメーターで直接指定することにより、プラン ガイドで提供されます。 最初に SQL ステートメントを実行して、プラン キャッシュ内にプランを生成します。 この例では、生成されたプランが目的のプランであり、追加のクエリ チューニングが不要であると想定しています。 クエリの XML プラン表示は、 `sys.dm_exec_query_stats`、 `sys.dm_exec_sql_text`、および `sys.dm_exec_text_query_plan` の各動的管理ビューをクエリすることにより取得され、 `@xml_showplan` 変数に割り当てられます。 次に `@xml_showplan` 変数が、 `sp_create_plan_guide` パラメーターで `@hints` ステートメントに渡されます。 または、 [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) ストアド プロシージャを使用して、プラン キャッシュ内のクエリ プランからプラン ガイドを作成することもできます。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints =@xml_showplan;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [プランガイド](../../relational-databases/performance/plan-guides.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_get_query_template &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md)  
  
  
