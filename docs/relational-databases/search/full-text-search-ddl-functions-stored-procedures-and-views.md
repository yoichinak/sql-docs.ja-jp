---
description: フルテキスト検索の DDL、関数、ストアド プロシージャ、およびビュー
title: フルテキスト検索の DDL、関数、ストアド プロシージャ、ビュー
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: 98c36715-4195-482e-a4a3-d93ff65b75f1
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: bd7907a1f5dee4516f1cdcca6c7bd0fb45c80605
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498611"
---
# <a name="full-text-search-ddl-functions-stored-procedures-and-views"></a>フルテキスト検索の DDL、関数、ストアド プロシージャ、およびビュー
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  プロパティ検索機能を含むフルテキスト検索をサポートする Transact-SQL ステートメントおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース オブジェクトの一覧を示します。  
  
 非推奨のオブジェクトは含まれていません。  
  
 セマンティック検索をサポートするデータベース オブジェクトの一覧については、「 [セマンティック検索の DDL、関数、ストアド プロシージャ、およびビュー](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md)」を参照してください。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Transact-SQL データ定義言語 (DDL) ステートメント  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
-   [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)  
  
-   [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
-   [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
-   [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)  
  
-   [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)  
  
-   [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="system-predicates-and-functions"></a><a name="func"></a> システムの述語と関数  
  
-   [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
  
-   [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
  
-   [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)  
  
-   [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
  
##  <a name="system-metadata-functions"></a><a name="meta"></a> システム メタデータ関数  
  
-   [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
  
-   [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)  
  
-   [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)  
  
-   [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)  
  
-   [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)  
  
-   [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
-   [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
##  <a name="system-stored-procedures"></a><a name="proc"></a> システム ストアド プロシージャ  
  
-   [sp_fulltext_keymappings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
  
-   [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
  
-   [sp_fulltext_pendingchanges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
  
-   [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
  
##  <a name="system-views---catalog-views"></a><a name="cat"></a> システム ビュー - カタログ ビュー  
  
-   [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)  
  
-   [sys.fulltext_document_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)  
  
-   [sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
-   [sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
-   [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)  
  
-   [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
-   [sys.fulltext_system_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)  
  
-   [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
##  <a name="system-views---dynamic-management-views"></a><a name="dmv"></a> システム ビュー - 動的管理ビュー  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
-   [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  
