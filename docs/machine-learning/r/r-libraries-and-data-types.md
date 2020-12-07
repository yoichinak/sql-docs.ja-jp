---
title: R と SQL のデータ型を変換する
description: データ サイエンスおよび機械学習のソリューションで、R と SQL Server の間の暗黙的および明示的なデータ型の変換について確認します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d10d65f8be4ff8e53cbfad795f1e515a22eada71
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92098861"
---
# <a name="data-type-mappings-between-r-and-sql-server"></a>R と SQL Server の間のデータ型マッピング
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

この記事では、SQL Server Machine Learning Services の R 統合機能を使用する場合にサポートされるデータ型および実行されるデータ型変換の一覧を示します。

## <a name="base-r-version"></a>基本の R のバージョン

SQL Server 2016 R Services および SQL Server Machine Learning Services (R 付属) は、Microsoft R Open の特定のリリースに合わせられています。 たとえば、最新リリースの SQL Server 2019 Machine Learning Services は、Microsoft R Open 3.5.2 に基づいて構築されています。

SQL Server の特定のインスタンスに関連付けられている R のバージョンを表示するには、SQL インスタンスで **RGui** を開きます。 たとえば、SQL Server 2019 での既定のインスタンスのパスは、`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe` となります。

このツールでは、基本の R とその他のライブラリが読み込まれます。 パッケージのバージョン情報は、セッションの開始時に読み込まれる各パッケージの通知に記載されています。

## <a name="r-and-sql-data-types"></a>R と SQL のデータ型

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は数十種類のデータ型をサポートしていますが、R がサポートするスカラー データ型は限られています (数値、整数、複素数、論理、文字、日時および未処理)。 その結果、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータを R スクリプト内で使用する場合、データは互換性のあるデータ型に暗黙的に変換される可能性があります。 ただし、多くの場合は正確な変換を自動的に実行することはできず、"未処理の SQL データ型" などのエラーが返されます。

このセクションでは、提供されている暗黙的な変換の一覧を示し、サポートされていないデータ型についても一覧表示します。 R と SQL Server の間でデータ型をマッピングするための、いくつかのガイダンスが用意されています。

## <a name="implicit-data-type-conversions"></a>暗黙的なデータ型の変換

次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータを R スクリプトで使用する場合と、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に返された場合のデータ型と値の変化の一覧です。

| SQL 型                         | R クラス     | RESULT SET の型    | 説明            |
|----------------------------------|-------------|--------------------|---------------------|
| **bigint**                       | `numeric`   | **float**          | `sp_execute_external_script` で R スクリプトを実行すると、bigint データ型が入力データとして許可されます。 ただし、それらは R の数値型に変換されるため、きわめて大きい値や小数点値を持つ値では精度が失われます。 R では最大 53 ビットの整数がサポートされるだけであり、その後は精度が失われ始めます。                                                                                         |
| **binary(n)**<br /> n <= 8000    | `raw`       | **varbinary(max)** | 入力パラメーターと出力にのみ使用できます。 |
| **bit**                          | `logical`   | **bit**            |                     |
| **char(n)**<br /> n <= 8000      | `character` | **varchar(max)**   | 入力データ フレーム (input_data_1) は、*stringsAsFactors* パラメーターを明示的に設定することなく作成されるため、列の型は R の *default.stringsAsFactors()* に依存します                                                                                                                                                                                                                                           |
| **datetime**                     | `POSIXct`   | **datetime**       | GMT として表現されます  |
| **date**                         | `POSIXct`   | **datetime**       | GMT として表現されます  |
| **decimal(p,s)**                 | `numeric`   | **float**          | `sp_execute_external_script` で R スクリプトを実行すると、decimal データ型が入力データとして許可されます。 ただし、それらは R の数値型に変換されるため、きわめて大きい値や小数点値を持つ値では精度が失われます。 R スクリプトによる `sp_execute_external_script` では、このデータ型の範囲全体はサポートされておらず、小数部分がある場合は特に、末尾の数桁が変更される場合があります。 |
| **float**                        | `numeric`   | **float**          |                     |
| **int**                          | `integer`   | **int**            |                     |
| **money**                        | `numeric`   | **float**          | `sp_execute_external_script` で R スクリプトを実行すると、money データ型が入力データとして許可されます。 ただし、それらは R の数値型に変換されるため、きわめて大きい値や小数点値を持つ値では精度が失われます。 セント値が不正確になり、次のような警告が発行されることがあります。"*警告: セント値を正確に表すことができません*"。                                               |
| **numeric(p,s)**                 | `numeric`   | **float**          | `sp_execute_external_script` で R スクリプトを実行すると、numeric データ型が入力データとして許可されます。 ただし、それらは R の数値型に変換されるため、きわめて大きい値や小数点値を持つ値では精度が失われます。 R スクリプトによる `sp_execute_external_script` では、このデータ型の範囲全体はサポートされておらず、小数部分がある場合は特に、末尾の数桁が変更される場合があります。 |
| **real**                         | `numeric`   | **float**          |                     |
| **smalldatetime**                | `POSIXct`   | **datetime**       | GMT として表現されます  |
| **smallint**                     | `integer`   | **int**            |                     |
| **smallmoney**                   | `numeric`   | **float**          |                     |
| **tinyint**                      | `integer`   | **int**            |                     |
| **uniqueidentifier**             | `character` | **varchar(max)**   |                     |
| **varbinary(n)**<br /> n <= 8000 | `raw`       | **varbinary(max)** | 入力パラメーターと出力にのみ使用できます。 |
| **varbinary(max)**               | `raw`       | **varbinary(max)** | 入力パラメーターと出力にのみ使用できます。 |
| **varchar(n)**<br /> n <= 8000   | `character` | **varchar(max)**   | 入力データ フレーム (input_data_1) は、*stringsAsFactors* パラメーターを明示的に設定することなく作成されるため、列の型は R の *default.stringsAsFactors()* に依存します                                                                                                                                                                                                                                           |

## <a name="data-types-not-supported-by-r"></a>R でサポートされていないデータ型

[SQL Server 型システム](../../t-sql/data-types/data-types-transact-sql.md)でサポートされるデータ型のカテゴリのうち、次の型は R コードに渡されるときに問題が発生する可能性があります。

+ SQL 型システムに関する記事の**その他**のセクションに示されているデータ型: **カーソル**、**タイムスタンプ**、**hierarchyid**、**一意識別子**、**sql_variant**、**xml**、**テーブル**
+ すべての空間型
+ **image**

## <a name="data-types-that-might-convert-poorly"></a>適切に変換できない可能性があるデータ型

+ **datetimeoffset** 以外のほとんどの datetime 型は機能します。
+ ほとんどの数値データ型はサポートされますが、**money** と **smallmoney** については、変換が失敗することがあります。
+ **varchar** はサポートされますが、SQL Server では原則として Unicode を使用するため、可能な場合には **nvarchar** とその他の Unicode テキスト データ型の使用をお勧めします。
+ RevoScaleR ライブラリの先頭に rx が付く関数は、SQL バイナリ データ型 (**バイナリ**と **varbinary**) を処理できますが、ほとんどのシナリオでは、これらの型に対して特別な処理が必要になります。 R コードの大部分は、バイナリ列で動作しません。

  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型について詳しくは、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」をご覧ください

## <a name="changes-in-data-types-between-sql-server-versions"></a>SQL Server バージョン間でのデータ型の変更

Microsoft SQL Server 2016 以降では、データ型変換とその他のいくつかの操作の改善が行われています。 これらの改善のほとんどでは、浮動小数点型を処理する場合の精度が向上し、従来の**日時**型に対する操作が若干変更されています。

これらの改善は、データベース互換性レベル 130 またはそれ以降を使用する場合に既定ですべて使用可能になります。 ただし、別の互換性レベルを使用しているか、以前のバージョンを使用してデータベースに接続する場合は、数値またはその他の結果の精度が異なる可能性があります。 

詳しくは、「[SQL Server 2016 improvements in handling some data types and uncommon operations](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon-)」(いくつかのデータ型と一般的でない操作を処理するときの SQL Server の 2016 の機能強化) をご覧ください。
 

## <a name="verify-r-and-sql-data-schemas-in-advance"></a>R と SQL のデータ スキーマを事前に確認する

一般的に、特定のデータ型またはデータ構造を R で使用する方法についてわからない点がある場合は、  `str()` 関数を使用して内部構造と R オブジェクトの種類を取得してください。 この関数の結果は R コンソールに出力され、 **の** [メッセージ] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]タブのクエリ結果で確認することもできます。 

R コードで使用するためのデータをデータベースから取得する場合、R で使用できない列、ならびに GUID (一意識別子)、監査に使用されるタイム スタンプやその他の列、または ETL プロセスによって作成された系列情報などの分析に使用できない列を、常に除外する必要があります。 

不要な列を含めると、カーディナリティの大きい列が係数として使用されている場合には特に、R コードのパフォーマンスが大幅に低下することがあります。 そのため、SQL Server システム ストアド プロシージャと情報ビューを使用して、事前に特定のテーブルのデータ型を取得し、互換性のない列を排除または変換することをお勧めします。 詳しくは、「[システム情報スキーマ ビュー (TRANSACT-SQL)](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)」をご覧ください

特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型が R でサポートされておらず、R スクリプトでデータの列を使用する必要がある場合、R スクリプトでデータを使用する前に、[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 関数を使用してデータ型変換が意図したとおりに実行されることを確認することをお勧めします。  

> [!WARNING]
> データの移動中に **rxDataStep** を使用して互換性のない列を削除する場合、引数 "_varsToKeep_" と "_varsToDrop_" は **RxSqlServerData** データ ソース型としてサポートされないことにご注意ください。


## <a name="examples"></a>例

### <a name="example-1-implicit-conversion"></a>例 1:暗黙的な変換

次の例では、SQL Server と R の間を往復するときにデータを変換する方法を示しています。

このクエリは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルから一連の値を取得し、ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して、R ランタイムを使用して値を出力します。

```sql
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```

**結果**

|行 \#|C1|C2|C3|C4|
|-|-|-|-|-|
|1|1|こんにちは|6e225611-4b58-4995-a0a5-554d19012ef1|4|
|2|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|

R で `str` 関数を使用すると、出力データのスキーマが取得されます。 この関数からは、次の情報が返されます。

```output
'data.frame':2 obs. of  4 variables:
 $ c1: int  1 -11
 $ c2: Factor w/ 2 levels "Hello","world": 1 2
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1
 $ cR: num  4 2
```

その結果から、次のデータ型の変換がこのクエリの一部として暗黙的に実行されたことがわかります。

+ **列 C1**。 この列は **ssNoversion** では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、R では `integer` 、出力結果セットでは **ssNoversion** と表現されます。  
  
  型変換は実行されていません。  
  
+ **列 C2**。 この列は **ssNoversion** では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、R では `factor` 、出力結果セットでは **varchar(max)** と表現されます。  
  
  出力の変化に注目してください。文字列の長さにかかわらず、R の文字列 (係数または通常の文字列) は **varchar(max)** と表現されます。  
  
+ **列 C3**。  この列は **ssNoversion** では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、R では `character` 、出力結果セットでは **varchar(max)** と表現されます。
  
  発生したデータ型の変換に注目してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **ssNoversion** をサポートしていますが、R はサポートしていません。そのため、識別子は文字列として表されます。
  
+ **列 C4**。 この列には、元のデータには存在しない、R スクリプトで生成された値が含まれます。


## <a name="example-2-dynamic-column-selection-using-r"></a>例 2:R を使用した動的な列の選択

次の例では、R コードを使用して無効な列の型をチェックする方法を示します。 指定されたテーブルのスキーマを SQL Server システム ビューを使用して取得し、指定された無効な型を持つ列をすべて削除します。

```R
connStr <- "Server=.;Database=TestDB;Trusted_Connection=Yes"
data <- RxSqlServerData(connectionString = connStr, sqlQuery = "SELECT COLUMN_NAME FROM TestDB.INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = N'testdata' AND DATA_TYPE <> 'image';")
columns <- rxImport(data)
columnList <- do.call(paste, c(as.list(columns$COLUMN_NAME), sep = ","))
sqlQuery <- paste("SELECT", columnList, "FROM testdata")
```

## <a name="see-also"></a>関連項目

+ [Python と SQL Server の間のデータ型マッピング](../python/python-libraries-and-data-types.md)
