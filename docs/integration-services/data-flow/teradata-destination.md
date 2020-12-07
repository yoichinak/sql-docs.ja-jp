---
description: Teradata 変換先
title: Teradata 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 191c89d1fdced6ad1581dadff1e4ed92f397f640
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194715"
---
# <a name="teradata-destination"></a>Teradata 変換先

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Teradata 変換先では、Teradata データベースにデータが一括で読み込まれます。

この変換先では、Teradata 接続マネージャーを使用してデータ ソースに接続します。 詳細については、[Teradata 接続マネージャー](teradata-connection-manager.md)に関するページを参照してください。

## <a name="load-options"></a>読み込みオプション

Teradata 変換先では、次の 2 つのデータ読み込みモードがサポートされています。

- **TPT Stream**:このモードでは、TPT API Stream 演算子 (Teradata TPump プロトコル) が使用されます。

- **TPT Load** (高速一括読み込み):このモードでは、TPT API Load 演算子 (Teradata FastLoad プロトコル) を使用して高速一括読み込みが行われます。

高速読み込みモードには次の制限があります。

- Teradata データベースのセッションの制限は、次の要因のいずれか最初に検出されたものによって決まります。
    - SESSIONS コマンドを使用して設定されたセッションの制限
    - AMP あたり 1 セッションの Teradata データベースの制限
    - アプリケーションあたりのセッションの最大数に対するプラットフォームの制限:通信プロセッサ (COP) インターフェイス ソフトウェア ファイル CLISPB.DAT の MaxSess 変数によって定義されます。 TDP SET MAXSESSIONS コマンドを使用して、プラットフォームの制限を指定できます。 既定の制限は、サーバーの MAXSESS と同じです。

- インデックスの結合はサポートされていません。
- ターゲット テーブルの外部キー参照はサポートされていません。
- セカンダリ インデックスで定義されているターゲット テーブルはサポートされていません。

Teradata の高速読み込みの制限の詳細については、Teradata の高速読み込みのリファレンスを参照してください。

モードは [Teradata 変換先エディター ([接続マネージャー] ページ)](#teradata-destination-editor-connection-manager-page) で設定できます。

## <a name="error-handling"></a>エラー処理

読み込み処理中に返されたエラーは、一時的なエラー テーブルに書き込まれます。このテーブルは読み込み処理中はロックされます。
詳細エディターの **[エラーの最大数 (MaxErrors)]** プロパティによって、これらのテーブルに書き込めるエラーの最大数が設定されます。

エラーの最大数が 0 より大きい場合は、一意の名前を持つエラー テーブルが生成され、情報メッセージがパッケージ ログに出力されます。 エラーは、標準 SSIS コンポーネントのエラー出力によって取得できます。

読み込み処理が完了すると、一時テーブルは削除されます。 Teradata 変換先でテンポラル テーブルを読み取ることができない場合は、**[常にエラーテーブルを削除する]** プロパティがオンになっていない限り、削除されません。  読み込みプロセスが完了前に停止した場合は、必要に応じて、これらのテーブルを手動で削除する必要があります。 これらのテーブルは、変換先テーブルと同じデータベースに格納されています。

**エラーの最大数** に達したときのターゲット テーブルの状態は、使用しているモードによって異なります。

- 高速読み込みモードでは、ターゲット テーブルは使用できません。 もう一度実行するには、ターゲット テーブルを切り捨てるか削除し、再作成する必要があります。 ロールバックはサポートされていません。
- TPT Stream 演算子モードでは、Teradata 変換先はバッファーされた行メカニズムを介して実行されます。 ジョブが失敗すると、失敗した時点で完了した (バッファーが送信された) すべての変更がターゲット テーブルに永続的に保存されます。 ロールバックの概念はありません。 エラー テーブルは削除されます。

Teradata 変換先にはエラー出力があります。 詳細については、「[Teradata ソース エディター ([エラー出力] ページ)](#teradata-destination-editor-error-output-page)」をご覧ください。

## <a name="parallelism"></a>Parallelism

並列処理は高速読み込みモードでは制限されており、複数の独立した高速読み込みジョブが同時に同じテーブルにアクセスすることはできません。 また、高速読み込みジョブの同時実行の数は、データベース変数 **MaxLoadTasks** によって制限されます。

TPT Stream モードでは、並列処理の制限はありません。 同じテーブルに対して複数の Teradata 変換先を同時に実行することもできますが、これにより Teradata あたりのパフォーマンスが低下する可能性があります。 詳細については、Teradata のドキュメントをご覧ください。

## <a name="troubleshooting-the-teradata-destination"></a>Teradata 変換先のトラブルシューティング

Teradata ソースから Teradata Parallel Transporter API (TPT API) への呼び出しをログに記録できます。 呼び出しをログに記録するには、パッケージのログ記録を有効にし、パッケージ レベルで **診断** イベントを選択します。

Teradata ソースから Teradata ODBC ドライバーへの ODBC の呼び出しをログに記録するには、ODBC ドライバー マネージャーのトレースを有効にします。 詳細については、「 *ODBC で ODBC トレースを生成する方法 (データ ソース管理者向け)* 」 の Microsoft のドキュメントを参照してください。

## <a name="teradata-destination-custom-properties"></a>Teradata 変換先のカスタム プロパティ

次の表で、Teradata 変換先のカスタム プロパティについて説明します。 すべてのプロパティは読み取り/書き込み可能です。

|プロパティ名|データ型|説明|
|:-|:-|:-|
|AlwaysDropErrorTable|ブール型|既定値は **False** です。 **True** の場合、Teradata 変換先が読み取りに失敗した場合でも、すべてのエラー テーブルが削除されます。|
|ArraySupport|ブール型|既定値は **True** です。 **True** の場合、DML グループで ArraySupport が使用されます。 TPT Stream にのみ適用されます。 このプロパティは、**詳細エディター** にあります。|
|バッファー|Integer|増加する要求バッファーの数。値は 2 から 64 で設定できます。 TPT Stream にのみ適用されます。 このプロパティは、**詳細エディター** にあります。|
|BufferMode|ブール型|既定値は **True** です。 PutBuffer 機能が使用されている場合、**True** にする必要があります。 このプロパティは、**詳細エディター** にあります。|
|BufferSize|Integer|読み込みパーセルの送信に使用される出力バッファー サイズ (KB 単位)。 既定値は 1024 です。 TPT Load にのみ適用されます。 このプロパティは、**詳細エディター** にあります。|
|DataEncryption|ブール型|既定値は **False** です。 **True** の場合は、完全セキュリティ暗号化が使用されます。|
|DefaultCodePage|Integer|データ ソースにコード ページ情報がない場合に使用されるコード ページ。 <br>**注**:このプロパティは、**詳細エディター** にあります。|
|DetailedTracingLevel|Integer (列挙)|詳細トレースに対して、次のいずれかのオプションを選択します。 <br> **Off**:詳細ログは記録されません。 <br> **General**:ドライバー固有のアクティビティの一般的なトレースがログに記録されます。 <br> **CLI**:CLIv2 に関連するアクティビティのトレースがログに記録されます。 <br> **Notify Method**:通知機能に関連するアクティビティのトレースがログに記録されます。 <br> **Common Library**: opcommon ライブラリ アクティビティのトレースがログに記録されます。 <br> **[すべて]** : 上記のすべてのアクティビティのトレースがログに記録されます。 <br> 詳細トレース ログ ファイルは、**DetailedTracingFile** プロパティで定義されています。 <br> オプションが Off になっていない場合は、**DetailedTracingFile** プロパティを設定する必要があります。 <br> このプロパティは、**詳細エディター** にあります。|
|DetailedTracingFile|String|**DetailedTracingLevel** が **Off** になっていない場合に、自動的に生成されるログ ファイルのパス。 このプロパティは、**詳細エディター** にあります。|
|DiscardLargeRow|ブール型|既定値は **False** です。 **True** の場合、大きい行 (64K を超える) が破棄されます。|
|ErrorTableName|String|エラー テーブル名。 既定値はターゲット テーブル名です。|
|ExtendedStringColumnsAllocation|ブール型|**True** の場合、**Maximal Transfer Character Allocation Factor** が使用されます。 <br> Teradata データベースの **Export Width Table ID** プロパティが **Maximal Defaults** に設定されている場合は、この値を **True** に設定する必要があります。 <br> 既定値は **False** です。|
|FastLoad|ブール型|**True** の場合、高速読み込みが使用されます。 既定値は **false** です。 これは、[Teradata 変換先エディター ([接続マネージャー] ページ)](#teradata-destination-editor-connection-manager-page) で設定することもできます。|
|[MaxErrors]|Integer|データ フローを停止する前に許容されるエラーの数を指定します。 既定値は **0** です。これは、エラー数の制限がないことを意味します。<br> **[エラー処理]** ページで **[フローのリダイレクト]** が選択されている場合。 エラー数が上限に達する前に、すべてのエラーがエラー出力に返されます。 詳細については、「[Teradata ソース エディター ([エラー出力] ページ)](#teradata-destination-editor-error-output-page)」をご覧ください。|
|MaxSessions|Integer|ログオンされているセッションの最大数。 この値は、1 より大きくする必要があります。 既定値は、使用可能な AMP ごとに 1 つのセッションです。|
|MinSessions|Integer|ログオンされているセッションの最小数。 この値は、1 より大きくする必要があります。 既定値は、使用可能な AMP ごとに 1 つのセッションです。|
|Pack|Integer|複数ステートメントの要求にパックするステートメントの数。 既定値は 20 で、最大許容値は 2400 です。 TPT Stream にのみ適用されます。 このプロパティは、**詳細エディター** にあります。|
|PackMaximum|ブール型|**True** の場合、現在の Stream ジョブの最大パック係数が動的に決定されます。 TPT Stream にのみ適用されます。 このプロパティは、**詳細エディター** にあります。|
|QueryBandSessInfo|Varchar|チャージバックの監視とガバナンスを有効にする、ユーザー定義のセッションベースのクエリ バンド式。 このプロパティは、接続文字列の形式である必要があります。 このプロパティは、**詳細エディター** にあります。|
|ReplicationOveride|Integer (列挙)|オプション: <br> **既定**:SET SESSION OVERRIDE REPLICATION ステートメントがデータベースに送信されません。 データベースの既定の設定が使用されます。 <br> **更新日時**:通常のレプリケーション サービス コントロールはオーバーライドされます。 <br> **Off**:通常のレプリケーション サービス コントロールが使用されます。 <br> このプロパティは、TPT Stream のみに適用されます。 <br> このプロパティは、**詳細エディター** にあります。|
|Robust|ブール型|**True** の場合、復旧と再起動の操作に Robust の再起動ロジックが使用されます。 このプロパティは、**TPT Stream** のみに適用されます。 このプロパティは、**詳細エディター** にあります。|
|TableName|String|使用されているデータを含むテーブルの名前。|
|TenacityHours|Integer|読み込み操作またはエクスポート操作の最大数が既に実行されている場合に、TPT ドライバーがログインを試行する時間数。 既定値は 4 時間です。 このプロパティは、**詳細エディター** にあります。|
|TenacitySleep|Integer|TPT ドライバーが制限に達したときにログインを試行する前に一時停止する分数。 制限は **MaxSessions** プロパティと **TenacityHours** プロパティによって定義されます。 既定値は 6 分です。 このプロパティは、**詳細エディター** にあります。|
|UnicodePassThrough|ブール型|Off (既定値):Unicode パス スルーを無効にします。 <br>On:Unicode パス スルーを有効にします。|

## <a name="configuring-the-teradata-destination"></a>Teradata 変換先を構成する

Teradata 変換先は、プログラムによって、または SSIS デザイナーを使用して構成できます。

Teradata 変換先エディターを次の図に示します。 それには、[接続マネージャー] ページ、[マッピング] ページ、および [エラー出力] ページが含まれています。

詳細については、次のいずれかのトピックを参照してください。

- [Teradata 変換先エディター ([接続マネージャー] ページ)](#teradata-destination-editor-connection-manager-page)
- [Teradata 変換先エディター ([マッピング] ページ)](#teradata-destination-editor-mappings-page)
- [Teradata 変換先エディター ([エラー出力] ページ)](#teradata-destination-editor-error-output-page)

![変換先エディター](media/teradata-destination.png)

**[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。
**[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。

- Integration Services プロジェクトの **[データ フロー]** 画面で、Teradata 変換先を右クリックし、**[詳細エディターの表示]** を選択します。

[詳細エディター] ダイアログ ボックスで設定できるプロパティの詳細については、「[Teradata 変換先のカスタム プロパティ](#teradata-destination-custom-properties)」を参照してください。

## <a name="teradata-destination-editor-connection-manager-page"></a>Teradata 変換先エディター ([接続マネージャー] ページ)

**[Teradata 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用して、変換先用の Teradata 接続マネージャーを選択します。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。

Teradata 変換先エディターの [接続マネージャー] ページを開くには

- SQL Server Data Tools で、Teradata 変換先を含む SQL Server Integration Services (SSIS) パッケージを開きます。

- [データ フロー] タブで、Teradata 変換先をダブルクリックします。

- [Teradata 変換先エディター] で、[接続マネージャー] をクリックします。

### <a name="options"></a>Options

**Connection manager**

既存の接続マネージャーを一覧から選択するか、**[新規作成]** をクリックして新しい Teradata 接続マネージャーを作成します。

**[新規作成]**

**[新規作成]** をクリックします。 **[Teradata 接続マネージャー エディター]** ダイアログ ボックスが開き、ここで新しい接続マネージャーを作成できます。

**[データ アクセス モード]**

入力元のデータを選択する方法を選択します。 次の表に示すオプションがあります。

|オプション|説明|
|:-|:-|
|テーブル名 - TPT Stream|TPT Stream 演算子を使用した増分モード。 <br>**[テーブル名またはビュー名]** :既存のテーブルまたはビューを一覧から選択します。 この一覧には、最初の 1000 個のテーブルのみが表示されます。 テーブル名のプレフィックスを入力するか、名前の任意の部分と (*) ワイルドカードを使用して、使用するテーブルを一覧表示することができます。|
|テーブル名 - TPL Load|TPT API Load 演算子 (Teradata FastLoad プロトコル) を使用した高速 (ダイレクト パス) 読み込みモード。ターゲット テーブルを空にする必要があります。 <br>**[テーブル名またはビュー名]** : 既存のテーブルまたはビューを一覧から選択します。 この一覧には、最初の 1000 個のテーブルのみが表示されます。 テーブル名のプレフィックスを入力するか、名前の任意の部分と (*) ワイルドカードを使用して、使用するテーブルを一覧表示することができます。|

**[データの暗号化]** チェック ボックス: データの暗号化を有効にします。 既定では選択されていません。

**[常にエラーテーブルを削除する]** チェック ボックス: すべてのインスタンスのエラー テーブルを削除します。

**[エラー テーブル]**: エラーが書き込まれるテーブルの名前。

**[セッションの最小数]**: ログオンされているセッションの最小数。 既定値は、使用可能な AMP ごとに 1 つのセッションです。 値は 1 よりも大きくする必要があります。

**[セッションの最大数]**: ログオンされているセッションの最大数。 既定値は、使用可能な AMP ごとに 1 つのセッションです。 値は 1 よりも大きくする必要があります。

**[エラーの最大数]**: データ フローが停止またはリダイレクトされる前に返すことができるエラーの最大数。 

## <a name="teradata-destination-editor-mappings-page"></a>Teradata 変換先エディター ([マッピング] ページ)

**[Teradata 変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用して、入力列を変換先列にマップします。

Teradata 変換先エディターの [マッピング] ページを開くには

- SQL Server Data Tools で、Teradata 変換先を含む SQL Server Integration Services (SSIS) パッケージを開きます。

- [データ フロー] タブで、Teradata 変換先をダブルクリックします。

- [Teradata 変換先エディター] で、[マッピング] をクリックします。

### <a name="options"></a>オプション

**使用できる入力列**

使用できる入力列の一覧です。 使用できる変換先列に入力列をドラッグ アンド ドロップして、列をマップできます。

**使用できる変換先列**

使用できる変換先列の一覧です。 使用できる入力列に変換先列をドラッグ アンド ドロップして、列をマップできます。

**入力列**

選択した入力列を表示します。 **< 無視 >** を選択して出力から列を除外することで、マッピングを削除できます。

**変換先列**

使用できるすべての変換先列を表示します (マップ済みの列とマップされていない列を両方とも含む)。

>[!NOTE]
>
>サポートされていないデータ型の列は、警告と共にマッピングから削除されます。

## <a name="teradata-destination-editor-error-output-page"></a>Teradata 変換先エディター ([エラー出力] ページ)
[Teradata 変換先エディター] ダイアログ ボックスの [エラー出力] ページを使用して、エラー処理オプションを選択します。

**Teradata 変換先エディターの [エラー出力] ページを開くには**

- SQL Server Data Tools で、Teradata 変換先を含む SQL Server Integration Services (SSIS) パッケージを開きます。

- [データ フロー] タブで、Teradata 変換先をダブルクリックします。

- [Teradata 変換先エディター] で、[エラー出力] をクリックします。

### <a name="options"></a>Options

**エラー動作**

Teradata 変換先でフローのエラーを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。

**関連トピック:** [データのエラー処理](./error-handling-in-data.md?view=sql-server-2017)

**切り捨て**

Teradata 変換先でフローの切り捨てを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。

## <a name="next-steps"></a>次のステップ

- [Teradata 接続マネージャー](teradata-connection-manager.md)を構成する
- [Teradata ソース](teradata-source.md)を構成する
- [Teradata 変換先](teradata-destination.md)を構成する
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA6iwdw)を参照してください。