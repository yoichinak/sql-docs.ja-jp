---
title: Transact-SQL エディターを使用したスクリプトの編集と実行
description: Transact-SQL エディターについて理解します。 エディターを開く方法について説明します。また、エディターのペインに表示される情報と、その機能に関するリソースを確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLEDITOR
- sql.data.tools.sqleditor
ms.assetid: fa78e2cf-3c64-49f5-93cc-a3d50b1e7d05
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 4c9bb76ddd3ee5f5c0828f5c9ef181f98e26f94d
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067074"
---
# <a name="use-transact-sql-editor-to-edit-and-execute-scripts"></a>Transact-SQL エディターを使用したスクリプトの編集と実行

Transact\-SQL エディターには、スクリプトの編集およびデバッグに役立つ豊富な機能が用意されています。 このエディターは、 **[コードの表示]** コンテキスト メニューを使用して、接続されているデータベースまたはプロジェクトのデータベース エンティティを開くと起動します。 SQL Server オブジェクト エクスプローラーの **[新しいクエリ]** コンテキスト メニューを使用するときと、データベース プロジェクトに新しいスクリプト オブジェクトを追加するときにも、このエディターが自動的に開きます。  
  
データベースに接続していない状態で、そのデータベースに対するクエリを実行する場合にも、 **[SQL]** -> **[Transact\-SQL エディター]** メニュー オプションの **[新しいクエリ接続]** ダイアログ ボックスを使用してデータベースに接続し、Transact\-SQL エディターを起動できます。  
  
Transact\-SQL エディターには、Transact\-SQL スクリプトの記述および編集を実行できる場所として、メインの **T-SQL** ペインがあります。 TSQL エディターでは、IntelliSense がサポートされているほか、複雑なステートメントを読みやすくするために、構文のカラー コーディング機能も用意されています。 また、検索と置換、一括コメントアウト、フォントと色のカスタマイズ、および行番号表示の機能も使用できます。 エディター内のスクリプトを実行する対象のデータベースを変更することもできます。 詳細については、「[既存のデータベースを複製する方法](../ssdt/how-to-clone-an-existing-database.md)」を参照してください。 **結果** ペインには、クエリ結果がグリッドまたはテキストとして表示されます。 クエリ結果をファイルにリダイレクトすることもできます。 **メッセージ** ペインには、スクリプトの実行時に返されるエラー、警告、および情報メッセージが表示されます。 クライアント統計が有効化されていると、クエリ実行に関する情報がカテゴリ別に **統計** ペインに表示されます。 **実行プラン** ペインには、SQL Server によって選択されたデータ取得方法が表示され、特定のステートメントまたはクエリの実行コストが示されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|---------|---------------|  
|[方法:  スニペットをアウトライン表示し、Transact-SQL スクリプトに追加する](../ssdt/how-to-outline-and-add-snippets-to-transact-sql-script.md)|スニペット ピッカーを使用して、あらかじめ用意されている Transact\-SQL コードをクエリに挿入します。|  
|[方法:  スクリプト間を移動する](../ssdt/how-to-navigate-between-scripts.md)|[定義へ移動] と [すべての参照の検索] を使用してスクリプト間を移動します。|  
|[方法:  名前の変更とリファクタリングを使用して、データベース オブジェクトを変更する](../ssdt/how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects.md)|すべてのスクリプトでオブジェクトの名前を変更し、変更のプレビューを確認します。|  
|[方法:  部分クエリを実行する](../ssdt/how-to-execute-a-partial-query.md)|スクリプトの一部を選択し、その部分を単一のクエリとして実行します。|  
|[方法:  ストアド プロシージャをデバッグする](../ssdt/how-to-debug-stored-procedures.md)|Transact\-SQL ストアド プロシージャを作成し、ステップ インでデバッグします。|  
|[スクリプトのパフォーマンス分析](../ssdt/analyze-script-performance.md)|実行プラン、クライアント統計、およびコード分析を使用して、クエリ、ストアド プロシージャ、またはスクリプトのパフォーマンスを向上できるかどうかを判定します。|  
  
## <a name="see-also"></a>参照

[方法:  クエリを使用して新しいデータベース オブジェクトを作成する](../ssdt/how-to-create-new-database-objects-using-queries.md)