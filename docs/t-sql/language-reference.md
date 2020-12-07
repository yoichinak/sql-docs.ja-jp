---
description: Transact-SQL リファレンス (データベース エンジン)
title: Transact-SQL リファレンス (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 04/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql13.tsqlref.f1
- devlang-tsql
helpviewer_keywords:
- Transact-SQL
ms.assetid: dbba47d7-e08e-4435-b876-35dced1f325d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 422ab559997e5dc33a0d8155c198cb23cba5698b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035895"
---
# <a name="transact-sql-reference-database-engine"></a>Transact-SQL リファレンス (データベース エンジン)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

このトピックでは、Microsoft [!INCLUDE[tsql](../includes/tsql-md.md)] (T-SQL) のリファレンス トピックを見つけて使用する方法の基本事項を説明します。 T-SQL は、Microsoft SQL の製品やサービスを使用するときの中心となる機能です。 SQL データベースと通信するツールやアプリケーションはすべて、T-SQL のコマンドを送信するという方法で通信します。  

## <a name="t-sql-compliance-to-sql-standard"></a>SQL 標準に準拠した T-SQL
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] での特定の標準の実装方法に関する詳細な技術ドキュメントについては、[Microsoft SQL Server 標準のサポート ドキュメント](/openspecs/sql_standards/ms-sqlstandlp/89fb00b1-4b9e-4296-92ce-a2b3f7ca01d2)を参照してください。

## <a name="tools-that-use-t-sql"></a>T-SQL を使用するツール
Microsoft のツールのうち、T-SQL のコマンドを発行する主なものは次のとおりです。

- [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [sqlcmd](../tools/sqlcmd-utility.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
  
## <a name="locate-the-transact-sql-reference-topics"></a>Transact-SQL のリファレンス トピックを見つける  
T-SQL のトピックを見つけるには、このページの右上にある検索ボックスを使用するか、ページの左側にある目次を使用します。 また、T-SQL のキーワードを Management Studio のクエリ エディター ウィンドウで入力して F1 キーを押すという方法もあります。 
  
## <a name="find-system-views"></a>システム ビューを見つける
システム テーブル、ビュー、関数、プロシージャを見つけるには、下記のリンクを参照してください。これらは、SQL のドキュメントの[リレーショナル データベースの使用](../relational-databases/databases/databases.md)のセクションにあります。

- [システム カタログ ビュー](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [システム互換性ビュー](../relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)
- [システム動的管理ビュー](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [システム関数](../relational-databases/system-functions/system-functions-category-transact-sql.md)
- [システム情報スキーマ ビュー](../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [システム ストアド プロシージャ](../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
- [システム テーブル](../relational-databases/system-tables/system-tables-transact-sql.md)

## <a name="applies-to-references"></a>"適用されます" リファレンス  
 T-SQL のリファレンス トピックは、SQL Server 2008 以降の複数のバージョンを対象としており、その他に Azure SQL のサービスも対象としています。 各トピックの先頭近くにあるセクションで、どの製品やサービスがそのトピックの説明対象をサポートしているかを示しています。 

たとえば、このトピックはすべてのバージョンに適用されるため、次のようなラベルが付いています。 
  
 [!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]   

次の例のラベルは、トピックが Azure Synapse Analytics と Parallel Data Warehouse だけに適用されることを示しています。

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../includes/applies-to-version/asa-pdw.md)]

場合によっては、トピックがある製品またはサービスで使用されていても、引数のすべてがサポートされているわけではないこともあります。 この場合は、別の "**適用されます**" セクションが、そのトピック本文中の該当する引数の説明の中に挿入されます。  
 
## <a name="get-help-from-microsoft-q--a"></a>Microsoft Q & A から支援を受ける  
オンラインで支援を受けるには、[Microsoft Q & A Transact-SQL フォーラム](/answers/topics/sql-server-transact-sql.html)を参照してください。  
 
## <a name="see-other-language-references"></a>その他の言語リファレンス
SQL のドキュメントには、他にも次のような言語リファレンスが含まれています。
  
- [XQuery 言語リファレンス](../xquery/xquery-language-reference-sql-server.md)
- [Integration Services 言語リファレンス](../integration-services/integration-services-language-reference.md)
- [レプリケーション言語リファレンス](../relational-databases/replication/replication-language-reference.md)
- [Analysis Services 言語リファレンス](../mdx/multidimensional-expressions-mdx-reference.md)  

## <a name="next-steps"></a>次のステップ
T-SQL のリファレンス トピックを見つける方法を理解したので、次のことができるようになりました。

- T-SQL を記述する方法を短いチュートリアルで学習します。「[チュートリアル: Transact-SQL ステートメントの作成](../t-sql/tutorial-writing-transact-sql-statements.md)」を参照してください。 
- 「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照します。  

  
