---
description: DROP SEARCH PROPERTY LIST (Transact-SQL)
title: DROP SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 48a62e9aa8137d38e47b38d0228ec617c563f572
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191828"
---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  検索プロパティ リストがデータベース内のフルテキスト インデックスに現在関連付けられていない場合に、現在のデータベースからプロパティ リストを削除します。  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *property_list_name*  
 削除する検索プロパティ リストの名前です。 *property_list_name* は識別子です。  
  
 既存のプロパティ リストの名前を表示するには、次のように [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) カタログ ビューを使用します。  
  
```sql  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>注釈  
 リストがいずれかのフルテキスト インデックスに関連付けられている場合は、データベースから検索プロパティ リストを削除できません。削除しようとすると失敗します。 特定のフルテキスト インデックスから検索プロパティ リストを削除するには、[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ステートメントを使い、SET SEARCH PROPERTY LIST 句に OFF または別の検索プロパティ リストの名前を指定します。  
  
 **サーバー インスタンス上のプロパティ リストを表示するには**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **フルテキスト インデックスに関連付けられているプロパティ リストを表示するには**  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **フルテキスト インデックスからプロパティ リストを削除するには**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 検索プロパティ リストに対する CONTROL 権限が必要です。  
  
> [!NOTE]  
>  プロパティ リストの CONTROL 権限はそのリストの所有者が許可できます。 既定では、検索プロパティ リストを作成したユーザーがその所有者になります。 所有者は、[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使って変更できます。  
  
## <a name="examples"></a>例  
 次の例では、`JobCandidateProperties` プロパティ リストを `AdventureWorks2012` データベースから削除します。  
  
```sql  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  
