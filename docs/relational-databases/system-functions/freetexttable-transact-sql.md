---
description: FREETEXTTABLE (Transact-SQL)
title: FREETEXTTABLE (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f44a757695d067f518de22f9d3bc59af455a67c
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753774"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  は、SELECT ステートメントの [from 句](../../t-sql/queries/from-transact-sql.md) で使用される関数で、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文字ベースのデータ型を含むフルテキストインデックス列に対してフルテキスト検索を実行します。 この関数は、指定された *freetext_string*内のテキストの正確な表現だけでなく、意味に一致する値を含む列について、0行、1行、または複数の行から成るテーブルを返します。 FREETEXTTABLE は、通常のテーブル名のように参照されます。  
  
 FREETEXTTABLE は、 [FREETEXT &#40;transact-sql&#41;](../../t-sql/queries/freetext-transact-sql.md)と同じ種類の一致に便利です。  
  
 FREETEXTTABLE を使用するクエリでは、各行の関連順位値 (RANK) とフルテキストキー (キー) が返されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているフルテキスト検索の形式については、「[フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)」を参照してください。  
  
(https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>引数  
 *テーブル*  
 フルテキストクエリ用にマークされているテーブルの名前を指定します。 *テーブル* または *ビュー*には、1、2、または3つの要素で構成されるデータベースオブジェクト名を指定できます。 ビューに対してクエリを実行する場合は、フルテキスト インデックスが作成されたベース テーブルを 1 つだけ指定できます。  
  
 *テーブル* にサーバー名を指定することはできません。また、リンクサーバーに対するクエリでは使用できません。  
  
 *column_name*  
 FROM 句で指定したテーブルのフルテキスト インデックス付きの列の名前を指定します。 列には、**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary**、**varbinary(max)** のいずれかの型を指定できます。  
  
 *column_list*  
 コンマ区切りで複数の列を指定できます。 *column_list* は、かっこで囲む必要があります。 *language_term* を指定しない場合、*column_list* で指定するすべての列の言語は同じにする必要があります。  
  
 \*  
 フルテキスト検索用に登録されているすべての列を使用して、指定した *freetext_string* を検索します。 *Language_term*が指定されていない限り、テーブル内のすべてのフルテキストインデックス列の言語は同じである必要があります。  
  
 *freetext_string*  
 *column_name* で検索するテキストです。 単語、フレーズ、文など、あらゆるテキストを入力できます。 用語または一定の形式になっている用語がフルテキスト インデックス内に見つかった場合、一致するものと判断されます。  
  
 CONTAINS 検索条件とは異なり、とはキーワードで、 *freetext_string* で使用されている場合、"and" はノイズワード ( [ストップワード](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) と見なされ、破棄されます。  
  
 WEIGHT、FORMSOF、ワイルドカード、NEAR、その他の構文は使用できません。 *freetext_string* は単語、語幹に分割され、類義語がチェックされて渡されます。  
  
 LANGUAGE *language_term*  
 クエリにおいて、単語区切り、語幹への分割、類義語のチェック、ストップワードの破棄を行うときに使用する言語リソースの言語を指定します。 このパラメーターは省略可能で、言語のロケール識別子 (LCID) に対応する文字列、整数、または 16 進数の値を指定できます。 *language_term* を指定した場合、その言語は検索条件のすべての要素に適用されます。 値を指定しなかった場合は、列のフルテキストの言語が使用されます。  
  
 1 つの列に言語の異なる複数のドキュメントが BLOB (Binary Large Object) として格納されている場合、そのインデックスの作成に使用される言語は、そのドキュメントのロケール識別子 (LCID) によって決まります。 このような列に対してクエリを実行するときに、 *言語 language_term* を指定すると、一致する確率が高くなる可能性があります。  
  
 *language_term* を文字列で指定する場合は、[sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 互換性ビューの **alias** 列の値と同じ値を指定します。  文字列の場合は、'*language_term*' のように引用符 (') で囲む必要があります。 *language_term* を整数で指定する場合は、その言語を表す実際の LCID を指定します。 *language_term* を 16 進数の値で指定する場合は、「0x」の後に LCID の 16 進数の値を指定します。 16 進数の値は、先頭の 0 を含め、8 桁以内で指定してください。  
  
 値を 2 バイト文字セット (DBCS) の形式で指定すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で Unicode に変換されます。  
  
 指定した言語が無効であるか、その言語に該当するリソースがインストールされていない場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によりエラーが返されます。 ニュートラル言語リソースを使用するには、*language_term* に「0x0」を指定してください。  
  
 *top_n_by_rank*  
 一致したものの中から、降順で順位の高い方から *n 個*だけを返すことを指定します。 整数値 *n*が指定されている場合にのみ適用されます。 *top_n_by_rank* を他のパラメーターと組み合わせた場合、クエリから返される行数は、実際にすべての述語に一致する行数より少なくなります。 *top_n_by_rank* を使用すると、最も関連性の高いヒットだけを再度呼び出すことで、クエリのパフォーマンスを向上させることができます。  
  
## <a name="remarks"></a>解説  
 フルテキストの述語と関数の対象は、FROM 述語で示される 1 つのテーブルです。 複数のテーブルを検索するには、FROM 句で結合テーブルを使用して、複数のテーブルが組み合わされた結果セットを検索します。  
  
 FREETEXTTABLE では、FREETEXT 述語と同じ検索条件が使用されます。  
  
 CONTAINSTABLE と同様に、返されるテーブルには **KEY** と **RANK**という名前の列があります。この列はクエリ内で参照され、適切な行を取得し、行の順位付け値を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 FREETEXTTABLE を呼び出すには、指定されるテーブルまたは参照されるテーブル列に対して適切な SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-simple-example"></a>A. 簡単な例  
 次の例では、2つの列からなる単純なテーブルを作成し、そのフラグの3つの市区郡と色を一覧表示します。 このメソッドは、テーブルにフルテキストカタログとインデックスを作成して設定します。 次に、 **FREETEXTTABLE** 構文を示します。  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. INNER JOIN での FREETEXT の使用  
 次の例では、の意味に一致する説明を持つ製品の説明と順位を返し `high level of performance` ます。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. 言語および最高順位の一致の指定  
 次の例は同じであり、 `LANGUAGE` *language_term*と*top_n_by_rank*パラメーターの使用方法を示しています。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]
>  *Top_n_by_rank*パラメーターを使用するには、言語*language_term*パラメーターは必要ありません。  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索の概要](../../relational-databases/search/get-started-with-full-text-search.md)   
 [フルテキスト カタログの作成と管理](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [フルテキスト検索クエリの作成 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-full-text-search-queries-visual-database-tools.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [行セット関数 &#40;Transact-sql&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [precompute rank サーバー構成オプション](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
