---
title: SQL にフラット ファイルをインポートする | Microsoft Docs
description: '[フラット ファイルのインポート] ウィザードを使用すると、.csv または .txt ファイルのデータを新しいデータベースのテーブルに簡単にコピーできます。 この記事では、このウィザードを使用する方法とタイミングを示します。'
ms.custom: ''
ms.date: 09/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: data-movement
ms.topic: conceptual
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
ms.reviewer: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68144fbcffdc2535471c279b5771963fcfb05fec
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868730"
---
# <a name="import-flat-file-to-sql-wizard"></a>SQL のフラット ファイルのインポート ウィザード
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
> インポートおよびエクスポート ウィザードに関連するコンテンツについては、「[SQL Server Import and Export Wizard](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」(SQL Server インポートおよびエクスポート ウィザード) を参照してください。

フラット ファイルのインポート ウィザードを使用すると、フラット ファイル (.csv、.txt) からデータベース内の新しいテーブルにデータを簡単にコピーできます。  フラット ファイルのインポート ウィザードでは、コンマ区切りと固定幅形式のファイルの両方がサポートされています。 この概要では、このウィザードを使用する理由、このウィザードを見つける方法、実行が簡単な例について説明します。

## <a name="why-would-i-use-this-wizard"></a>このウィザードを使用する理由
このウィザードは、Program Synthesis using Examples ([PROSE](https://microsoft.github.io/prose/)) と呼ばれるインテリジェント フレームワークを利用して現在のインポート操作を改善するために作成されました。 特殊なドメインの知識を持っていないユーザーの場合、データのインポートは複雑で、間違いやすく、面倒な作業になりがちです。 このウィザードでは、インポート プロセスが入力ファイルと一意のテーブル名を選択するだけの簡単な操作に整理され、後の処理は PROSE フレームワークが行います。

PROSE は、入力ファイルのデータ パターンを分析し、列の名前、型、区切り記号などを推定します。 このフレームワークはファイルの構造を学習し、ユーザーの代わりにすべての面倒な作業を実行します。

フラット ファイルのインポート ウィザードのユーザー エクスペリエンス改善の詳細については、このビデオをご覧ください。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>前提条件
この機能は、SQL Server Management Studio (SSMS) バージョン 17.3 以降で使用できます。 最新バージョンを使用していることを確認してください。 最新バージョンは[こちら](../../ssms/download-sql-server-management-studio-ssms.md)で入手できます。
 
## <a name="getting-started"></a><a id="started"></a>はじめに
フラット ファイルのインポート ウィザードにアクセスするには、次の手順を実行します。

1. **SQL Server Management Studio** を開きます。
2. SQL Server Database Engine または localhost のインスタンスに接続します。
3. **[データベース]** を展開し、データベース (下の例では test) を右クリックし、 **[タスク]** をポイントして、[データのインポート] の上の **[フラット ファイルのインポート]** をクリックします。

![ウィザードのメニュー](media/import-flat-file-wizard/import-flat-file-menu.png)

ウィザードの各機能の詳細については、次のチュートリアルを参照してください。

## <a name="tutorial"></a>チュートリアル
このチュートリアルには、任意のフラット ファイルを使うことができます。 自分のファイルを使わない場合は、このチュートリアルでは次の Excel の CSV 形式のファイルを使用します。自由にコピーしてください。 この CSV を使用する場合は、**example.csv** という名前を付けて、デスクトップなどの簡単な場所に csv ファイルとして保存してください。

![Excel のウィザード](media/import-flat-file-wizard/import-flat-file-example.png)

概要:
1. [ウィザードにアクセスする](#step-1-access-wizard-and-intro-page)
2. [入力ファイルを指定する](#step-2-specify-input-file)
3. [データをプレビューする](#step-3-preview-data)
4. [列を変更する](#step-4-modify-columns)
5. [まとめ](#step-5-summary)
6. [結果](#step-6-results)

### <a name="step-1-access-wizard-and-intro-page"></a>手順 1:ウィザードの [はじめに] ページにアクセスする
[こちら](#started)の手順に従ってウィザードにアクセスします。

ウィザードの最初のページは [ようこそ] ページです。 このページを再表示したくない場合は、 **[次回からこの開始ページを表示しない]** をクリックします。

![ウィザードの [はじめに]](media/import-flat-file-wizard/import-flat-file-intro.png)

### <a name="step-2-specify-input-file"></a>手順 2:入力ファイルを指定する
[参照] をクリックして入力ファイルを選択します。 ウィザードの既定で、.csv ファイルと .txt ファイルが検索されます。 PROSE によって、ファイル拡張子に関係なく、ファイルがコンマ区切りまたは固定幅形式であるかが検出されます。

新しいテーブル名は一意にする必要があります。一意ではない場合、ウィザードを次に進めることはできません。

![ウィザードの指定](media/import-flat-file-wizard/import-flat-file-specify.png)

### <a name="step-3-preview-data"></a>手順 3:データをプレビューする
プレビューが生成され、最初の 50 行を確認できます。 問題がある場合は [キャンセル] をクリックします。ない場合は、次のページに進みます。

![ウィザードのプレビュー](media/import-flat-file-wizard/import-flat-file-preview.png)

### <a name="step-4-modify-columns"></a>手順 4:列を変更する
ウィザードでは、列名、データ型などについて正しいと思われるものを特定します。ここでは、フィールドが正しくない場合に編集できます (たとえば、データ型が int ではなく float など)。

空の値が検出された列では、[Null を許容] がチェックされています。 ただし、null が想定される列で [Null を許容] がチェックされていない場合は、ここで 1 つまたはすべての列で null を許容するようにテーブル定義を更新できます。

準備ができたら次に進みます。

![ウィザードの変更](media/import-flat-file-wizard/import-flat-file-modify.png)

### <a name="step-5-summary"></a>手順 5:まとめ
これは、現在の構成が表示される概要ページです。 問題がある場合は、前のセクションに戻ることができます。 問題がない場合は、[完了] をクリックします。インポート プロセスが開始されます。

![ウィザードの概要](media/import-flat-file-wizard/import-flat-file-summary.png)

### <a name="step-6-results"></a>手順 6:結果
このページには、インポートが成功したかどうかが表示されます。 緑のチェック マークが表示される場合は成功です。それ以外の場合は、構成や入力ファイルに誤りがないか確認する必要があります。

![ウィザードの結果](media/import-flat-file-wizard/import-flat-file-results.png)

## <a name="troubleshooting"></a>トラブルシューティング
フラット ファイルのインポート ウィザードでは、最初の 200 行に基づいてデータ型が検出されます。  それ以降のフラット ファイルのデータが、自動検出されたデータ型に準拠していないシナリオでは、インポート中にエラーが発生します。 次のようなエラー メッセージが表示されます。
```
Error inserting data into table. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type nvarchar of the specified target column. (System.Data)
String or binary data would be truncated. (System.Data)
```
このエラーを軽減する方法:
- nvarchar 列の長さなど、「[列を変更する](#step-4-modify-columns)」ステップでデータ型のサイズを拡張すると、フラット ファイルの残りの部分でのデータの変化が補正される場合があります。
- 「[列を変更する](#step-4-modify-columns)」ステップでエラーの報告を有効にすると (特に、小さな数値で)、フラット ファイル内のどの行に、選択したデータ型に適合しないデータが含まれているかがわかります。 たとえば、2 番目の行でエラーが発生したフラット ファイルでは、範囲を 1 にしたエラー報告でインポートを実行すると、具体的なエラー メッセージが表示されます。  その場所でファイルを直接調べると、識別された行のデータに基づいて、さらに対象を絞ってデータ型を変更できます。

![エラー報告の結果](media/import-flat-file-wizard/import-flat-file-error.png)

```
Error inserting data into table occured while inserting rows 1 - 2. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type float of the specified target column. (System.Data)
Failed to convert parameter value from a String to a Double. (System.Data)
```


## <a name="learn-more"></a>詳細情報

ウィザードの詳細については、以下を参照してください。
 
- **その他のリソースのインポートに関する詳細**。 複数のフラット ファイルをインポートする場合は、「[SQL Server Import and Export Wizard](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」(SQL Server インポートおよびエクスポート ウィザード) を参照してください。
- **フラット ファイル ソースへの接続に関する詳細**。 フラット ファイル ソースへの接続の詳細については、「[Connect to a Flat File Data Source](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)」(フラット ファイル データ ソースへの接続) を参照してください。
- **PROSE の詳細**。 このウィザードに使用されるインテリジェント フレームワークの概要については、「[PROSE SDK](https://microsoft.github.io/prose/)」を参照してください。