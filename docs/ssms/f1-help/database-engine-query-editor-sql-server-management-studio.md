---
title: SSMS クエリ エディター
description: SQL Server Management Studio (SSMS) クエリ エディター
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.query.advanced.f1
- sql13.swb.query.ansi.f1
- sql13.swb.query.general.f1
- sql13.swb.query.grid.f1
- sql13.swb.sqleditors.multiserverresultssettings
- sql13.swb.tsqlquery.f1
- sql13.swb.tsqlresults.f1
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], editor
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
- SQL Server Management Studio [SQL Server], templates
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio]
- Query Editor [Database Engine]
- Query Editor [Database Engine], Features
- Query Editor [Database Engine], Toolbar
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- Query Editor [SQL Server Management Studio], about Query Editor
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Code Editor [SQL Server Management Studio], about Query Editor
- editors [SQL Server Management Studio], Database Engine Query Editor
- full screen mode [SQL Server Management Studio]
- writing scripts
- modifying scripts
- writing queries
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019, contperfq1
ms.date: 08/28/2020
ms.openlocfilehash: 7450a77549d05dab5a024b39be6d2b4aef6c09de
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364848"
---
# <a name="sql-server-management-studio-ssms-query-editor"></a>SQL Server Management Studio (SSMS) クエリ エディター

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

この記事では、SQL Server Management Studio (SSMS) のクエリ エディターの機能について説明します。

> [!Note]
> Transact-SQL (T-SQL) の F1 ヘルプの使用方法については、「[Transact-SQL F1 ヘルプ](#transact-sql-f1-help)」のセクションをご覧ください。
>
> エディターで処理できるタスクを理解する場合は、「[エディターのタスク](#editor-tasks)」のセクションをご覧ください。

SSMS のエディターは、一般的なアーキテクチャを共有します。 テキスト エディターは基本的なレベルの機能を実装し、テキスト ファイル用の基本的なエディターとして使用できます。 それ以外のエディター (クエリ エディター) は、SQL Server でサポートされるいずれかの言語の構文を定義する言語サービスを追加することで、この機能ベースを拡張したものです。 クエリ エディターには、IntelliSense やデバッグなど、さまざまなエディター機能が実装されています。 クエリ エディターには、データベース エンジン クエリ エディター (T-SQL および XQuery ステートメントを含んだスクリプトの作成用)、MDX エディター (MDX 言語用)、DMX エディター (DMX 言語用)、および XML/A エディター (XML for Analysis 言語用) があります。
クエリ エディターを使用して、Transact-SQL ステートメントを含むスクリプトの作成と実行を行えます。

![[新しいクエリ]](media/database-engine-query-editor-sql-server-management-studio/new-query.png)

## <a name="sql-editor-toolbar"></a>SQL エディター ツール バー

クエリ エディターが開いているときは、次のボタンを持つ SQL エディター ツール バーが表示されます。

また、 **[表示]** メニューの **[ツール バー]** を選択し、 **[SQL エディター]** を選択して、SQL エディター ツール バーを追加することもできます。 クエリ エディターのウィンドウが開いていない状態で SQL エディター ツール バーを追加した場合、すべてのボタンが使用できなくなります。

![エディター ツール バー](media/database-engine-query-editor-sql-server-management-studio/editor-toolbar.png)

### <a name="connect-using-the-editor-toolbar"></a>エディター ツール バーを使用した [接続]

**[[サーバーへの接続]](connect-to-server-database-engine.md)** ダイアログ ボックスが開きます。 このダイアログ ボックスを使用すると、サーバーへの接続を確立できます。

[コンテキスト メニュー](#connection-using-the-context-menu)を使用してデータベースに接続することもできます。

### <a name="change-connection-using-the-editor-toolbar"></a>エディター ツール バーを使用した [接続の変更]

**[サーバーへの接続]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、[別のサーバーへの接続](f1-help-for-server-connections-sql-server-management-studio.md)を確立できます。

[コンテキスト メニュー](#connection-using-the-context-menu)を使用して接続を変更することもできます。

### <a name="available-databases-using-the-editor-toolbar"></a>エディター ツール バーを使用した [使用できるデータベース]

接続を同じサーバー上の別のデータベースに変更します。

### <a name="execute-using-the-editor-toolbar"></a>エディター ツール バーを使用した [実行]

選択されているコードを実行します。コードが選択されていない場合は、すべてのクエリ エディター コードを実行します。

F5 キーを押すか、 [コンテキスト メニュー](#execute-using-the-context-menu)から選択してクエリを **実行** することもできます。

### <a name="cancel-executing-query-using-the-editor-toolbar"></a>エディター ツール バーを使用した [クエリ実行のキャンセル]

キャンセル要求をサーバーに送信します。 即座にキャンセルできないクエリもあります。そのようなクエリは、適切なキャンセル条件が整うまでキャンセルできません。 トランザクションが取り消されると、トランザクションがロールバックされる間に遅延が発生することがあります。

Alt + Break キー押して、実行中のクエリをキャンセルすることもできます。

### <a name="parse-using-the-editor-toolbar"></a>エディター ツール バーを使用した [解析]

選択されているコードの構文をチェックします。 コードが選択されていない場合は、クエリ エディター ウィンドウ内のすべてのコードの構文がチェックされます。

また、Ctrl + F5 キーを押すことで、クエリ エディターでコードをチェックすることもできます。

### <a name="display-estimated-execution-plan-using-the-editor-toolbar"></a>エディター ツール バーを使用した [推定実行プランの表示]

クエリを実行することなくクエリ プロセッサからクエリ実行プランを要求し、プランを **[実行プラン]** ウィンドウに表示します。 このプランでは、インデックス統計を使用して、クエリ実行中の各部分で返される行数が推定されます。 実際に使用されるクエリ プランは、推定実行プランとは異なる場合があります。 返される行数が推定値と異なり、クエリ プロセッサによってプランが効率化される場合に、この状況が発生する可能性があります。

推定実行プランを表示するには、Ctrl + L キーを押すか、[コンテキスト メニュー](#display-estimated-execution-plan-using-the-context-menu)から選択することもできます。

### <a name="query-options-using-the-editor-toolbar"></a>エディター ツール バーを使用した [クエリ オプション]

**[クエリ オプション]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、クエリの実行およびクエリ結果に関する既定のオプションを構成できます。

**[クエリ オプション]** は、 [コンテキスト メニュー](#query-options-using-the-context-menu)から選択することもできます。

### <a name="intellisense-enabled-using-the-editor-toolbar"></a>エディター ツール バーを使用した [IntelliSense 有効]

データベース エンジン クエリ エディターで、[IntelliSense](../scripting/configure-intellisense-sql-server-management-studio.md) 機能が使用できるかどうかを示します。 このオプションは、既定で設定されています。

**[IntelliSense 有効]** を選択するには、Ctrl + B キーを押した後、Ctrl + I キーを押すか、 [コンテキスト メニュー](#intellisense-enabled-using-the-context-menu)から選択することもできます。

### <a name="include-actual-execution-plan-using-the-editor-toolbar"></a>エディター ツール バーを使用した [実際の実行プランを含める]

クエリを実行し、クエリ結果を返し、クエリに対して実行プランを使用します。 クエリは、グラフィカルなクエリ プランとして **[実行プラン]** ウィンドウに表示されます。

**[実際の実行プランを含める]** を選択するには、Ctrl + M キーを押すか、 [コンテキスト メニュー](#include-actual-execution-plan-using-the-context-menu)から選択することもできます。

### <a name="include-live-query-statistics-using-the-editor-toolbar"></a>エディター ツール バーを使用した [ライブ クエリ統計を含む]

クエリ プラン演算子間の制御フローとして、クエリ実行プロセスのリアルタイムの分析情報を提供します。

**[ライブ クエリ統計を含む]** は、 [コンテキスト メニュー](#include-live-query-statistics-using-the-context-menu)から選択することもできます。

### <a name="include-client-statistics-using-the-editor-toolbar"></a>エディター ツール バーを使用した [クライアント統計情報を含める]

クエリおよびネットワーク パケットに関する統計、およびクエリの経過時間を表示する **[クライアント統計]** ウィンドウを含めます。

**[ライブ クエリ統計を含む]** は、Shift + Alt + S キーを押すか、 [コンテキスト メニュー](#include-client-statistics-using-the-context-menu)から選択することもできます。

### <a name="results-to-text-using-the-editor-toolbar"></a>エディター ツール バーを使用した [結果をテキストで表示]

クエリ結果をテキストとして **[結果]** ウィンドウに表示します。

結果をテキストで返すには、Ctrl + T キーを押すか、[コンテキスト メニュー](#results-using-the-context-menu)から選択することもできます。

### <a name="results-to-grid-using-the-editor-toolbar"></a>エディター ツール バーを使用した [結果をグリッドに表示]

クエリ結果を 1 つまたは複数のグリッドとして **[結果]** ウィンドウに表示します。 既定では、このオプションは有効になっています。

結果をテキストで返すには、Ctrl + D キーを押すか、[コンテキスト メニュー](#results-using-the-context-menu)から選択することもできます。

### <a name="results-to-file-using-the-editor-toolbar"></a>エディター ツール バーを使用した [結果をファイルに出力]

クエリを実行したときに、 **[結果の保存]** ダイアログ ボックスが開きます。 ファイルを保存するフォルダーを **[保存先]** で選択します。 **[ファイル名]** にファイルの名前を入力し、 **[保存]** を選択して、拡張子 .rpt を持つ **レポート** ファイルとしてクエリ結果を保存します。 詳細設定オプションを指定するには、 **[保存]** ボタンの下向き矢印を選択し、 **[エンコード付きで保存]** を選択します。

結果をテキストで返すには、Ctrl + Shift + F キーを押すか、[コンテキスト メニュー](#results-using-the-context-menu)から選択することもできます。

### <a name="comment-out-the-selected-lines-using-the-editor-toolbar"></a>エディター ツール バーを使用して、選択した行をコメント アウトする

行の先頭にコメント演算子 (--) を追加することで、現在の行をコメントにします。

Ctrl + K キーを押してから Ctrl + C キーを押しても、行をコメント アウトすることができます。

### <a name="uncomment-the-selected-lines-using-the-editor-toolbar"></a>エディター ツール バーを使用して、選択した行をコメント解除する

行の先頭にあるコメント演算子 (--) をすべて削除することで、現在の行をアクティブなソース ステートメントにします。

Ctrl + K キーを押してから Ctrl + U キーを押しても、行をコメント解除することができます。

### <a name="decrease-indent-using-the-editor-toolbar"></a>エディター ツール バーを使用した [インデント解除]

行の先頭にある空白を削除することで、行のテキストを左方向へ移動します。

### <a name="increase-line-indent-using-the-editor-toolbar"></a>エディター ツール バーを使用した [行インデント]

行の先頭に空白を追加することで、行のテキストを右方向へ移動します。

### <a name="specify-values-for-template-parameters-using-the-editor-toolbar"></a>エディター ツール バーを使用した [テンプレート パラメーターの値の指定]

ストアド プロシージャや関数のパラメーター値を指定するためのダイアログ ボックスを開きます。

## <a name="context-menu"></a>コンテキスト メニュー

コンテキスト メニューにアクセスするには、クエリ エディター内の任意の場所で *右クリック* します。 コンテキスト メニュー内のオプションは、SQL エディター ツール バーと同様です。 コンテキスト メニューでは、 **[接続]** および **[実行]** と同じオプションが表示されますが、 **[スニペットの挿入]** や **[ブロックの挿入]** などの他のオプションも表示されます。

![オプション](media/database-engine-query-editor-sql-server-management-studio/context-menu.png)

### <a name="insert-snippet-using-the-context-menu"></a>コンテキスト メニューを使用した [スニペットの挿入]

[T-SQL コード スニペット](../scripting/add-transact-sql-snippets.md)は、クエリ エディターで新しい Transact-SQL ステートメントを作成する際の開始点として使用できるテンプレートです。

### <a name="surround-with-using-the-context-menu"></a>コンテキスト メニューを使用した [ブロックの挿入]

ブロックの挿入スニペットは、BEGIN、IF、または WHILE ブロックで一連の Transact-SQL ステートメントを囲むときに出発点として使用できるテンプレートです。

### <a name="connection-using-the-context-menu"></a>コンテキスト メニューを使用した [接続]

![接続](media/database-engine-query-editor-sql-server-management-studio/context-menu-connections.png)

コンテキスト メニューには、SSMS のツール バー オプションと比較してより多くの **[接続]** オプションがあります。

- **[接続]** - [サーバーへの接続] ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、サーバーへの接続を確立できます。

- **[接続解除]** - 現在のクエリ エディターをサーバーから接続解除します。

- **[すべてのクエリの切断]** - すべてのクエリ接続を切断します。

- **[接続の変更]** - [サーバーへの接続] ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、別のサーバーへの接続を確立できます。

### <a name="open-server-in-object-explorer-using-the-context-menu"></a>コンテキスト メニューを使用してオブジェクト エクスプローラーでサーバーを開く

オブジェクト エクスプローラーは、SQL Server の各インスタンスのオブジェクトを表示し、管理するための階層形式のユーザー インターフェイスを備えています。 [オブジェクト エクスプローラーの詳細] ペインには、インスタンス オブジェクトの表形式のビューと、特定のオブジェクトを検索する機能が用意されています。 オブジェクト エクスプローラーの機能は、サーバーの種類によって多少異なりますが、データベースの開発機能と管理機能は、基本的にサーバーの種類にかかわりなく用意されています。

### <a name="execute-using-the-context-menu"></a>コンテキスト メニューを使用した [実行]

選択されているコードを実行します。コードが選択されていない場合は、クエリ エディター内のコード全体を実行します。

### <a name="display-estimated-execution-plan-using-the-context-menu"></a>コンテキスト メニューを使用した [推定実行プランの表示]

実際にクエリを実行することなくクエリ プロセッサからクエリ実行プランを要求し、プランを **[実行プラン]** ウィンドウに表示します。 このプランでは、インデックス統計を使用して、クエリ実行中の各部分で返される行数が推定されます。 実際に使用されるクエリ プランは、推定実行プランとは異なる場合があります。 返される行数が推定値と異なり、クエリ プロセッサによってプランが効率化される場合に、この状況が発生する可能性があります

### <a name="intellisense-enabled-using-the-context-menu"></a>コンテキスト メニューを使用した [IntelliSense 有効]

データベース エンジン クエリ エディターで、IntelliSense 機能が使用できるかどうかを示します。 このオプションは、既定で設定されています。

### <a name="trace-query-in-sql-server-profiler-using-the-context-menu"></a>コンテキスト メニューを使用した [SQL Server Profiler でクエリをトレース]

SQL Server Profiler は、トレースを作成および管理し、トレースの結果を分析および再生するためのインターフェイスです。 イベントはトレース ファイルに保存され、後で分析したり、問題の発生したステップを厳密に再現して診断する際に利用できます。

### <a name="analyze-query-in-database-engine-tuning-advisor-using-the-context-menu"></a>コンテキスト メニューを使用した [データベース エンジン チューニング アドバイザーでのクエリの分析]

Microsoft データベース エンジン チューニング アドバイザー (DTA) は、データベースを分析し、クエリ パフォーマンスの最適化に役立つ推奨事項を示します。 データベースの構造や SQL Server の内部構造に関する専門的な知識がなくても、データベース エンジン チューニング アドバイザーを使用して、インデックス、インデックス付きビュー、テーブル パーティション分割の最適な組み合わせを選択し作成します。 DTA を使用して、次の作業を実行できます。

### <a name="design-query-in-editor-using-the-context-menu"></a>コンテキスト メニューを使用した [エディターでクエリをデザイン]

ビューの定義を開いたり、クエリまたはビューの結果を表示したり、クエリを作成したり開いたりすると、クエリおよびビュー デザイナーが開きます。

### <a name="include-actual-execution-plan-using-the-context-menu"></a>コンテキスト メニューを使用した [実際の実行プランを含める]

クエリを実行し、クエリ結果を返し、クエリに対して実行プランを使用します。 クエリは、グラフィカルなクエリ プランとして **[実行プラン]** ウィンドウに表示されます。

### <a name="include-live-query-statistics-using-the-context-menu"></a>コンテキスト メニューを使用した [ライブ クエリ統計を含む]

クエリ プラン演算子間の制御フローとして、クエリ実行プロセスのリアルタイムの分析情報を提供します。

### <a name="include-client-statistics-using-the-context-menu"></a>コンテキスト メニューを使用した [クライアント統計情報を含める]

クエリおよびネットワーク パケットに関する統計、およびクエリの経過時間を表示する **[クライアント統計]** ウィンドウを含めます。

### <a name="results-using-the-context-menu"></a>コンテキスト メニューを使用した [結果]

![結果オプション](media/database-engine-query-editor-sql-server-management-studio/context-menu-results.png)

コンテキスト メニューから、任意の " *結果* " オプションを選択できます。

- **[結果をテキストで表示]** - クエリ結果をテキストとして **[結果]** ウィンドウに表示します。

- **[結果をグリッドに表示]** - クエリ結果を 1 つまたは複数のグリッドとして **[結果]** ウィンドウに表示します。

- **[結果をファイルに出力]** - クエリを実行したときに、 **[結果の保存]** ダイアログ ボックスが開きます。 ファイルを保存するフォルダーを **[保存先]** で選択します。 **[ファイル名]** にファイルの名前を入力し、 **[保存]** を選択して、拡張子 .rpt を持つ **レポート** ファイルとしてクエリ結果を保存します。 詳細設定オプションを指定するには、 **[保存]** ボタンの下向き矢印を選択し、 **[エンコード付きで保存]** を選択します。

### <a name="properties-window-using-the-context-menu"></a>コンテキスト メニューを使用したプロパティ ウィンドウ

[プロパティ ウィンドウ](../menu-help/properties-window-f1-help-management-studio.md)には、SQL Server Management Studio 内の項目 (接続、プラン表示操作など) の状態や、データベース オブジェクト (テーブル、ビュー、デザイナーなど) の情報が表示されます。

[プロパティ] ウィンドウを使用して、現在の接続のプロパティを表示します。 プロパティ ウィンドウに表示される多くのプロパティは読み取り専用ですが、Management Studio 内の別の場所で変更できます。 たとえば、[プロパティ] ウィンドウに表示されるクエリの [データベース] プロパティは読み取り専用ですが、ツール バーからの変更が可能です。

### <a name="query-options-using-the-context-menu"></a>コンテキスト メニューを使用した [クエリ オプション]

**[クエリ オプション]** ダイアログ ボックスを開きます。 このダイアログ ボックスを使用すると、クエリの実行およびクエリ結果に関する既定のオプションを構成できます。

## <a name="transact-sql-f1-help"></a>Transact-SQL F1 ヘルプ

クエリ エディターは F1 ヘルプをサポートしており、特定の Transact-SQL ステートメントから、関連するリファレンス トピックに移動することができます。 それには、Transact-SQL ステートメントの名前を強調表示し、F1 キーを押します。 強調表示した文字列と一致する F1 ヘルプ属性を持ったトピックが、ヘルプの検索エンジンによって検索されます。

強調表示した文字列と完全に一致する F1 ヘルプ キーワードに該当するトピックが見つからなかった場合は、このトピックが表示されます。 その場合は、次の 2 つの方法で、目的のヘルプを探すことができます。

- 強調表示した文字列をエディターからコピーし、SQL Server オンライン ブックの検索タブに貼り付けて検索を実行します。

- Transact-SQL ステートメントで、トピックに適用されている F1 ヘルプ キーワードと一致しそうな部分を強調表示してから再度 F1 キーを押します。 トピックに割り当てられている F1 ヘルプ キーワードと強調表示した文字列とが完全に一致している必要があります。 強調表示した文字列に、列名やパラメーター名など、特定の環境にしか存在しないような要素が含まれていると、検索エンジンで一致が見つかりません。 強調表示する文字列の例を次に示します。

  - Transact-SQL ステートメントの名前 (SELECT、CREATE DATABASE、BEGIN TRANSACTION など)。

  - 組み込み関数の名前 (SERVERPROPERTY、@@VERSION など)。

  - システム ストアド プロシージャのテーブル名やビュー名 (sys.data_spaces、sp_tableoption など)。

## <a name="editor-tasks"></a>エディターのタスク

| タスクの説明 | トピック |
|------------------|-------|
| SSMS でエディターを開くための、さまざまな方法について説明します。| [エディターを開く](../scripting/open-an-editor-sql-server-management-studio.md) |
| 行番号表示や IntelliSense オプションなど、各種エディターのオプションを構成します。 | [エディターの構成](../scripting/configure-editors-sql-server-management-studio.md) |
| 右端での折り返し、ウィンドウの分割、タブなど、各種表示モードを管理する方法。| [エディターと表示モードの管理](../scripting/manage-the-editor-and-view-mode.md) |
| テキストの非表示やインデントなど、書式設定オプションを設定します。 | [コードの書式設定の管理](../scripting/manage-code-formatting.md) |
| インクリメンタル検索やジャンプなどの機能を使用して、エディター ウィンドウ内でテキストを検索します。 | [コード内とテキスト内の移動](../scripting/navigate-code-and-text.md) |
| さまざまな構文の分類に対して色分けオプションを設定し、複雑なステートメントを見やすく表示します。 | [クエリ エディターでのコードの色分け](../scripting/color-coding-in-query-editors.md) |
| スクリプト内でドラッグ アンド ドロップによってテキストを移動します。| [テキストのドラッグ アンド ドロップ](../scripting/drag-and-drop-text.md) |
| コードの重要箇所を見つけやすいようにブックマークを設定します。 | [ブックマークの管理](../scripting/manage-bookmarks.md) |
| スクリプトまたはその結果をウィンドウまたはグリッドから印刷します。| [コードと結果の印刷](../scripting/print-code-and-results.md) |
| MDX クエリ エディターの基本的な機能を表示し、使用します。 | [Analysis Services スクリプトの作成](/analysis-services/instances/create-analysis-services-scripts-in-management-studio) |
| DMX クエリ エディターの基本的な機能を表示し、使用します。 | [DMX クエリの作成](/analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio) |
| XML/A エディターの基本的な機能を表示し、使用します。 | [XML エディター](../scripting/xml-editor-sql-server-management-studio.md) |
| データベース エンジン クエリ エディターで sqlcmd の機能を使用する方法。| [SQLCMD スクリプトの編集](../scripting/edit-sqlcmd-scripts-with-query-editor.md) |
| データベース エンジン クエリ エディターでのコード スニペットの使用方法。 スニペットは、使用頻度の高いステートメントまたはブロックのテンプレートです。特定用途のスニペットを追加して拡張したりカスタマイズしたりすることができます。| [T-SQL コード スニペット](../scripting/add-transact-sql-snippets.md) |
| Transact\-SQL デバッガーを使用してコードをステップ実行したり、デバッグ情報 (変数やパラメーターの値など) を表示したりします。| [T-SQL デバッガー](../scripting/transact-sql-debugger.md) |

## <a name="see-also"></a>関連項目

- [メニューとショートカット キーのカスタマイズ](../customize-menus-and-shortcut-keys.md)
- [SQL Server Management Studio のキーボード ショートカット](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)