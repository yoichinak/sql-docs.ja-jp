---
description: SSMA コンソールの実行 (管理用 Sql)
title: SSMA コンソールの実行 (管理用 Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 655b6f64391ebf8c7fd28d179000753ed4f95faa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492515"
---
# <a name="executing-the-ssma-console-accesstosql"></a>SSMA コンソールの実行 (管理用 Sql)
Microsoft では、SSMA アクティビティを実行および制御するための、堅牢なスクリプトファイルコマンドとコマンドラインオプションのセットを提供しています。 以降のセクションでも同じことが説明されています。  
  
## <a name="project--script-file-commands"></a>プロジェクトスクリプトファイルのコマンド  
プロジェクトコマンドは、プロジェクトの作成、プロジェクトのオープン、保存、および終了を処理します。  
  
**コマンド**  
  
create-new-project: 新しい SSMA プロジェクトを作成します。  
  
**スクリプト**  
  
-   `project-folder` 作成するプロジェクトのフォルダーを示します。  
  
-   `project-name` プロジェクトの名前を示します。 {string}  
  
-   `overwrite-if-exists`省略可能な属性は、既存のプロジェクトを上書きする必要があるかどうかを示します。 演算  
  
-   `project-type` は省略可能な属性です。  プロジェクトの種類では、次のオプションを使用できます。  
  
    -   sql-サーバー-2005  
  
    -   sql-サーバー-2008  
  
    -   sql-サーバー-2012  
  
    -   sql-サーバー-2014  
  
    -   sql-サーバー-2016  
  
    -   sql-azure  
  
    既定値は "sql-server-2008" です。  
  
**例:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
/>  
```  
既定では、属性 ' overwrite-exists ' は **false** です。  
  
既定では、属性 ' プロジェクトの種類 ' は **sql server-2008** です。  
  
**コマンド**  
  
[プロジェクトを開く]: 既存のプロジェクトを開きます。  
  
**スクリプト**  
  
-   `project-folder` 作成するプロジェクトのフォルダーを示します。 指定されたフォルダーが存在しない場合、コマンドは失敗します。  {string}  
  
-   `project-name` プロジェクトの名前を示します。 指定されたプロジェクトが存在しない場合、コマンドは失敗します。  {string}  
  
**構文の例:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
**注:** SSMA For Access コンソールアプリケーションでは、旧バージョンとの互換性がサポートされています。 以前のバージョンの SSMA で作成されたプロジェクトを開くことができます。  
  
**コマンド**  
  
プロジェクトの保存: 移行プロジェクトを保存します。  
  
**スクリプト**  
  
**構文の例:**  
  
```xml  
<save-project/>  
```  
**コマンド**  
  
[プロジェクトの終了]: 移行プロジェクトを閉じます。  
  
**スクリプト**  
  
**構文の例:**  
  
```xml  
<close-project  
  
  if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
属性 ' if-modified ' は省略可能です。既定では **無視** されます。  
  
## <a name="database-connection-script-file-commands"></a>データベース接続スクリプトファイルのコマンド  
データベース接続コマンドを使用すると、データベースに接続できます。  
  
UI の **参照** 機能は、コンソールではサポートされていません。  
  
SQL Azure に接続する場合、 **windows 認証** と **ポート** のパラメーターは適用されません。  
  
"スクリプトファイルの作成" の詳細については、「 [&#41;&#40;スクリプトファイルの作成 ](../../ssma/access/creating-script-files-accesstosql.md)」を参照してください。  
  
**コマンド**
  
接続ソース-データベース  
  
- ソースデータベースへの接続を実行し、メタデータの一部ではなく、ソースデータベースの高レベルのメタデータを読み込みます。  
  
- ソースへの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションの実行が停止します。  
  
**スクリプト**
  
サーバー定義は、サーバー接続ファイルまたはスクリプトファイルの server セクション内の各接続に対して定義されている name 属性から取得されます。  
  
**構文の例:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**コマンド**  
  
読み込み-アクセスデータベース: access データベースファイルの読み込みに使用されます。  
  
**スクリプト**  
  
**構文の例:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
or  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
```  
**コマンド**  
  
強制読み込み-ソース/ターゲット-データベース  
  
-   ソースメタデータを読み込みます。  
  
-   移行プロジェクトをオフラインで作業する場合に便利です。  
  
-   ソース/ターゲットへの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションの実行が停止します。  
  
**スクリプト**  
  
コマンドラインパラメーターとして、1つまたは複数のメタベースノードが必要です。  
  
**構文の例:**  
  
```xml  
<force-load  
  
  object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
or  
  
```xml  
<force-load>  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**コマンド**  
  
再接続-ソース-データベース  
  
- ソースデータベースに再接続しますが、接続元データベースのコマンドとは異なり、メタデータは読み込まれません。  
  
- (Re) ソースとの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。  
  
**スクリプト**
  
**構文の例:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```

**コマンド**
  
接続-ターゲット-データベース  
  
- ターゲットの SQL Server または SQL Azure データベースに接続し、メタデータ全体ではなく、ターゲットデータベースの高レベルのメタデータを読み込みます。  
  
- ターゲットへの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。  
  
**スクリプト**
  
サーバーの定義は、サーバー接続ファイルまたはスクリプトファイルの server セクション内の各接続に対して定義されている name 属性から取得されます。  
  
**構文の例:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  

**コマンド**
  
再接続-ターゲット-データベース  
  
- ターゲットデータベースに再接続しますが、メタデータは読み込まれません。これは、接続先データベースのコマンドとは異なります。  
  
- ターゲットへの (re) 接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。  
  
**スクリプト**
  
**構文の例:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  

## <a name="report-script-file-commands"></a>レポートスクリプトファイルのコマンド

レポートコマンドにより、さまざまな SSMA コンソールアクティビティのパフォーマンスに関するレポートが生成されます。

**コマンド**
  
生成-評価-レポート  
  
- ソースデータベースに対して評価レポートを生成します。  
  
- このコマンドを実行する前にソースデータベース接続が実行されていない場合は、エラーが生成され、コンソールアプリケーションは終了します。  
  
- コマンドの実行中にソースデータベースサーバーに接続できなかった場合は、コンソールアプリケーションが終了します。  
  
**スクリプト**

- `assessment-report-folder:` 評価レポートを格納できるフォルダーを指定します。(省略可能な属性)  
  
- `object-name:` 評価レポートの生成の対象となるオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名を持つことができます)。  
  
- `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
- `assessment-report-overwrite:` 評価レポートフォルダが既に存在する場合に上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
- `write-summary-report-to:` レポートが生成されるパスを指定します。  
  
    フォルダーパスのみが指定されている場合は、AssessmentReport n という名前でファイルを指定し ** &lt; &gt; ます。XML** が作成されます。 (省略可能な属性)  
  
    レポートの作成には、次の2つのサブカテゴリがあります。  
  
    - `report-errors` (= "true/false"、既定値は "false" (省略可能な属性)  
  
    - `verbose` (= "true/false"、既定値は "false" (省略可能な属性)  
  
**構文の例:**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```

or
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>移行スクリプトファイルのコマンド

移行コマンドは、ターゲットデータベーススキーマをソーススキーマに変換し、データを対象サーバーに移行します。  
  
移行コマンドの既定のコンソール出力設定は ' Full ' 出力レポートで、詳細なエラー報告はありません。概要は、ソースオブジェクトツリーのルートノードでのみです。  
  
**コマンド**

変換-スキーマ  
  
- 送信元スキーマから送信先スキーマへのスキーマ変換を実行します。  
  
- このコマンドを実行する前に転送元または転送先のデータベース接続が実行されない場合、またはコマンドの実行中に転送元または転送先のデータベースサーバーへの接続に失敗した場合は、エラーが生成され、コンソールアプリケーションが終了します。  
  
**スクリプト**

- `conversion-report-folder:` 評価レポートを格納できるフォルダーを指定します。(省略可能な属性)  
  
- `object-name:` スキーマを変換する際に考慮するソースオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名を使用できます)。  
  
- `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
- `conversion-report-overwrite:` 評価レポートフォルダが既に存在する場合に上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
- `write-summary-report-to:` レポートが生成されるパスを指定します。  
  
    フォルダーパスのみが指定されている場合は、SchemaConversionReport n という名前でファイルを指定し ** &lt; &gt; ます。XML** が作成されます。 (省略可能な属性)  
  
    レポートの作成には、次の2つのサブカテゴリがあります。  
  
    - `report-errors` (= "true/false"、既定値は "false" (省略可能な属性)  
  
    - `verbose` (= "true/false"、既定値は "false" (省略可能な属性)  
  
**構文の例:**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```

or  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```

**コマンド**
  
データの移行  
  
- ソースデータをターゲットに移行します。  
  
**スクリプト**
  
- `object-name:` データを移行する際に考慮するソースオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名を持つことができます)。  
  
- `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
- `write-summary-report-to:` レポートが生成されるパスを指定します。  
  
    フォルダーパスのみが指定されている場合は、DataMigrationReport n という名前でファイルを指定し ** &lt; &gt; ます。XML** が作成されます。 (省略可能な属性)  
  
    レポートの作成には、次の2つのサブカテゴリがあります。  
  
    - `report-errors` (= "true/false"、既定値は "false" (省略可能な属性)  
  
    - `verbose` (= "true/false"、既定値は "false" (省略可能な属性)  
  
**構文の例:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```

or  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```

**コマンド**
  
リンクテーブル: このコマンドは、ソース (Access) テーブルを対象テーブルにリンクします。  
  
**スクリプト**

**構文の例:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```

or  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```

**コマンド**
  
テーブルのリンク解除: このコマンドは、ソース (Access) テーブルとターゲットテーブルとのリンクを解除します。  
  
**スクリプト**
  
**構文の例:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```

or  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>移行準備スクリプトファイルコマンド

移行準備コマンドを実行すると、ソースデータベースとターゲットデータベース間のスキーママッピングが開始されます。  
  
**コマンド**
  
マップ-スキーマ: ソースデータベースから送信先スキーマへのスキーママッピング。  
  
**スクリプト**
  
- `source-schema` 移行するソーススキーマを指定します。  
  
- `sql-server-schema` 移行するターゲットスキーマを指定します。  
  
**構文の例:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>管理コマンド

管理容易性コマンドを使用すると、ターゲットデータベースオブジェクトとソースデータベースを同期できます。  
  
移行コマンドの既定のコンソール出力設定は ' Full ' 出力レポートで、詳細なエラー報告はありません。概要は、ソースオブジェクトツリーのルートノードでのみです。  
  
**コマンド**

同期-ターゲット  
  
- ターゲットデータベースとターゲットオブジェクトを同期します。  
  
- このコマンドがソースデータベースに対して実行されると、エラーが発生します。  
  
- このコマンドを実行する前にターゲットデータベース接続が実行されなかった場合、またはターゲットデータベースサーバーへの接続がコマンドの実行中に失敗した場合は、エラーが生成され、コンソールアプリケーションが終了します。  
  
**スクリプト**
  
- `object-name:` ターゲットデータベースと同期する対象のオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名を持つことができます)。  
  
- `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
- `on-error:` 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー発生時に使用可能なオプション:  
  
    - レポート-合計-警告  
  
    - レポート-警告ごと  
  
    - 失敗-スクリプト  
  
- `report-errors-to:` 同期操作のエラーレポートの場所を指定します (省略可能属性)。フォルダーのパスのみを指定した場合は、[名前でファイルを **TargetSynchronizationReport.XML** ] が作成されます。  
  
**構文の例:**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```

or  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```

or  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```

**コマンド**
  
データベースからの更新  
  
- データベースからソースオブジェクトを更新します。  
  
- 対象のデータベースに対してこのコマンドを実行すると、エラーが生成されます。  
  
**スクリプト**
  
コマンドラインパラメーターとして、1つまたは複数のメタベースノードが必要です。  
  
- `object-name:` ソースデータベースからの更新の対象となるソースオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名を持つことができます)。  
  
- `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
- `on-error:` 更新エラーを警告またはエラーとして指定するかどうかを指定します。 エラー発生時に使用可能なオプション:  
  
    - レポート-合計-警告  
  
    - レポート-警告ごと  
  
    - 失敗-スクリプト  
  
- `report-errors-to:` 更新操作のエラーレポートの場所を指定します (省略可能)。フォルダーのパスのみを指定した場合は、[名前でファイルを **SourceDBRefreshReport.XML** ] が作成されます。  
  
**構文の例:**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```

or  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```

or  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>スクリプト生成スクリプトファイルのコマンド

スクリプト生成コマンドは、コンソールの出力をスクリプトファイルに保存するのに役立ちます。  
  
**コマンド**
  
スクリプトとして保存  
  
メタベース = ターゲットとして記述されているファイルにオブジェクトのスクリプトを保存するために使用します。ここでは、スクリプトを取得し、ターゲットデータベースで同じを実行する同期コマンドの代替手段です。  
  
**スクリプト**
  
コマンドラインパラメーターとして、1つまたは複数のメタベースノードが必要です。  
  
- `object-name:` スクリプトを保存するオブジェクトを指定します。 (個々のオブジェクト名またはグループオブジェクト名を持つことができます)  
  
- `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
- `metabase:` ソースまたはターゲットのメタベースかどうかを指定します。  
  
- `destination:` スクリプトを保存するパスまたはフォルダーを指定します。ファイル名が指定されていない場合は、(object_name 属性値) という形式のファイル名になります。  
  
- `overwrite:` true の場合、同じファイル名が存在するかどうかを上書きします。 値 (true/false) を指定できます。  
  
**構文の例:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```

or  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-steps"></a>次の手順

コマンドラインオプションの詳細については、「 [SSMA コンソールのコマンドラインオプション &#40;の&#41;](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) 」を参照してください。  
  
サンプルのコンソールスクリプトファイルの詳細については、「 [FilesExecuting The Sample Console script」 (SSMA コンソールのサンプル](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)) の操作」を参照してください &#40;&#41;  
  
次の手順は、プロジェクトの要件によって異なります。  
  
- パスワードの指定、またはパスワードのエクスポート/インポートについては、「パスワードの管理」を参照してください [&#40;&#41;](../../ssma/access/managing-passwords-accesstosql.md)。  
  
- レポートを生成する方法については、「レポートの生成」を参照してください [&#40;&#41;](../../ssma/access/generating-reports-accesstosql.md)。  
  
- コンソールでの問題のトラブルシューティングについては、「 [&#41;&#40;のトラブルシューティング ](../../ssma/access/troubleshooting-accesstosql.md)」を参照してください。  
