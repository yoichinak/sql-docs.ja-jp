---
description: Teradata ソースに接続する
title: Teradata ソースに接続する | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b4e64c2d7ada0db923f1aa623576e7b2994d8e6
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127952"
---
# <a name="connect-to-the-teradata-source"></a>Teradata ソースに接続する

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Teradata ソースでは、次を使用して Teradata データベースからデータが抽出されます。
- テーブルまたはビュー。
- SQL ステートメントの結果。

ソースでは、Teradata 接続マネージャーを使用して Teradata ソースに接続します。 詳細については、「[Teradata 接続マネージャーの使用](teradata-connection-manager.md)」を参照してください。

## <a name="troubleshoot-the-teradata-source"></a>Teradata ソースのトラブルシューティング

Teradata ソースから Teradata Parallel Transporter (TPT) API への呼び出しをログに記録できます。 これを行うには、パッケージのログ記録を有効にし、パッケージ レベルで **診断** イベントを選択します。

Teradata ソースから Teradata ODBC ドライバーへの Open Database Connectivity (ODBC) の呼び出しをログに記録するには、ODBC ドライバー マネージャーのトレースを有効にします。 詳細については、[ODBC データ ソース アドミニストレーターを使用して ODBC トレースを生成する方法](../../odbc/admin/setting-tracing-options.md)に関するページを参照してください。

## <a name="parallelism"></a>Parallelism

Teradata ソースでは、並列処理がサポートされているため、エクスポート ジョブが同じテーブルまたは別のテーブルに同時にアクセスできます。 `MaxLoadTasks` というデータベース変数により、同時に実行できるエクスポート ジョブ数の制限が設定されます。 この最大数は、`MaxLoadTasks` 変数を使用して定義できます。

## <a name="teradata-source-custom-properties"></a>Teradata ソースのカスタム プロパティ

次の表に、Teradata ソースのカスタム プロパティの一覧を示します。 すべてのプロパティは読み取り/書き込み可能です。

|プロパティ名|データ型|説明|
|:-|:-|:-|
|AccessMode|Integer (列挙)|データベースへのアクセスに使用するモード。 指定できる値は、 *[テーブル名]* と *[SQL コマンド]* です。 既定値は *Table Name* です。|
|BlockSize|Integer|クライアントにデータを返すときに使用されるブロック サイズ (バイト単位)。 既定値は 1048576 (1 MB) です。 最小値は 256 バイトです。 最大値は 16775168 バイトです。<br> このプロパティは、**[詳細エディター]** ペインにあります。|
|BufferMaxSize|Integer|GetBuffer 関数によって返されるデータ バッファーの最大サイズの合計。 このサイズは、行ヘッダー、実際のデータ行、バッファー トレーラーなど、少なくとも 1 行のデータを保持するのに十分な大きさである必要があります。 データ バッファーの既定の最大合計サイズは 16775552 バイトです。 <br>詳細については、「[Export data from a Teradata database by using GetBuffer](https://docs.teradata.com/reader/TvVKKmxaBAoyETJZD8zz_g/oaxiwNJmnCa6UctY4k498w)」 (GetBuffer を使用して Teradata データベースからデータをエクスポートする) を参照してください。|
|BufferMode|ブール型|既定値は *True* です。 PutBuffer 機能が使用されている場合、値は *True* にする必要があります。 このプロパティは、**[詳細エディター]** ペインにあります。|
|DataEncryption|ブール型|既定値は *False* です。 値が *True* の場合は、完全セキュリティ暗号化が使用されます。|
|DefaultCodePage|Integer|データ ソースにコード ページ情報がない場合に使用されるコード ページ。 このプロパティは、**[詳細エディター]** ペインにあります。|
|DetailedTracingLevel|Integer (列挙)|詳細トレースに対して、次のいずれかのオプションを選択します。 <br> *Off*:詳細ログは記録されません。 <br> *General*:ドライバー固有のアクティビティの一般的なトレースがログに記録されます。 <br> *CLI*:CLIv2 に関連するアクティビティのトレースがログに記録されます。 <br> *Notify Method*:通知機能に関連するアクティビティのトレースがログに記録されます。 <br> *Common Library*: opcommon ライブラリ アクティビティのトレースがログに記録されます。 <br> *[すべて]* : 上記のすべてのアクティビティのトレースがログに記録されます。 <br> 詳細トレース ログ ファイルは、`DetailedTracingFile` プロパティで定義されています。 <br> オプションが *Off* になっていない場合は、`DetailedTracingFile` プロパティを設定する必要があります。 このプロパティは、**[詳細エディター]** ペインにあります。|
|DetailedTracingFile|String|*DetailedTracingLevel* が *Off* になっていない場合に、自動的に生成されるログ ファイルのパス。 このプロパティは、**[詳細エディター]** ペインにあります。|
|DiscardLargeRow|ブール型|既定値は *False* です。 値が *True* の場合は、大きい行 (64 KB より大きい) が破棄されます。|
|ExtendedStringColumnsAllocation|ブール型|値が *True* の場合、*Maximal Transfer Character Allocation Factor* が使用されます。 <br> Teradata データベースの `Export Width Table ID` プロパティが *Maximal Defaults* に設定されている場合は、この値を *True* に設定する必要があります。 <br> 既定値は *False* です。|
|JobMaxRowSize|Integer|行の最大サイズをサポートできます。 `DiscardLargeRow` 値が *True* の場合は、この値が必要です。<br>有効な値: <br>*64* (既定値):2 バイトの行の長さをサポートできます。 <br>*1024*:4 バイトの行の長さをサポートできます。|
|MaxSessions|Integer|ログインされているセッションの最大数。 この値は、1 より大きくする必要があります。 既定値は、使用可能な Access Module Processor (AMP) ごとに 1 つのセッションです。|
|MinSessions|Integer|ログインされているセッションの最小数。 この値は、1 より大きくする必要があります。 既定値は、使用可能な AMP ごとに 1 つのセッションです。|
|QueryBandSessInfo|Varchar|ユーザー定義のセッションベースのクエリ バンド式 (接続文字列形式)。 このプロパティは、チャージバックの監視とガバナンスに使用します。 このプロパティは、**[詳細エディター]** ペインにあります。|
|SpoolMode|Varchar|有効な値は次のとおりです。 <br>*Spool*:既定値 *Spool* を使用します。 <br> *NoSpool*:*Spool* は使用しないでください。 この値は、データベース サーバー (DBS) で *NoSpool* がサポートされている場合にのみ有効です。 <br>  *NoSpoolOnly*:どのような場合でも *Spool* は使用しないでください。 DBS で *NoSpool* がサポートされていない場合、ジョブはエラーで終了します。|
|SqlCommand|String|`AccessMode` が *SQL Command* に設定されている場合に実行される SQL コマンド。|
|TableName|String|`AccessMode` が *Table Name* に設定されている場合に使用されるデータを含むテーブルの名前。|
|TenacityHours|Integer|読み込み操作またはエクスポート操作の最大数が既に実行されている場合に、TPT ドライバーがログインを試行する時間数。 既定値は *4 hours* です。 このプロパティは、**[詳細エディター]** ペインにあります。|
|TenacitySleep|Integer|TPT ドライバーが制限に達したときにログインを試行する前に一時停止する時間 (分単位)。 この制限は、`MaxSessions` プロパティと `TenacityHours` プロパティによって定義されます。 既定値は 6 分です。 このプロパティは、**[詳細エディター]** ペインにあります。|
|UnicodePassThrough|ブール型|*Off* (既定値):Unicode パススルーを無効にします。 <br>*更新日時*:Unicode パススルーを有効にします。|

## <a name="configure-the-teradata-source"></a>Teradata ソースを構成する

Teradata ソースは、プログラムによって、または SQL Server Integration Services (SSIS) デザイナーを使用して構成できます。

次の図は、**[Teradata ソース エディター]** ペインを示しています。 詳細については、次の Teradata ソース エディターの各セクションを参照してください。

- [[接続マネージャー] ペイン](#the-connection-manager-pane)
- [[列] ペイン](#the-columns-pane)
- [[エラー出力] ペイン](#the-error-output-pane)

![Teradata ソース エディター](media/teradata-source.png)

**[詳細エディター]** ペインには、プログラムによって設定できるプロパティが含まれます。 ペインを開くには:
- Integration Services プロジェクトの **[データ フロー]** ページで、Oracle ソースを右クリックし、**[詳細エディターの表示]** を選択します。

**[詳細エディター]** ペインで設定できるプロパティの詳細については、「[Teradata ソースのカスタム プロパティ](#teradata-source-custom-properties)」を参照してください。

## <a name="the-connection-manager-pane"></a>[接続マネージャー] ペイン

**[接続マネージャー]** ペインを使用して、ソースの Teradata 接続マネージャー インスタンスを選択します。 このペインでは、データベースからテーブルまたはビューを選択することもできます。 ペインを開くには:

1. SQL Server Data Tools で、Teradata ソースを含む SSIS パッケージを開きます。

1. **[データ フロー]** タブで、Teradata ソースをダブルクリックします。

1. Teradata ソース エディターで、**[接続マネージャー]** タブを選択します。

### <a name="options"></a>Options

**Connection manager**

* 一覧から既存の接続マネージャーを選択するか、**[新規作成]** を選択して新しい Teradata 接続マネージャー インスタンスを作成します。

**[新規作成]**

* **[新規]** を選択します。 **[Teradata 接続マネージャー エディター]** ペインが開きます。 このペインから、新しい接続マネージャーを作成できます。

**データ アクセス モード**

* ソースからデータを選択する方法を選択します。 次の表に示すオプションがあります。

    |オプション|説明|
    |:-|:-|
    |テーブル名 - TPT Export|Teradata データ ソースのテーブルまたはビューからデータを取得します。 このオプションを選択した場合、使用できるテーブルまたはビューを **[テーブル名またはビュー名]** の一覧から選択します。|
    |SQL コマンド - TPT Export|SQL クエリを使用して、Teradata データ ソースからデータを取得します。 このオプションを選択した場合は、以下のいずれかの方法でクエリを入力します。 <ul><li>**[SQL コマンド テキスト]** フィールドに SQL クエリのテキストを入力します。</li><li>**[参照]** を選択して、テキスト ファイルから SQL クエリを読み込みます。</li><li>**[クエリの解析]** を選択して、クエリ テキストの構文を検証します。</li></ul>|

**プレビュー**

* **[プレビュー]** を選択すると、選択したテーブルまたはビューから抽出されたデータを先頭から最大で 200 行表示できます。

## <a name="the-columns-pane"></a>[列] ペイン

**[列]** ペインを使用すると、出力列をそれぞれの外部 (ソース) 列にマップできます。 ペインを開くには:

1. SQL Server Data Tools で、Teradata ソースを含む SSIS パッケージを開きます。

1. **[データ フロー]** タブで、Teradata ソースをダブルクリックします。

1. Teradata ソース エディターで、**[列]** タブを選択します。

### <a name="options"></a>オプション

**使用できる外部列**

次の表に、**[外部列]** の一覧に追加するように選択できる使用可能な外部列を示します。 選択した順序で列を一覧表示できます。 このテーブルを使用して列を追加または削除することはできません。

* すべての列を選択するには、**[すべて選択]** チェック ボックスを選択します。

**外部列**

選択した外部 (ソース) 列が順序どおりに一覧表示されます。 順序を変更するには、まず **[使用できる外部列]** の一覧をクリアしてから、別の順序で列を選択します。

**出力列**

選択した外部 (ソース) 列の名前は既定の出力名ですが、任意の一意の名前を入力できます。

>[!NOTE]
>>サポートされていないデータ型を含む列がある場合、サポートされていないデータ型を表示する警告が表示され、関連する列がマッピング列から削除されます。

## <a name="the-error-output-pane"></a>[エラー出力] ペイン

**[エラー出力]** ペインを使用して、エラー処理オプションを選択します。 ペインを開くには:

1. SQL Server Data Tools で、Teradata ソースを含む SSIS パッケージを開きます。

1. **[データ フロー]** タブで、Teradata ソースをダブルクリックします。

1. Teradata ソース エディターで、**[エラー出力]** タブを選択します。

### <a name="options"></a>Options

**エラー動作**

* Teradata ソースでフローのエラーを処理する方法を選択します。 
  * エラーを無視する
  * 行をリダイレクトする
  * コンポーネントを失敗させる

**関連トピック**: 「[データのエラー処理](error-handling-in-data.md)」を参照してください。

**切り捨て**

* Teradata ソースでフローの切り捨てを処理する方法を選択します。 
  * エラーを無視する
  * 行をリダイレクトする
  * コンポーネントを失敗させる

## <a name="next-steps"></a>次のステップ

- [Teradata 変換先](teradata-destination.md)を構成する。
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA6iwdw)を参照してください。