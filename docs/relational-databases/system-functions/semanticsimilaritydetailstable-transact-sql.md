---
description: semanticsimilaritydetailstable (Transact-sql)
title: semanticsimilaritydetailstable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fa94a6c16eaaf2548b3c0375d43848d5e03a7f12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474586"
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  2つのドキュメント (ソースドキュメントと一致するドキュメント) に共通するキーフレーズの0行、1行、または複数の行から成るテーブルを返します。このテーブルの内容は意味が似ています。  
  
 この行セット関数は、SELECT ステートメントの FROM 句で参照できます。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 **テーブル**  
 フルテキスト インデックスとセマンティック インデックスが有効になっているテーブルの名前を指定します。  
  
 この名前には 1 ~ 4 つの部分名を指定できますが、リモートサーバー名は許可されません。  
  
 **source_column**  
 類似性を比較されるコンテンツを含んだソース行の列の名前。  
  
 **source_key**  
 ソース ドキュメントの行を表す一意のキー。  
  
 このキーは、可能であれば常に、ソース テーブル内の一意なフルテキスト キーの型に、暗黙的に変換されます。 キーは定数または変数として指定できますが、式またはスカラーサブクエリの結果にすることはできません。 無効なキーが指定された場合、行は返されません。  
  
 **matched_column**  
 類似性と比較するコンテンツを含む、一致する行の列の名前。  
  
 **matched_key**  
 一致ドキュメントの行を表す一意のキー。  
  
 このキーは、可能であれば常に、ソース テーブル内の一意なフルテキスト キーの型に、暗黙的に変換されます。 キーは定数または変数として指定できますが、式またはスカラーサブクエリの結果にすることはできません。  
  
## <a name="table-returned"></a>返されるテーブル  
 次の表は、この行セット関数が返すキーフレーズに関する情報を示しています。  
  
|Column_name|Type|説明|  
|------------------|----------|-----------------|  
|**キーフレーズ**|**NVARCHAR**|ソースドキュメントと一致したドキュメントとの類似性に貢献するキーフレーズ。|  
|**スコア**|**本当の**|2つのドキュメント間で類似している他のすべてのキーフレーズとの関係における、このキーフレーズの相対値。<br /><br /> この値は [0.0, 1.0] の範囲内の小数値です。スコアの値が大きいほど類似性が高く、1.0 は完全に一致することを表します。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、「 [セマンティック検索による類似および関連ドキュメントの検索](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 セマンティック類似性の抽出と作成の詳細と状態については、次の動的管理ビューに対してクエリを実行します。  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 フルテキストおよびセマンティック インデックスが作成されたベース テーブルに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、AdventureWorks2012 サンプルデータベースの **humanresources.employee** テーブル内の指定された候補との間に最も高い類似性スコアを持つ5つのキーフレーズを取得します。 @CandidateId変数と @MatchedID 変数は、フルテキストインデックスのキー列の値を表します。  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
