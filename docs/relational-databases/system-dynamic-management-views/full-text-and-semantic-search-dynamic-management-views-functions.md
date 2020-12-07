---
description: フルテキストおよびセマンティック検索の動的管理ビュー-関数
title: フルテキスト検索とセマンティック検索の動的管理ビュー-Functions |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dynamic management objects [SQL Server], full-text search
- full-text search [SQL Server], dynamic management views
ms.assetid: 199dbd5a-29f6-4ef0-8e65-86e32c0aaa3a
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 3f2d7a48bfbccf174b26a08ec3a887f44247a457
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834291"
---
# <a name="full-text-and-semantic-search-dynamic-management-views---functions"></a>フルテキストおよびセマンティック検索の動的管理ビュー-関数
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ここでは、フルテキスト検索とセマンティック検索に関連する次の動的管理ビューおよび関数について説明します。  
  
## <a name="full-text-search-dynamic-management-views-and-functions"></a>フルテキスト検索の動的管理ビューおよび関数  
 [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
 サーバー上でいくつかの作成アクティビティが進行中のフルテキストカタログに関する情報を返します。  
  
 [sys.dm_fts_fdhosts](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
 サーバー インスタンス上のフィルター デーモン ホストの現在のアクティビティに関する情報を返します。  
  
 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
 指定されたテーブルのフルテキスト インデックスのコンテンツに関する情報を返します。  
  
 [sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
 指定されたテーブルについて、フルテキスト インデックスのドキュメント レベルのコンテンツに関連する情報を返します。 個々のキーワードは、複数のドキュメントに出現する場合があります。  
  
 [sys.dm_fts_index_keywords_by_property](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
 指定されたテーブルのフルテキストインデックスに含まれるプロパティ関連のすべてのコンテンツを返します。 これには、そのフルテキストインデックスに関連付けられている検索プロパティリストによって登録されたすべてのプロパティに属するすべてのデータが含まれます。  
  
 sys.dm_fts_index_keywords_position_by_document  
 ドキュメント内のキーワードの位置を返します。  
  
 [sys.dm_fts_index_population](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
 現在実行中の、フルテキスト インデックス設定に関する情報を返します。  
  
 [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
 フルテキスト クロールまたはフルテキスト クロール範囲の一部として使用される、特定のメモリ プールのメモリ バッファーに関する情報を返します。  
  
 [sys.dm_fts_memory_pools](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
 フルテキストクロールまたはフルテキストクロールの範囲でフルテキスト Gatherer コンポーネントで使用できる共有メモリプールに関する情報を返します。  
  
 [sys.dm_fts_outstanding_batches](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
 各フルテキストインデックスバッチに関する情報を返します。  
  
 [sys.dm_fts_parser](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
 特定のワードブレーカー、類義語辞典、およびストップリストの組み合わせをクエリ文字列入力に適用した後に、最終的なトークン化の結果を返します。 出力は、指定したクエリ文字列が Full-Text Engine に対して発行された場合の出力と同じです。  
  
 [sys.dm_fts_population_ranges](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
 現在実行中のフルテキストインデックスの作成に関連する特定の範囲に関する情報を返します。  
  
## <a name="semantic-search-dynamic-management-views-and-functions"></a>セマンティック検索の動的管理ビューおよび関数  
 [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
 関連付けられたセマンティックインデックスを持つ各テーブルの各類似性インデックスについて、ドキュメントの類似性のインデックスの作成に関するステータス情報の1行を返します。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)  
  
