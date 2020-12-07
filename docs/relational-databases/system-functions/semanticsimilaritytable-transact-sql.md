---
description: semanticsimilaritytable (Transact-sql)
title: semanticsimilaritytable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritytable
- semanticsimilaritytable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritytable function
ms.assetid: b49d40ab-7552-438b-ad67-6237dcccb75b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4866c5002fce3540014b9ad0c94ccd7b20a0e235
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397278"
---
# <a name="semanticsimilaritytable-transact-sql"></a>semanticsimilaritytable (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定した列の内容が、指定したドキュメントと意味的に似ているドキュメントについて、0行、1行、または複数の行から成るテーブルを返します。  
  
 この行セット関数は、標準のテーブル名のように、SELECT ステートメントの FROM 句で参照できます。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
SEMANTICSIMILARITYTABLE  
    (  
    table,  
    { column | (column_list) | * },  
    source_key  
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
  
 キーは、可能な場合は常に、ソーステーブル内のフルテキスト一意キーの型に暗黙的に変換されます。 キーは定数または変数として指定できますが、式またはスカラーサブクエリの結果にすることはできません。  
  
## <a name="table-returned"></a>返されるテーブル  
 次の表では、この行セット関数が返す類似ドキュメントおよび関連ドキュメントについて説明します。  
  
 結果が複数の列から要求された場合、一致したドキュメントが列ごとに返されます。  
  
|Column_name|Type|説明|  
|------------------|----------|-----------------|  
|**source_column_id**|**int**|ソース ドキュメントを使用して類似したドキュメントを検出したときの、検出元の列の ID。<br /><br /> 列 ID から列名 (または列名から列 ID) を取得する方法の詳細については、COL_NAME 関数と COLUMNPROPERTY 関数のセクションを参照してください。|  
|**matched_column_id**|**int**|類似したドキュメントが見つかった列の ID。<br /><br /> 列 ID から列名 (または列名から列 ID) を取得する方法の詳細については、COL_NAME 関数と COLUMNPROPERTY 関数のセクションを参照してください。|  
|**matched_document_key**|**\***<br /><br /> このキーは、ソーステーブル内の一意なキーの型と一致します。|クエリで指定したドキュメントに類似していることが判明したドキュメントまたは行の、フルテキストおよびセマンティックな抽出の一意のキー値。|  
|**スコア**|**本当の**|類似した他のすべてのドキュメントとの関係における、このドキュメントの類似性の相対値。<br /><br /> この値は、[0.0, 1.0] の範囲の小数点値です。この値より高いスコアは、近い方の一致を表し、1.0 は完全なスコアになります。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、「 [セマンティック検索による類似および関連ドキュメントの検索](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)」を参照してください。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 複数の列にわたって類似したドキュメントに対するクエリを実行することはできません。 **SEMANTICSIMILARITYTABLE**関数は、 **source_key**引数によって識別される、ソース列と同じ列から類似したドキュメントだけを取得します。  
  
## <a name="metadata"></a>メタデータ  
 セマンティック類似性の抽出と作成の詳細と状態については、次の動的管理ビューに対してクエリを実行します。  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 フルテキストおよびセマンティック インデックスが作成されたベース テーブルに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、AdventureWorks2012 サンプル データベースの HumanResources.JobCandidate テーブルから、指定した候補に類似する上位 10 件の候補を取得します。  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROMSEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
