---
description: dm_fts_parser (Transact-sql)
title: dm_fts_parser (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_parser_TSQL
- dm_fts_parser
- dm_fts_parser_TSQL
- sys.dm_fts_parser
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_parser dynamic management function
- troubleshooting [SQL Server], full-text search
ms.assetid: 2736d376-fb9d-4b28-93ef-472b7a27623a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 3005c1d843796bfa9206750134d7be1c4f4546fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454959"
---
# <a name="sysdm_fts_parser-transact-sql"></a>dm_fts_parser (Transact-sql)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定の [ワードブレーカー](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)、 [類義語辞典](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)、および [ストップリスト](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) の組み合わせをクエリ文字列入力に適用した後に、最終的なトークン化の結果を返します。 トークン化の結果は、指定されたクエリ文字列のフルテキストエンジンの出力に相当します。  
  
 sys.dm_fts_parser は動的管理関数です。  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_fts_parser('query_string', lcid, stoplist_id, accent_sensitivity)  
```  
  
## <a name="arguments"></a>引数  
 *query_string*  
 解析するクエリ。 *query_string* 構文のサポートを [含む](../../t-sql/queries/contains-transact-sql.md) 文字列チェーンを指定できます。 たとえば、変化形、類義語辞典、および論理演算子を含めることができます。  
  
 *lcid*  
 *Query_string*の解析に使用するワードブレーカーのロケール識別子 (LCID)。  
  
 *stoplist_id*  
 *Lcid*によって識別されるワードブレーカーによって使用されるストップリスト (存在する場合) の ID。 *stoplist_id* は **int**です。' NULL ' を指定した場合、ストップリストは使用されません。 0を指定した場合は、システムストップリストが使用されます。  
  
 ストップリスト ID は、データベース内で一意です。 指定されたテーブルのフルテキストインデックスのストップリスト ID を取得するには、 [fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) カタログビューを使用します。  
  
 *accent_sensitivity*  
 フルテキスト検索で分音文字を区別するかしないかを制御するブール値です。 *accent_sensitivity* は **ビット**で、次のいずれかの値になります。  
  
|値|アクセントの区別は...|  
|-----------|----------------------------|  
|0|大文字と小文字は区別されない<br /><br /> "カフェ" や "カフェ" などの単語は、同じように扱われます。|  
|1|重要<br /><br /> "カフェ" や "カフェ" などの単語は、異なる方法で処理されます。|  
  
> [!NOTE]  
>  フルテキストカタログのこの値の現在の設定を表示するには、次のステートメントを実行します [!INCLUDE[tsql](../../includes/tsql-md.md)] : `SELECT fulltextcatalogproperty('` *catalog_name* `', 'AccentSensitivity');` 。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|キーワード (keyword)|**varbinary (128)**|ワードブレーカーによって返される特定のキーワードの16進数表現。 この表記は、フルテキスト インデックスにキーワードを格納するために使用します。 この値は人間が判読できませんが、フルテキストインデックスの内容を返す他の動的管理ビューによって返される出力に特定のキーワードを関連付けると便利です。たとえば、 [dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md) や [dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)などです。<br /><br /> **注:** 0 Xff は、ファイルまたはデータセットの末尾を示す特殊文字を表します。|  
|group_id|**int**|特定の用語の生成元である論理グループを区別するのに役立つ整数値を格納します。 たとえば、英語の場合、'`Server AND DB OR FORMSOF(THESAURUS, DB)"`' で次の group_id 値が生成されます。<br /><br /> 1: サーバー<br />2: DB<br />3: DB|  
|phrase_id|**int**|には、フルテキストなどの複合単語の代替形式がワードブレーカーによって発行されるケースを区別するのに役立つ整数値が含まれています。 複合語 ('multi-million' など) が存在する場合、ワード ブレーカーによって代替形式が発行されることがあります。 このような代替形式 (語句) は区別が必要になる場合があります。<br /><br /> たとえば、英語の場合、'`multi-million`' で次の phrase_id 値が生成されます。<br /><br /> の場合は1 `multi`<br />の場合は1 `million`<br />2 `multimillion`|  
|occurrence|**int**|解析結果の各用語の順序を示します。 たとえば、英語の "`SQL Server query processor`" という語句の場合、occurrence には語句内の用語に対する次のオカレンス値が格納されます。<br /><br /> の場合は1 `SQL`<br />2 `Server`<br />3 `query`<br />4 `processor`|  
|special_term|**nvarchar (4000)**|ワード ブレーカーによって発行されている用語の特性に関する情報を格納します。次のいずれかになります。<br /><br /> 完全一致<br /><br /> ノイズワード<br /><br /> 文の終わり<br /><br /> 段落の末尾<br /><br /> 章の終わり|  
|display_term|**nvarchar (4000)**|人間が判読できる形式のキーワードが含まれています。 フルテキスト インデックスのコンテンツにアクセスするように設計されている関数と同様に、ここに表示される用語は、非正規化の制限のため元の用語と同一とは限りません。 ただし、元の入力から識別しやすいように、十分な値にする必要があります。|  
|expansion_type|**int**|特定の用語の拡張の特性に関する情報を格納します。次のいずれかになります。<br /><br /> 0 = 1 つの単語の場合<br /><br /> 2 = 変化形の拡張<br /><br /> 4 = 類義語辞典の拡張と置換<br /><br /> たとえば、類義語辞典で run が `jog` の拡張として定義されている場合を考えてみます。<br /><br /> `<expansion>`<br /><br /> `<sub>run</sub>`<br /><br /> `<sub>jog</sub>`<br /><br /> `</expansion>`<br /><br /> この用語は、 `FORMSOF (FREETEXT, run)` 次の出力を生成します。<br /><br /> `run` : expansion_type=0<br /><br /> `runs` : expansion_type=2<br /><br /> `running` : expansion_type=2<br /><br /> `ran` : expansion_type=2<br /><br /> `jog` : expansion_type=4|  
|source_term|**nvarchar (4000)**|特定の用語の生成元または解析元になった用語または語句です。 たとえば、英語の場合、`word breakers" AND stemmers'` に対するクエリで次の source_term 値が生成されます。<br /><br /> `word breakers` display_term`word`<br />`word breakers` display_term`breakers`<br />`stemmers` display_term`stemmers`|  
  
## <a name="remarks"></a>解説  
 **dm_fts_parser** は、 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) や [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)などのフルテキスト述語の構文と機能、および [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) や [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)などの関数をサポートしています。  
  
## <a name="using-unicode-for-parsing-special-characters"></a>特殊文字の解析での Unicode の使用  
 クエリ文字列を解析する場合、dm_fts_parser では、クエリ文字列を Unicode として指定しない限り、接続先のデータベースの照合順序が使用され**ます。** したがって、üやçなどの特殊文字を含む非 Unicode 文字列の場合、データベースの照合順序によっては出力が予期しないものになる可能性があります。 データベースの照合順序とは無関係にクエリ文字列を処理するには、文字列の先頭にを付け `N` ます。つまり、 `N'` *query_string* `'` します。  
  
 詳細については、「C」を参照してください。 特殊文字を含む文字列の出力を表示する」を参照してください。  
  
## <a name="when-to-use-sysdm_fts_parser"></a>Dm_fts_parser を使用する場合  
 **dm_fts_parser** は、デバッグの目的で非常に強力です。 主な使用シナリオには、次のようなものがあります。  
  
-   特定のワードブレーカーが特定の入力をどのように処理するかを理解するには  
  
     クエリから予期しない結果が返された場合、ワードブレーカーがデータを解析および分割する方法が原因である可能性があります。 sys.dm_fts_parser を使用すると、ワード ブレーカーからフルテキスト インデックスに渡される結果を検出できます。 また、フルテキストインデックスでは検索されないストップワードの用語も確認できます。 用語が特定の言語のストップワードであるかどうかは、関数で宣言されている *stoplist_id* 値によって指定されたストップリスト内にあるかどうかによって異なります。  
  
     ユーザーがワード ブレーカーによる入力の解析方法を確認できるようにするアクセントの区別フラグには、アクセントの区別に関する情報が格納されているので、これも確認してください。  
  
-   特定の入力でのステマーの動作を理解するには  
  
     ワードブレーカーとステマーによってクエリ用語とそのステミング形式がどのように解析されるかを確認するには、次のようなクエリを含む CONTAINS または CONTAINSTABLE クエリを指定します。  
  
    ```  
    FORMSOF( INFLECTIONAL, query_term )  
    ```  
  
     この結果から、フルテキスト インデックスに渡されている用語がわかります。  
  
-   類義語辞典によって入力の全体または一部がどのように拡大または置換されるかを理解するには  
  
     次のように指定することもできます。  
  
    ```  
    FORMSOF( THESAURUS, query_term )  
    ```  
  
     このクエリの結果は、ワードブレーカーと類義語辞典がクエリ用語に対してどのように対話するかを示しています。 類義語辞典から拡張または置換を確認し、フルテキスト インデックスに対して実際に発行されているクエリを特定することができます。  
  
     ユーザーが次のような場合に注意してください。  
  
    ```  
    FORMSOF( FREETEXT, query_term )  
    ```  
  
     変化形と類義語辞典の機能は自動的に行われます。  
  
 上記の使用シナリオに加え、sys.dm_fts_parser は、フルテキスト クエリに関する他の多くの問題の理解やトラブルシューティングに大きく役立ちます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップと、指定されたストップリストへのアクセス権が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-the-output-of-a-given-word-breaker-for-a-keyword-or-phrase"></a>A. キーワードまたは語句に関する特定のワード ブレーカーの出力を表示する  
 次の例では、LCID が1033で、次のクエリ文字列にストップリストがない、英語のワードブレーカーを使用した場合の出力が返されます。  
  
 `The Microsoft business analysis`  
  
 アクセントの区別は無効になっています。  
  
```sql
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis" ', 1033, 0, 0);  
```  
  
### <a name="b-displaying-the-output-of-a-given-word-breaker-in-the-context-of-stoplist-filtering"></a>B. ストップリストのフィルター処理のコンテキストで特定のワードブレーカーの出力を表示する  
 次の例では、次のクエリ文字列に対して LCID が1033で、ID が77である英語ストップリストを使用した場合の出力が返されます。  
  
 `"The Microsoft business analysis" OR "MS revenue"`  
  
 アクセントの区別は無効になっています。  
  
```sql
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis"  OR " MS revenue" ', 1033, 77, 0);  
```  
  
### <a name="c-displaying-the-output-of-a-string-that-contains-special-characters"></a>C. 特殊文字を含む文字列の出力を表示する  
 次の例では、Unicode を使用して次のフランス語の文字列を解析します。  
  
 `français`  
  
 この例では、フランス語の LCID として `1036` と、ユーザー定義のストップリストの ID として `5` を指定します。 アクセントの区別が有効になっています。  
  
```sql
SELECT * FROM sys.dm_fts_parser(N'français', 1036, 5, 1);  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [検索用のワードブレーカーとステミング機能の構成と管理](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [フルテキスト検索用の類義語辞典ファイルの構成と管理](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [フルテキスト検索のためのストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [セキュリティ保護可能](../../relational-databases/security/securables.md)  
  
  
