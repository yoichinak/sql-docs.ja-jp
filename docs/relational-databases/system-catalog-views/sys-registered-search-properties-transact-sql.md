---
description: sys.registered_search_properties (Transact-SQL)
title: registered_search_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d7c4944b4014c4c0a584e19eb2d4ba12f244ee47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447898"
---
# <a name="sysregistered_search_properties-transact-sql"></a>sys.registered_search_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベースの検索プロパティリストに含まれる検索プロパティごとに1行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|このプロパティが属する検索プロパティリストの ID。|  
|**property_set_guid**|**uniqueidentifier**|検索プロパティが属するプロパティ セットを識別するグローバル一意識別子 GUID。|  
|**property_int_id**|**int**|プロパティセット内でこの検索プロパティを識別する整数。 **property_int_id** は、プロパティセット内で一意です。|  
|**property_name**|**nvarchar (64)**|検索プロパティリストでこの検索プロパティを一意に識別する名前。<br /><br /> 注: プロパティを検索するには、 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 述語でこのプロパティ名を指定します。|  
|**property_description**|**nvarchar(512)**|プロパティの説明。|  
|**property_id**|**int**|**Property_list_id**値によって識別される検索プロパティリスト内の検索プロパティの内部プロパティ ID。<br /><br /> 特定のプロパティが特定の検索プロパティ リストに追加されると、Full-Text Engine は、プロパティを登録し、このプロパティ リストに固有の内部プロパティ ID を、そのプロパティに割り当てます。 内部プロパティ ID (整数) は、特定の検索プロパティリストに対して一意です。 特定のプロパティを複数の検索プロパティ リストに登録した場合、検索プロパティ リストごとに異なる内部プロパティ ID が割り当てられる可能性があります。<br /><br /> 注: 内部プロパティ ID は、プロパティを検索プロパティリストに追加するときに指定されるプロパティ整数識別子とは異なります。 詳細については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。<br /><br /> フルテキストインデックス内のすべてのプロパティ関連コンテンツを表示するには、次のようにします。 <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>解説  
 検索プロパティ リストについて詳しくは、「[検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 検索プロパティのメタデータの表示は、自分が所有しているか、または何らかの参照権限が付与されている検索プロパティリスト内のものに限定されます。  
  
> [!NOTE]  
>  検索プロパティリストの所有者は、一覧に対する参照または制御権限を許可できます。 CONTROL 権限を持つユーザーは、他のユーザーに REFERENCE 権限を与えることができます。  
  
## <a name="examples"></a>例  
 次の例は、登録されている検索プロパティのすべてのメタデータを表示します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.registered_search_properties;   
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [fulltext_indexes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
