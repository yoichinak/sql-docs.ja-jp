---
description: sp_fulltext_load_thesaurus_file (Transact-SQL)
title: sp_fulltext_load_thesaurus_file (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7fa28cb49c289437bc6c9dea524d1ff9e8b8ac64
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546184"
---
# <a name="sp_fulltext_load_thesaurus_file-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーインスタンスが、LCID が指定されている言語に対応する類義語辞典ファイルのデータを解析して読み込みます。 このストアドプロシージャは、類義語辞典ファイルを更新した後に便利です。 **Sp_fulltext_load_thesaurus_file**を実行すると、指定した LCID の類義語辞典を使用するフルテキストクエリが再コンパイルされます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>引数  
 *lcid*  
 類義語辞典 XML 定義を作成する言語のロケール識別子 (LCID) をマッピングする整数。 サーバーインスタンスで使用できる言語の Lcid を取得するには、 [fulltext_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) カタログビューを使用します。  
  
 ** \@ loadonlyifnotloaded**  =  *アクション*  
 類義語辞典ファイルが既に読み込まれている場合でも、内部の類義語辞典テーブルに類義語辞典ファイルを読み込むかどうかを指定します。 *アクション* は次のいずれかです。  
  
|値|定義|  
|-----------|----------------|  
|**0**|既に読み込まれているかどうかにかかわらず、類義語辞典ファイルを読み込みます。 これは **sp_fulltext_load_thesaurus_file**の既定の動作です。|  
|1|類義語辞典ファイルがまだ読み込まれていない場合にのみ、類義語辞典ファイルを読み込みます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 類義語辞典ファイルは、類義語辞典を使用するフルテキスト クエリによって自動的に読み込まれます。 フルテキストクエリのパフォーマンスへの影響を初めて回避するには、 **sp_fulltext_load_thesaurus_file**を実行することをお勧めします。  
  
 フルテキスト検索に登録されている言語の一覧を更新するには、 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_fulltext_load_thesaurus_file**ストアドプロシージャを実行できるのは、 **sysadmin**固定サーバーロールのメンバー、またはシステム管理者だけです。  
  
 類義語辞典ファイルを更新、変更、または削除できるのはシステム管理者だけです。  
  
## <a name="examples"></a>例  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>A. 類義語辞典ファイルが既に読み込まれている場合でも類義語辞典ファイルを読み込む  
 次の例では、英語の類義語辞典ファイルを解析して読み込みます。  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1033;
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. 類義語辞典ファイルがまだ読み込まれていない場合にのみ、類義語辞典ファイルを読み込む。  
 次の例では、既に読み込まれている場合を除き、アラビア語の類義語辞典ファイルを解析して読み込みます。  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;
```  

## <a name="see-also"></a>参照

[FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)  
[システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
[フルテキスト検索に使用する類義語辞典ファイルの構成と管理](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)
