---
description: semantickeyphrasetable (Transact-sql)
title: semantickeyphrasetable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8026760d93132e3a18b51145bc1802e416bc0934
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464811"
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたテーブル内の指定された列に関連付けられているキー フレーズに対し、0 行、1 行、または複数の行を含むテーブルを返します。  
  
 この行セット関数は、標準のテーブル名のように、SELECT ステートメントの FROM 句で参照できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
    )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 **テーブル**  
 フルテキスト インデックスとセマンティック インデックスが有効になっているテーブルの名前を指定します。  
  
 この名前には 1 ~ 4 つの部分名を指定できますが、リモートサーバー名は許可されません。  
  
 **column**  
 結果が返されるインデックス付き列の名前。 列でセマンティックインデックス作成が有効になっている必要があります。  
  
 **column_list**  
 複数の列をコンマで区切り、かっこで囲んで指定します。 すべての列でセマンティックインデックス作成が有効になっている必要があります。  
  
 **\***  
 セマンティック インデックスが有効になっているすべての列が含まれていることを示します。  
  
 **source_key**  
 行の一意のキーで、特定の行の結果を要求します。  
  
 キーは、可能な場合は常に、ソーステーブル内のフルテキスト一意キーの型に暗黙的に変換されます。 キーは定数または変数として指定できますが、式またはスカラーサブクエリの結果にすることはできません。 Source_key を省略した場合、すべての行に対して結果が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
 次の表は、この行セット関数が返すキーフレーズに関する情報を示しています。  
  
|Column_name|Type|説明|  
|------------------|----------|-----------------|  
|**column_id**|**int**|現在のキーフレーズを抽出してインデックスを作成した列の ID。<br /><br /> 列 ID から列名 (または列名から列 ID) を取得する方法の詳細については、COL_NAME 関数と COLUMNPROPERTY 関数のセクションを参照してください。|  
|**document_key**|**\***<br /><br /> このキーは、ソーステーブル内の一意なキーの型と一致します。|現在のキーフレーズのインデックスが作成されたドキュメントまたは行の一意のキー値。|  
|**キーフレーズ**|**NVARCHAR**|Column_id によって識別され、document_key によって指定されたドキュメントに関連付けられている列に含まれるキーフレーズ。|  
|**スコア**|**本当の**|インデックス付き列内の同じドキュメント内の他のすべてのキーフレーズとの関係における、このキーフレーズの相対値。<br /><br /> この値は [0.0, 1.0] の範囲内の小数値です。スコアの値が大きいほど類似性が高く、1.0 は完全に一致することを表します。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、「 [セマンティック検索を使用してドキュメント内のキーフレーズを検索](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)する」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 セマンティックなキー フレーズの抽出および生成の詳細と状態については、次の動的管理ビューに対してクエリを実行してください。  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 フルテキストおよびセマンティック インデックスが作成されたベース テーブルに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
  
###  <a name="example-1-find-the-top-key-phrases-in-a-specific-document"></a><a name="HowToTopPhrases"></a> 例 1: 特定のドキュメントに含まれる上位のキーフレーズを検索する  
 次の例では、AdventureWorks サンプル データベースの Production.Document テーブルの Document 列にある、@DocumentId 変数で指定されたドキュメントから、上位 10 個のキー フレーズを取得します。 @DocumentId 変数は、フルテキスト インデックスのキー列の値を表します。 **SEMANTICKEYPHRASETABLE** 関数は、テーブル スキャンではなくインデックス シークを使用してこれらの結果を効率的に取得します。 この例では、列がフルテキストインデックスとセマンティックインデックス作成用に構成されていることを前提としています。  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="example-2-find-the-top-documents-that-contain-a-specific-key-phrase"></a><a name="HowToTopDocuments"></a> 例 2: 特定のキーフレーズを含む上位のドキュメントを検索する  
 次の例では、AdventureWorks サンプル データベースの Production.Document テーブルの Document 列から、キー フレーズ "Bracket" を含む上位 25 個のドキュメントを取得します。 この例では、列がフルテキストインデックスとセマンティックインデックス作成用に構成されていることを前提としています。  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
  
```  
  
  
