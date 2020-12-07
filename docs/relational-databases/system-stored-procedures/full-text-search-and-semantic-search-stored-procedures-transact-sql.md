---
description: フルテキスト検索およびセマンティック検索ストアド プロシージャ (Transact-SQL)
title: フルテキスト検索およびセマンティック検索ストアドプロシージャ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], stored procedures
- full-text search [SQL Server], stored procedures
- full-text catalogs [SQL Server], stored procedures
- system stored procedures [SQL Server], full-text search
ms.assetid: 0d185a16-2b16-4958-884f-efe675e2e551
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e69a1f01da28883311b96d3a623acc1888c642d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542045"
---
# <a name="full-text-search-and-semantic-search-stored-procedures-transact-sql"></a>フルテキスト検索およびセマンティック検索ストアド プロシージャ (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、フルテキストインデックスおよびセマンティックインデックスの実装とクエリに使用される、次のシステムストアドプロシージャがサポートされています。  
  
## <a name="full-text-search-stored-procedures"></a>フルテキスト検索ストアド プロシージャ  
 [sp_fulltext_catalog](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)  
 フルテキスト カタログの作成と削除、およびカタログのインデックス作成の開始と中止を行います。 各データベースに対して複数のフルテキストカタログを作成できます。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに、[ [フルテキスト](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)カタログの作成]、[ [フルテキスト](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)カタログの変更]、および [ [フルテキスト](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) カタログの削除] を使用します。  
  
 [sp_fulltext_column](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)  
 テーブルの特定の列がフルテキストインデックスに参加するかどうかを指定します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [ALTER フルテキストインデックス](../../t-sql/statements/alter-fulltext-index-transact-sql.md) を使用してください。  
  
 [sp_fulltext_database](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)  
 以降のバージョンのフルテキストカタログには影響しません [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 。旧バージョンとの互換性のためにのみサポートされています。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
 ドキュメント識別子 (**DocId**) とフルテキストキー値の間のマッピングを返します。  
  
 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 LCID に対応する更新された類義語辞典ファイルのデータを解析して読み込み、類義語辞典を使用するフルテキストクエリの再コンパイルを行います。  
  
 [sp_fulltext_pendingchanges](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
 変更の追跡を使用している指定されたテーブルについて、保留中の挿入、更新、削除などの未処理の変更を返します。  
  
 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
 SQL Server のフルテキスト検索のサーバープロパティを変更します。  
  
 [sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)  
 フルテキストインデックスを作成するテーブルをマークまたは非表示にします。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに、フル [テキストインデックスの作成](../../t-sql/statements/create-fulltext-index-transact-sql.md)、フルテキストインデックスの [変更](../../t-sql/statements/alter-fulltext-index-transact-sql.md)、および [フルテキスト](../../t-sql/statements/drop-fulltext-index-transact-sql.md) インデックスの削除を使用します。  
  
 [sp_help_fulltext_catalog_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql.md)  
 現在のデータベースにあるすべてのフルテキスト カタログに使用されている、すべてのコンポーネント (フィルター、ワード ブレーカー、プロトコル ハンドラー) の一覧を返します。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_help_fulltext_catalogs](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
 指定したフルテキストカタログの ID、名前、ルートディレクトリ、状態、およびフルテキストインデックスが作成されたテーブルの数を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) カタログビューを使用してください。  
  
 [sp_help_fulltext_catalogs_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)  
 カーソルを使用して、指定したフルテキストカタログの ID、名前、ルートディレクトリ、状態、およびフルテキストインデックスが作成されたテーブルの数を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) カタログビューを使用してください。  
  
 [sp_help_fulltext_columns](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)  
 フルテキスト インデックス作成用として指定された列を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) カタログビューを使用してください。  
  
 [sp_help_fulltext_columns_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)  
 カーソルを使用して、フルテキストインデックス作成用に指定された列を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) カタログビューを使用してください。  
  
 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
 登録されているワードブレーカー、フィルター、およびプロトコルハンドラーの情報に加え、指定したコンポーネントを使用したデータベースとフルテキストカタログの識別子の一覧を返します。  
  
 [sp_help_fulltext_tables](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)  
 フルテキストインデックス作成用に登録されているテーブルの一覧を返します。  
  
 [sp_help_fulltext_tables_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)  
 フルテキストインデックス作成用に登録されているテーブルの一覧を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) カタログビューを使用してください。  
  
## <a name="semantic-search-stored-procedures"></a>セマンティック検索ストアド プロシージャ  
 [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスで、事前にデータが設定されているセマンティック言語統計データベースを登録します。  
  
 [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)  
 の現在のインスタンスから既存のセマンティック言語統計データベースの登録 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を解除し、関連付けられているメタデータを削除します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索およびセマンティック検索カタログビュー ](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)  
  
  
