---
description: sp_describe_first_result_set (Transact-SQL)
title: sp_describe_first_result_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9cc2e3bef68a6900d5b9735ef3a5f8a050a34361
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548125"
---
# <a name="sp_describe_first_result_set-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  バッチの最初の使用可能な結果セットのメタデータを返し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 バッチが結果を返さない場合は、空の結果セットを返します。 では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 静的分析を実行することによって実行される最初のクエリのメタデータをが判別できない場合に、エラーが発生します。 動的管理ビューの [dm_exec_describe_first_result_set &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) は同じ情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>引数  
`[ \@tsql = ] 'Transact-SQL_batch'` 1つ以上の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント。 *Transact-sql SQL_batch* は **nvarchar (***n***)** または **nvarchar (max)** です。  
  
`[ \@params = ] N'parameters'`\@params は、バッチのパラメーターの宣言文字列を提供し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。これは sp_executesql に似ています。 パラメーターには、 **nvarchar (n)** または **nvarchar (max)** を指定できます。  
  
 _Batch に埋め込まれているすべてのパラメーターの定義を含む1つの文字列を指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*します。 この文字列は Unicode 定数または Unicode 変数にする必要があります。 各パラメーター定義は、パラメーター名とデータ型で構成されます。 *n* は、追加のパラメーター定義を示すプレースホルダーです。 ステートメントで指定するすべてのパラメーターは、params で定義する必要があり \@ ます。 ステートメント [!INCLUDE[tsql](../../includes/tsql-md.md)] 内のステートメントまたはバッチにパラメーターが含まれていない場合、 \@ params は必要ありません。 このパラメーターの既定値は NULL です。  
  
`[ \@browse_information_mode = ] tinyint` 追加のキー列とソーステーブル情報を返すかどうかを指定します。 1に設定すると、各クエリはクエリに FOR BROWSE オプションが含まれているかのように分析されます。 追加のキー列とソース テーブル情報が返されます。  
  
-   0に設定すると、情報は返されません。  
  
-   1に設定すると、各クエリはクエリに FOR BROWSE オプションが含まれているかのように分析されます。 ベースのテーブル名がソース列情報として返されます。  
  
-   2に設定すると、各クエリは、カーソルの準備または実行時に使用されるかのように分析されます。 ビュー名がソース列情報として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **sp_describe_first_result_set** は、成功した場合に常に0の状態を返します。 プロシージャがエラーをスローし、プロシージャが RPC として呼び出された場合、返される状態は、dm_exec_describe_first_result_set の error_type 列に記述されているエラーの種類によって設定されます。 プロシージャがから呼び出された場合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 、エラーが発生した場合でも、戻り値は常に0になります。  
  
## <a name="result-sets"></a>結果セット  
 この共通メタデータは、結果のメタデータの各列に対する 1 行の結果セットとして返されます。 各行には、列の種類と NULL 値の許容属性が次のセクションに示す形式で記述されます。 各コントロールのパスに最初のステートメントが存在しない場合は、0 行の結果セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit NOT NULL**|列が参照情報のために追加された余分な列であり、実際には結果セットに表示されないことを示します。|  
|**column_ordinal**|**int NOT NULL**|結果セット内の列の位置を示す序数を格納します。 最初の列の位置は1として指定されます。|  
|**name**|**sysname NULL**|列の名前を確認できる場合は、その名前を格納します。 それ以外の場合、NULL が含まれます。|  
|**is_nullable**|**bit NOT NULL**|列で Null が許容される場合は値1が格納され、列が null を許容しない場合は0、null を許容するかどうかを判断できない場合は1が格納されます。|  
|**system_type_id**|**int NOT NULL**|に指定されている列のデータ型の system_type_id が含まれています。型です。 CLR 型の場合は、system_type_name 列が NULL を返しても、この列は値 240 を返します。|  
|**system_type_name**|**nvarchar (256) NULL**|列のデータ型に指定されている名前と引数 (長さ、有効桁数、小数点以下桁数など) を格納します。 データ型がユーザー定義の別名型の場合は、基になるシステム型がここで指定されます。 CLR ユーザー定義型の場合は、この列には NULL が返されます。|  
|**max_length**|**smallint NOT NULL**|列の最大長 (バイト単位) です。<br /><br /> -1 = 列のデータ型は **varchar (max)**,、 **nvarchar (max)**,、 **varbinary (max)**,、または **xml**です。<br /><br /> **テキスト**列の場合、 **max_length**値は16か**sp_tableoption ' text in row '** によって設定された値になります。|  
|**有効桁数 (precision)**|**tinyint NOT NULL**|数値ベースの場合は、列の有効桁数です。 それ以外の場合は 0 を返します。|  
|**scale**|**tinyint NOT NULL**|数値ベースの場合は、列の小数点以下桁数です。 それ以外の場合は 0 を返します。|  
|**collation_name**|**sysname NULL**|文字ベースの場合は、列の照合順序の名前です。 それ以外の場合は NULL を返します。|  
|**user_type_id**|**int NULL**|CLR 型と別名型の場合、sys.types で指定された列のデータ型の user_type_id を格納します。 それ以外の場合は NULL です。|  
|**user_type_database**|**sysname NULL**|CLR 型と別名型の場合、その型が定義されたデータベースの名前を格納します。 それ以外の場合は NULL です。|  
|**user_type_schema**|**sysname NULL**|CLR 型と別名型の場合、その型が定義されたスキーマの名前を格納します。 それ以外の場合は NULL です。|  
|**user_type_name**|**sysname NULL**|CLR 型と別名型の場合、その型の名前を格納します。 それ以外の場合は NULL です。|  
|**assembly_qualified_type_name**|**nvarchar (4000)**|CLR 型の場合、その型を定義するアセンブリの名前とクラスを返します。 それ以外の場合は NULL です。|  
|**xml_collection_id**|**int NULL**|sys.columns で指定された列のデータ型の xml_collection_id を格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**xml_collection_database**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションが定義されているデータベースを格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**xml_collection_schema**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションが定義されているスキーマを格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**xml_collection_name**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションの名前を格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**is_xml_document**|**bit NOT NULL**|返されたデータ型が XML で、その型が XML フラグメントではなく完全な XML ドキュメント (ルート ノードを含む) であると保証される場合、1 を返します。 それ以外の場合は 0 を返します。|  
|**is_case_sensitive**|**bit NOT NULL**|列が大文字と小文字を区別する文字列型の場合は1、それ以外の場合は0を返します。|  
|**is_fixed_length_clr_type**|**bit NOT NULL**|列が固定長の CLR 型の場合は1、それ以外の場合は0を返します。|  
|**source_server**|**sysname**|この結果内の列によって返された元のサーバーの名前です (リモート サーバーから発生する場合)。 名前は、sys. サーバーに表示されるときに指定されます。 この列がローカル サーバー上で発生した場合、または元のサーバーを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_database**|**sysname**|この結果内の列によって返された元のデータベースの名前です。 データベースを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_schema**|**sysname**|この結果内の列によって返された元のスキーマの名前です。 スキーマを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_table**|**sysname**|この結果内の列によって返された元のテーブルの名前です。 テーブルを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_column**|**sysname**|結果列から返された元の列の名前です。 列を特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**is_identity_column**|**ビット NULL**|この列が ID 列の場合は 1、それ以外の場合は 0 を返します。 ID 列であることを確認できない場合は NULL を返します。|  
|**is_part_of_unique_key**|**ビット NULL**|この列が一意インデックス (一意制約と主キー制約を含む) の一部である場合は 1、それ以外の場合は 0 を返します。 一意インデックスの一部であることを確認できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**is_updateable**|**ビット NULL**|この列が更新可能である場合は 1、それ以外の場合は 0 を返します。 更新可能であることを確認できない場合は NULL を返します。|  
|**is_computed_column**|**ビット NULL**|この列が計算列の場合は 1、それ以外の場合は 0 を返します。 計算列であることを確認できない場合は NULL を返します。|  
|**is_sparse_column_set**|**ビット NULL**|この列がスパース列の場合は 1、それ以外の場合は 0 を返します。 列がスパース列セットの一部であることを判断できない場合は NULL を返します。|  
|**ordinal_in_order_by_list**|**smallint NULL**|ORDER BY リストにおけるこの列の位置。 列が ORDER BY リストに表示されない場合、または ORDER BY リストを一意に特定できない場合は、NULL を返します。|  
|**order_by_list_length**|**smallint NULL**|ORDER BY リストの長さを返します。 ORDER BY リストがない場合、または ORDER BY リストを一意に特定できない場合は NULL を返します。 この値は sp_describe_first_result_set によって返されるすべての行で同じであることに注意して **ください。**|  
|**order_by_is_descending**|**smallint NULL**|ordinal_in_order_by_list が NULL でない場合、**order_by_is_descending** 列には、この列の ORDER BY 句の方向がレポートされます。 それ以外の場合は、NULL が報告されます。|  
|**tds_type_id**|**int NOT NULL**|内部使用です。|  
|**tds_length**|**int NOT NULL**|内部使用です。|  
|**tds_collation_id**|**int NULL**|内部使用です。|  
|**tds_collation_sort_id**|**tinyint NULL**|内部使用です。|  
  
## <a name="remarks"></a>解説  
 **sp_describe_first_result_set** は、プロシージャが (仮定の) バッチ a に対して最初の結果セットのメタデータを返す場合に、そのバッチ (a) が後で実行されると、バッチによって (1) 最適化時のエラーが発生することを保証します。 (2) 実行時エラーが発生します。 (3) は結果セットを返しません。または、(4) **sp_describe_first_result_set**によって記述されたものと同じメタデータを持つ最初の結果セットを返します。  
  
 名前、NULL 値の許容属性、およびデータ型が異なる可能性があります。 **Sp_describe_first_result_set**が空の結果セットを返す場合、バッチ実行で結果セットが返されないという保証があります。  
  
 この保証は、サーバーに関連するスキーマの変更がないことを前提としています。 サーバー上での関連するスキーマ変更には、 **sp_describe_first_result_set** が呼び出されてから、バッチ B によって行われたスキーマの変更を含め、実行時に結果セットが返されるまでの間のバッチ a に一時テーブルまたはテーブル変数を作成することは含まれません。  
  
 **sp_describe_first_result_set** は、次のいずれかの場合にエラーを返します。  
  
-   入力 \@ tsql が有効なバッチではない場合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 有効性は、バッチの解析と分析によって決まり [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 バッチが有効であるかどうかを判断するときに、クエリの最適化中または実行中のバッチによって発生したエラーは考慮されません [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
-   \@Params が NULL ではなく、パラメーターに対して構文的に有効な宣言文字列ではない文字列が含まれている場合、またはパラメーターに複数回宣言する文字列が含まれている場合。  
  
-   入力バッチが、 [!INCLUDE[tsql](../../includes/tsql-md.md)] params で宣言されたパラメーターと同じ名前のローカル変数を宣言している場合 \@ 。  
  
-   ステートメントで一時テーブルを使用する場合はです。  
  
-   クエリには、パーマネントテーブルの作成が含まれ、その後クエリが実行されます。  
  
 他のすべてのチェックが成功した場合は、入力バッチ内のすべての制御フローパスが考慮されます。 この操作では、すべての制御フローステートメントが考慮される必要があります (GOTO、IF/ELSE、WHILE、および [!INCLUDE[tsql](../../includes/tsql-md.md)] TRY/CATCH ブロック) に加えて、 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXEC ステートメントによって入力バッチから呼び出されたプロシージャ、動的バッチ、またはトリガー、ddl トリガーを起動する ddl ステートメント、または外部キー制約の連鎖アクションによって変更された対象テーブルまたはテーブルでトリガーが起動される DML ステートメント。 制御パスの多くが考えられる場合、ある時点でアルゴリズムは停止します。  
  
 制御フローパスごとに、結果セットを返す最初のステートメント (存在する場合) が **sp_describe_first_result_set**によって決定されます。  
  
 バッチ内で使用可能な最初のステートメントが複数見つかった場合、その結果は、列数、列名、null 値の許容属性、およびデータ型によって異なる場合があります。 これらの違いを処理する方法の詳細について、ここに記載します。  
  
-   列の数が異なる場合は、エラーがスローされ、結果は返されません。  
  
-   列名が異なる場合、返される列名は NULL に設定されます。  
  
-   Null 値の許容は異なり、null 値が許容される場合は Null を許容します。  
  
-   データ型が異なる場合は、次の場合を除き、エラーがスローされ、結果は返されません。  
  
    -   varchar ( **a)** から**varchar (a ')** への ' >。  
  
    -   varchar **(a)** から**varchar (max)**  
  
    -   **nvarchar (a)** から **nvarchar (a ')** への ' >。  
  
    -   nvarchar **(a)** から**nvarchar (max)**  
  
    -   **varbinary (a)** から **varbinary (a ')** の場合、' > a です。  
  
    -   varbinary **(a)** から**varbinary (max)**  
  
 **sp_describe_first_result_set** は間接再帰をサポートしていません。  
  
## <a name="permissions"></a>アクセス許可  
 Tsql 引数を実行する権限が必要です \@ 。  
  
## <a name="examples"></a>例  
  
### <a name="typical-examples"></a>一般的な例  
  
#### <a name="a-simple-example"></a>A. 簡単な例  
 次の例では、1つのクエリから返される結果セットについて説明します。  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 次の例は、パラメーターを含む1つのクエリから返される結果セットを示しています。  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>B. ブラウズ モードの使用例  
 次の 3 つの例では、異なるブラウズ情報モード間の主要な違いを示します。 クエリ結果には、関係する列だけが含まれています。  
  
 0を使用して、情報が返されないことを示す例。  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 1を使用した例では、クエリに FOR BROWSE オプションが含まれているかのように情報が返されることを示しています。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 2を使用した例では、カーソルを準備しているかのように分析されています。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>問題の例  
 以下の例では、すべて 2 つのテーブルを使用します。 次のステートメントを実行して、これらのテーブルを作成します。  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>列の数の違いによるエラー  
 この例では、考えられる最初の結果セットの列数が異なります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>データ型の違いによるエラー  
 考えられる最初の結果セットの間で、列の型が異なります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 結果: エラー、型の不一致 (**int** と **smallint**)。  
  
#### <a name="column-name-cannot-be-determined"></a>列名を特定できません  
 最初の結果セットの列は、同じ可変長型、null 値の許容属性、および列名の長さによって異なります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 結果: \<Unknown Column Name> **varchar (20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>別名を使用して列名を強制的に同一にする  
 前の例と同じですが、列の別名を使用して列名を同じにしています。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 結果: b **varchar (20) NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>列の型を一致させることができないためエラーが発生しました  
 列の型が、考えられる最初の結果セットと異なります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 結果: エラー、型の不一致 (**varchar (10)** 、および **nvarchar (10)**)。  
  
#### <a name="result-set-can-return-an-error"></a>結果セットがエラーを返す可能性があります  
 最初の結果セットは、エラーまたは結果セットです。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 結果: **Intnull**  
  
#### <a name="some-code-paths-return-no-results"></a>一部のコードパスが結果を返さない  
 最初の結果セットが null または結果セットです。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 結果: **Intnull**  
  
#### <a name="result-from-dynamic-sql"></a>動的 SQL からの結果  
 最初の結果セットは、リテラル文字列であるため検出可能な動的 SQL です。  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 結果: **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>動的 SQL からの結果の失敗  
 動的 SQL のため、最初の結果セットが未定義となります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 結果: Error。 動的 SQL のため、結果を検出できません。  
  
#### <a name="result-set-specified-by-user"></a>ユーザー指定の結果セット  
 最初の結果セットがユーザーにより手動で指定されています。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 結果: Column1 **BIGINT NOT NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>あいまいな結果セットによるエラー  
 この例では、user1 という名前の別のユーザーが既定のスキーマ s1 に t1 という名前のテーブルを持ち、列 ( **INT NOT NULL**) を使用していると仮定しています。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 結果: Error。 t1 は、dbo. t1 または s1. t1 で、それぞれに異なる数の列があります。  
  
#### <a name="result-even-with-ambiguous-result-set"></a>あいまいな結果セットがあっても結果  
 前の例と同じ仮定を使用します。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 Result: dbo. t1. a と s1. t1 の両方の型が**int**で、null 値の許容が異なるため、 **int が NULL**になります。  
  
## <a name="see-also"></a>参照  
 [sp_describe_undeclared_parameters &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [dm_exec_describe_first_result_set &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [dm_exec_describe_first_result_set_for_object &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
