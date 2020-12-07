---
description: SSMA コンソールの実行 (SybaseToSQL)
title: SSMA コンソールの実行 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fee973fdcb79105d5fe7c412c10bdda2cd1bbec5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372238"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>SSMA コンソールの実行 (SybaseToSQL)
Microsoft では、SSMA アクティビティを実行および制御するための、堅牢なスクリプトファイルコマンドのセットを提供しています。 以降のセクションでも同じことが説明されています。  
  
## <a name="script-file-commands"></a>スクリプトファイルのコマンド  
コンソールアプリケーションでは、このセクションで列挙されている特定の標準スクリプトファイルコマンドを使用します。  
  
## <a name="project-commands"></a>プロジェクトコマンド  
プロジェクトコマンドは、プロジェクトの作成、プロジェクトのオープン、保存、および終了を処理します。  
  
### <a name="create-new-project"></a>create-new-project  
このコマンドにより、新しい SSMA プロジェクトが作成されます。  
  
-   `project-folder` 作成するプロジェクトのフォルダーを示します。  
  
-   `project-name` プロジェクトの名前を示します。 {string}  
  
-   `overwrite-if-exists`省略可能な属性既存のプロジェクトを上書きするかどうかを示します。 演算  
  
-   `project-type:`省略可能な属性です。 プロジェクトの種類を示します。これは "sql-server-2005" プロジェクトまたは "sql-server-2008" project または "sql-server-2012" プロジェクトまたは "sql-server-2014" プロジェクトまたは "sql-azure" プロジェクトです。 既定値は "sql-server-2008" です。  
  
**構文の例:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
既定では、属性 ' overwrite-exists ' は **false** です。  
  
既定では、属性 ' プロジェクトの種類 ' は **sql server-2008** です。  
  
### <a name="open-project"></a>プロジェクトを開く  
このコマンドを実行すると、プロジェクトが開きます。

-   `project-folder` 作成するプロジェクトのフォルダーを示します。 指定されたフォルダーが存在しない場合、コマンドは失敗します。  {string}  
  
-   `project-name` プロジェクトの名前を示します。 指定されたプロジェクトが存在しない場合、コマンドは失敗します。  {string}  
  
**構文の例:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA for SAP ASE コンソールアプリケーションでは、旧バージョンとの互換性がサポートされています。 これを使用して、以前のバージョンの SSMA で作成されたプロジェクトを開くことができます。  
  
### <a name="save-project"></a>save-project  
このコマンドは、移行プロジェクトを保存します。  
  
**構文の例:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>閉じる-プロジェクト  
このコマンドは、移行プロジェクトを閉じます。  
  
**構文の例:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
属性 ' if-modified ' は省略可能です。既定では **無視** されます。  
  
## <a name="database-connection-commands"></a>データベース接続コマンド  
データベース接続コマンドを使用すると、データベースに接続できます。  
  
> [!NOTE]  
> - UI の **参照** 機能は、コンソールではサポートされていません。  
> - 「スクリプトファイルの作成」の詳細については、「 [SybaseToSQL&#41;&#40;スクリプトファイルの作成 ](../../ssma/sybase/creating-script-files-sybasetosql.md)」を参照してください。  
  
### <a name="connect-source-database"></a>接続ソース-データベース  
このコマンドは、ソースデータベースへの接続を実行し、ソースデータベースの高レベルのメタデータを読み込みますが、すべてのメタデータを読み込みません。
  
ソースへの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。
  
サーバー定義は、サーバー接続ファイルまたはスクリプトファイルの server セクション内の各接続に対して定義されている name 属性から取得されます。  
  
**構文の例:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>強制読み込み-ソース/ターゲット-データベース  
このコマンドは、ソースのメタデータを読み込みます。これは、移行プロジェクトをオフラインで操作する場合に便利です。  
  
ソース/ターゲットへの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションの実行が停止します。  
  
このコマンドでは、コマンドラインパラメーターとして1つまたは複数のメタベースノードが必要です。  
  
**構文の例:**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>再接続-ソース-データベース  
このコマンドを実行すると、ソースデータベースに再接続されますが、メタデータは読み込まれません。これは、接続元データベースのコマンドとは異なります。  
  
(Re) ソースとの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。  
  
**構文の例:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>接続-ターゲット-データベース  
このコマンドは、ターゲットの SQL Server データベースに接続し、メタデータ全体ではなく、ターゲットデータベースの高レベルのメタデータを読み込みます。  
  
ターゲットへの接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。  
  
サーバー定義は、サーバー接続ファイルまたはスクリプトファイルの server セクション内の各接続に対して定義されている name 属性から取得されます。  
  
**構文の例:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>再接続-ターゲット-データベース  
  
このコマンドを実行すると、ターゲットデータベースに再接続されますが、メタデータは読み込まれません。これは、接続先データベースのコマンドとは異なります。  
  
ターゲットへの (re) 接続を確立できない場合は、エラーが生成され、コンソールアプリケーションはさらに実行を停止します。  
  
**構文の例:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>レポート コマンド  
このレポートコマンドでは、さまざまな SSMA コンソールアクティビティのパフォーマンスに関するレポートが生成されます。  
  
### <a name="generate-assessment-report"></a>生成-評価-レポート  
  
このコマンドは、ソースデータベースの評価レポートを生成します。  
  
このコマンドを実行する前にソースデータベース接続が実行されていない場合は、エラーが生成され、コンソールアプリケーションは終了します。  
  
コマンドの実行中にソースデータベースサーバーに接続できなかった場合も、コンソールアプリケーションが終了します。  
  
-   `conversion-report-folder:` 評価レポートを格納できるフォルダーを指定します。 (省略可能な属性)  
  
-   `object-name:` 評価レポートの生成の対象となるオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名をサポートします)。  
  
-   `object-type:` オブジェクト名属性で out と呼ばれるオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
-   `conversion-report-overwrite:` 評価レポートフォルダが既に存在する場合に上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` レポートが生成されるパスを指定します。  
  
    フォルダーパスのみが指定されている場合は、AssessmentReport n という名前でファイルを指定し ** &lt; &gt; ます。XML** が作成されます。 (省略可能な属性)  
  
    レポートの作成には、次の2つのサブカテゴリがあります。  
  
    -   `report-errors` (= "true/false"、既定値は "false" (省略可能な属性)  
  
    -   `verbose` (= "true/false"、既定値は "false" (省略可能な属性)  
  
**構文の例:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
or  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>移行コマンド  
移行コマンドは、ターゲットデータベーススキーマをソーススキーマに変換し、データをターゲットサーバーに移行します。  
  
### <a name="convert-schema"></a>変換-スキーマ  
このコマンドは、ソーススキーマから送信先スキーマへのスキーマ変換を実行します。  
  
このコマンドを実行する前に転送元または転送先のデータベース接続が実行されない場合、またはコマンドの実行中に転送元または転送先のデータベースサーバーへの接続に失敗した場合は、エラーが生成され、コンソールアプリケーションが終了します。  
  
-   `conversion-report-folder:` 評価レポートを格納できるフォルダーを指定します。 (省略可能な属性)  
  
-   `object-name:` スキーマを変換する際に考慮するソースオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名をサポートします)。  
  
-   `object-type:` オブジェクト名属性で out と呼ばれるオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
-   `conversion-report-overwrite:` 評価レポートフォルダが既に存在する場合に上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-summary-report-to:` 概要レポートが生成されるパスを指定します。  
  
    フォルダーパスのみが指定されている場合は、SchemaConversionReport n という名前でファイルを指定し ** &lt; &gt; ます。XML** が作成されます。 (省略可能な属性)  
  
    レポートの作成には、次の2つのサブカテゴリがあります。  
  
    -   `report-errors` (= "true/false"、既定値は "false" (省略可能な属性)  
  
    -   `verbose` (= "true/false"、既定値は "false" (省略可能な属性)  
  
**構文の例:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
or  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>データの移行  
このコマンドは、ソースデータをターゲットに移行します。  
  
-   `object-name:` データの移行の対象となるソースオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名をサポートします)。  
  
-   `object-type:` オブジェクト名属性で out と呼ばれるオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
-   `write-summary-report-to:` レポートが生成されるパスを指定します。  
  
    フォルダーパスのみが指定されている場合は、DataMigrationReport n という名前でファイルを指定し ** &lt; &gt; ます。XML** が作成されます。 (省略可能な属性)  
  
    レポートの作成には、次の2つのサブカテゴリがあります。  
  
    -   `report-errors` (= "true/false"、既定値は "false" (省略可能な属性)  
  
    -   `verbose` (= "true/false"、既定値は "false" (省略可能な属性)  
  
**構文の例:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
or  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>移行準備コマンド  
移行準備コマンドを実行すると、ソースデータベースとターゲットデータベース間のスキーママッピングが開始されます。  
  
> [!NOTE]  
> 移行コマンドの既定のコンソール出力設定は ' Full ' 出力レポートで、詳細なエラー報告はありません。概要は、ソースオブジェクトツリーのルートノードでのみです。  
  
### <a name="map-schema"></a>マップ-スキーマ  
このコマンドは、転送元データベースから送信先スキーマへのスキーママッピングを提供します。  
  
-   `source-schema` 移行する送信元スキーマを指定します。  
  
-   `sql-server-schema` 送信元スキーマの移行先となるターゲットスキーマを指定します。  
  
**構文の例:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>管理コマンド  
管理容易性コマンドを使用すると、ターゲットデータベースオブジェクトとソースデータベースを同期できます。  
  
> [!NOTE]  
> 移行コマンドの既定のコンソール出力設定は ' Full ' 出力レポートで、詳細なエラー報告はありません。概要は、ソースオブジェクトツリーのルートノードでのみです。  
  
### <a name="synchronize-target"></a>同期-ターゲット  
このコマンドにより、ターゲットオブジェクトとターゲットデータベースが同期されます。  
 
このコマンドがソースデータベースに対して実行されると、エラーが発生します。  
  
このコマンドを実行する前にターゲットデータベース接続が実行されなかった場合、またはターゲットデータベースサーバーへの接続がコマンドの実行中に失敗した場合は、エラーが生成され、コンソールアプリケーションが終了します。  
  
-   `object-name:` ターゲットデータベースとの同期を検討するターゲットオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名をサポートします)。  
  
-   `object-type:` オブジェクト名属性で out と呼ばれるオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
-   `on-error:` 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー発生時に使用可能なオプション:  
  
    -   レポート-合計-警告  
  
    -   レポート-警告ごと  
  
    -   失敗-スクリプト  
  
-   `report-errors-to:` 同期操作のエラーレポートの場所を指定します (省略可能)。 フォルダーのパスのみを指定した場合は、[名前でファイルを **TargetSynchronizationReport.XML** ] が作成されます。  
  
**構文の例:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
or  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
or  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>データベースからの更新  
このコマンドは、ソースオブジェクトをデータベースから更新します。  
  
対象のデータベースに対してこのコマンドを実行すると、エラーが生成されます。  
  
このコマンドでは、コマンドラインパラメーターとして1つまたは複数のメタベースノードが必要です。  
  
-   `object-name:` ソースデータベースからの更新の対象となるソースオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名をサポートします)。  
  
-   `object-type:` オブジェクト名属性で指定したオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
-   `on-error:` 更新エラーを警告またはエラーとして呼び出すかどうかを指定します。 エラー発生時に使用可能なオプション:  
  
    -   レポート-合計-警告  
  
    -   レポート-警告ごと  
  
    -   失敗-スクリプト  
  
-   `report-errors-to:` 更新操作のエラーレポートの場所を指定します (省略可能)。 フォルダーのパスのみを指定した場合は、[名前でファイルを **SourceDBRefreshReport.XML** ] が作成されます。  
  
**構文の例:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
or  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
or  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>スクリプト生成コマンド  
スクリプト生成コマンドは、2つのタスクを実行します。コンソールの出力をスクリプトファイルに保存し、指定したパラメーターに基づいて T-sql の出力をコンソールまたはファイルに記録します。  
  
### <a name="save-as-script"></a>スクリプトとして保存  
このコマンドは、メタベース = ターゲットの場合に示されているファイルにオブジェクトのスクリプトを保存するために使用します。 これは、スクリプトを取得し、ターゲットデータベースで同じを実行するという、同期コマンドの代替手段です。  
  
このコマンドでは、コマンドラインパラメーターとして1つまたは複数のメタベースノードが必要です。  
  
-   `object-name:` スクリプトを保存するオブジェクトを指定します (個々のオブジェクト名またはグループオブジェクト名をサポートします)。  
  
-   `object-type:` オブジェクト名属性で out と呼ばれるオブジェクトの種類を指定します (object カテゴリが指定されている場合、オブジェクトの種類は "category" になります)。  
  
-   `metabase:` ソースまたはターゲットのメタベースかどうかを指定します。  
  
-   `destination:` スクリプトを保存するパスまたはフォルダーを指定します。 ファイル名が指定されていない場合は、(object_name 属性値) out という形式のファイル名が指定されます。
  
-   `overwrite:` True の場合、同じファイル名を上書きします (存在する場合)。 値 (true/false) を指定できます。  
  
**構文の例:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
or  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert-sql ステートメント
このコマンドは、SQL ステートメントを変換します。  
  
-   `context` スキーマ名を指定します。  
  
-   `destination` 出力をファイルに格納するかどうかを指定します。  
  
    この属性が指定されていない場合は、変換後の T-sql ステートメントがコンソールに表示されます。 (省略可能な属性)  
  
-   `conversion-report-folder` 評価レポートを格納できるフォルダーを指定します。 (省略可能な属性)  
  
-   `conversion-report-overwrite` 評価レポートフォルダが既に存在する場合に上書きするかどうかを指定します。  
  
    **既定値:** false。 (省略可能な属性)  
  
-   `write-converted-sql-to` 変換された T-sql を格納するファイル (またはフォルダー) のパスを指定します。 フォルダーパスが属性と共に指定されている場合 `sql-files` 、各ソースファイルには、指定されたフォルダーの下に作成される対応するターゲット t-sql ファイルがあります。 フォルダーパスが属性と共に指定されている場合、変換された `sql` t-sql は、指定したフォルダーの下に、Result という名前のファイルに書き込まれます。  
  
-   `sql` 変換する Sybase sql ステートメントを指定します。1つ以上のステートメントを ";" で区切ることができます。  
  
-   `sql-files` T-sql コードに変換する必要がある sql ファイルのパスを指定します。  
  
-   `write-summary-report-to` 概要レポートが生成されるパスを指定します。 フォルダーパスのみが指定されている場合は、[名前でファイルを **ConvertSQLReport.XML** ] が作成されます。 (省略可能な属性)  
  
    概要レポートの作成には、次の2つのサブカテゴリがあります。  
  
    -   レポート-エラー (= "true/false"、既定値は "false" (省略可能な属性))。  
  
    -   verbose (= "true/false",、既定値は "false" (省略可能な属性))。  
  
このコマンドでは、コマンドラインパラメーターとして1つまたは複数のメタベースノードが必要です。  
  
**構文の例:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
or  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
or  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>次の手順  
コマンドラインオプションの詳細については、 [SSMA コンソールのコマンドラインオプション](../access/command-line-options-in-ssma-console-accesstosql.md)に関する情報を参照してください。  
  
サンプルコンソールスクリプトファイルの詳細については、「 [Working Basetosql &#40;サンプルコンソールスクリプトファイルの操作](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)」を参照してください&#41;  
  
次の手順は、プロジェクトの要件によって異なります。  
  
-   パスワードを指定する、またはパスワードをエクスポート/インポートする方法については、「パスワードの [管理 &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)」を参照してください。  
  
-   レポートを生成する方法については、「 [SybaseToSQL&#41;&#40;レポートの生成 ](../../ssma/sybase/generating-reports-sybasetosql.md)」を参照してください。  
  
-   コンソールでの問題のトラブルシューティングについては、「 [&#40;SybaseToSQL&#41;のトラブルシューティング ](../../ssma/sybase/troubleshooting-sybasetosql.md)」を参照してください。  
  
