---
title: SQL Server Integration Services DevOps 概要 | Microsoft Docs
description: SSIS DevOps ツールで SSIS CICD をビルドする方法について説明します。
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 597792aa200edf6dcb9cfe49c95ab5e1befa0c55
ms.sourcegitcommit: 5f3e0eca9840db20038f0362e5d88a84ff3424af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2020
ms.locfileid: "92343654"
---
# <a name="sql-server-integration-services-ssis-devops-tools-azure-devops-extension"></a>SQL Server Integration Services (SSIS) DevOps ツール Azure DevOps 拡張機能

[SSIS DevOps Tools](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) 拡張機能は **Azure DevOps** Marketplace で入手できます。

**Azure DevOps** 組織がない場合、まず、 [Azure Pipelines](/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops) に新規登録し、 [次の手順](/azure/devops/marketplace/overview?tabs=browser&view=azure-devops#add-an-extension)で **SSIS DevOps ツール** 拡張機能を追加します。

**SSIS DevOps ツール** には、 **SSIS Build** タスク、 **SSIS Deploy** リリース タスク、および **SSIS Catalog Configuration タスク** が含まれています。

- **[SSIS Build](#ssis-build-task)** タスクでは、プロジェクト デプロイ モデルまたはパッケージ デプロイ モデルでの dtproj ファイルのビルドがサポートされます。

- **[SSIS Deploy](#ssis-deploy-task)** タスクでは、1 つまたは複数の ispac ファイルをオンプレミスの SSIS カタログと Azure-SSIS IR にデプロイしたり、SSISDeploymentManifest ファイルとその関連ファイルをオンプレミスまたは Azure ファイル共有にデプロイしたりできます。

- **[SSIS Catalog Configuration](#ssis-catalog-configuration-task)** タスクでは、JSON 形式の構成ファイルを使用した SSIS カタログのフォルダー、プロジェクト、環境の構成がサポートされます。 このタスクでは次のシナリオがサポートされます。
    - Folder
        - フォルダーを作成します。
        - フォルダーの説明を更新します。
    - Project
        - パラメーターの値を構成します。literal 値と referenced 値の両方がサポートされます。
        - 環境参照を追加します。
    - 環境
        - 環境を作成します。
        - 環境の説明を更新します。
        - 環境変数を作成または更新します。

## <a name="ssis-build-task"></a>SSIS Build タスク

![ビルド タスク](media/ssis-build-task.png)

### <a name="properties"></a>Properties

#### <a name="project-path"></a>プロジェクト パス

ビルドするプロジェクト フォルダーまたはファイルのパス。 フォルダー パスが指定されている場合、SSIS Build タスクでは、このフォルダーの下にあるすべての dtproj ファイルが繰り返し検索され、すべてビルドされます。

プロジェクト パスを " *空* " にすることはできません。 **.** として設定して、 リポジトリのルート フォルダーからビルドします。

#### <a name="project-configuration"></a>プロジェクトの構成

ビルドに使用されるプロジェクト構成の名前。 指定されていない場合、各 dtproj ファイルに最初に定義されているプロジェクト構成が選択されます。

#### <a name="output-path"></a>[出力パス]

[ビルド成果物の公開タスク](/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops)によってビルド成果物として公開できるビルド結果を保存するための個別フォルダーのパス。

### <a name="limitations-and-known-issues"></a>制限事項と既知の問題

- SSIS Build タスクは Visual Studio と、ビルド エージェントで必須となる SSIS デザイナーに依存します。 そのため、パイプラインで SSIS Build タスクを実行するには、Microsoft によってホストされるエージェントに **vs2017-win2016** を選択するか、自己ホスト エージェントに Visual Studio と SSIS デザイナー (VS2017 + SSDT2017 または VS2019 + SSIS Projects 拡張機能) をインストールする必要があります。

- 面倒な設定の要らないコンポーネント (SSIS Azure Feature Pack やその他のサードパーティ コンポーネント) を利用して SSIS プロジェクトをビルドするには、パイプライン エージェントが実行されているコンピューターにそのようなコンポーネントをインストールする必要があります。  Microsoft によってホストされるエージェントの場合、[PowerShell Script タスク](/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops)または [Command Line Script タスク](/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops)を追加してコンポーネントをダウンロードし、インストールしてから SSIS Build タスクを実行できます。 次に示すのは、Azure Feature Pack をインストールするための PowerShell のサンプル スクリプトです。 

```powershell
wget -Uri https://download.microsoft.com/download/E/E/0/EE0CB6A0-4105-466D-A7CA-5E39FA9AB128/SsisAzureFeaturePack_2017_x86.msi -OutFile AFP.msi

start -Wait -FilePath msiexec -Args "/i AFP.msi /quiet /l* log.txt"

cat log.txt
```

- 保護レベルの **EncryptSensitiveWithPassword** と **EncryptAllWithPassword** は SSIS Build タスクではサポートされていません。 コードベースのいずれの SSIS プロジェクトでもこの 2 つの保護レベルが使用されていないことを確認してください。使用されている場合、SSIS Build タスクの実行中、応答が停止し、タイムアウトになります。

## <a name="ssis-deploy-task"></a>SSIS Deploy タスク

![デプロイ タスク](media/ssis-deploy-task.png)

### <a name="properties"></a>Properties

#### <a name="source-path"></a>ソース パス

デプロイするソース ISPAC ファイルまたは SSISDeploymentManifest ファイルのパス。 このパスはフォルダー パスやファイル パスになることがあります。

#### <a name="destination-type"></a>変換先の型

デプロイ先の種類。 SSIS Deploy タスクでは現在、2 つの種類がサポートされています。

- *ファイル システム* :SSISDeploymentManifest ファイルとその関連ファイルを指定のファイル システムにデプロイします。 オンプレミスと Azure ファイル共有の両方がサポートされています。
- *SSISDB* :オンプレミスの SQL Server または Azure-SSIS Integration Runtime でホストできる指定の SSIS カタログに ISPAC ファイルをデプロイします。

#### <a name="destination-server"></a>[転送先サーバー]

宛先となる SQL サーバーの名前。 これは、オンプレミスの SQL Server、Azure SQL Database、または Azure SQL Managed Instance の名前にすることができます。 このプロパティは、宛先の種類が SSISDB の場合にのみ表示されます。

#### <a name="destination-path"></a>宛先のパス

ソース ファイルがデプロイされる宛先フォルダーのパス。 次に例を示します。

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

フォルダーやサブフォルダーが存在しない場合、SSIS Deploy タスクによって作成されます。

#### <a name="authentication-type"></a>認証の種類

指定の宛先サーバーにアクセスするための認証の種類。 このプロパティは、宛先の種類が SSISDB の場合にのみ表示されます。 一般に、以下の認証の種類がサポートされています。

- Windows 認証
- SQL Server 認証
- Active Directory - パスワード
- Active Directory - 統合

しかし、特定の種類の認証がサポートされるかどうかは、宛先サーバーの種類やエージェントの種類によって異なります。 サポート マトリックスの詳細を一覧にしたものが下の表になります。

|宛先サーバーの種類|Microsoft によってホストされるエージェント|自己ホスト エージェント|
|---------|---------|---------|
|オンプレミスの SQL サーバーまたは VM |該当なし|Windows 認証|
|Azure SQL|SQL Server 認証 <br> Active Directory - パスワード|SQL Server 認証 <br> Active Directory - パスワード <br> Active Directory - 統合|

#### <a name="domain-name"></a>ドメイン名

指定のファイル システムにアクセスするためのドメイン名。 このプロパティは、宛先の種類がファイル システムの場合にのみ表示されます。
自己ホスト エージェントを実行するユーザー アカウントに指定の宛先パスの読み取り/書き込みアクセスが付与されている場合、この項目は空のまま残すことができます。

#### <a name="username"></a>ユーザー名

指定のファイル システムまたは SSISDB にアクセスするためのユーザー名。 このプロパティは宛先の種類がファイル システムの場合か、認証の種類が SQL Server 認証か "アクティブ ディレクトリ - パスワード" の場合に表示されます。
宛先の種類がファイル システムであり、自己ホスト エージェントを実行するユーザー アカウントに指定の宛先パスの読み取り/書き込みアクセスが付与されている場合、この項目は空のまま残すことができます。

#### <a name="password"></a>Password

指定のファイル システムまたは SSISDB にアクセスするためのパスワード。 このプロパティは宛先の種類がファイル システムの場合か、認証の種類が SQL Server 認証か "アクティブ ディレクトリ - パスワード" の場合に表示されます。
宛先の種類がファイル システムであり、自己ホスト エージェントを実行するユーザー アカウントに指定の宛先パスの読み取り/書き込みアクセスが付与されている場合、この項目は空のまま残すことができます。

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>同じ名前の既存のプロジェクトまたは SSISDeploymentManifest ファイルを上書きする

同じ名前の既存のプロジェクトまたは SSISDeploymentManifest ファイルを上書きするかどうかを指定します。 "いいえ" の場合、SSIS Deploy では、そのようなプロジェクトまたはファイルのデプロイがスキップされます。

#### <a name="continue-deployment-when-error-occurs"></a>エラーの発生時にデプロイを続行する

エラーの発生時に残りのプロジェクトまたはファイルのデプロイを続行するかどうかを指定します。 "いいえ" の場合、エラーの発生直後に SSIS Deploy タスクが停止します。

### <a name="limitations-and-known-issues"></a>制限事項と既知の問題

SSIS Deploy タスクでは、現在、次のシナリオはサポートされていません。

- SSIS カタログで環境を構成する。
- 多要素認証 (MFA) のみが許可される Azure SQL Server または Azure SQL マネージド インスタンスに ispac をデプロイする。
- MSDB または SSIS パッケージ ストアにパッケージをデプロイする。

## <a name="ssis-catalog-configuration-task"></a>SSIS Catalog Configuration タスク

![catalog configuration タスク](media/ssis-catalog-configuation-task.png)

### <a name="properties"></a>Properties

#### <a name="configuration-file-source"></a>構成ファイルのソース

SSIS カタログ構成 JSON ファイルのソース。 [ファイル パス] または [インライン] にすることができます。

[構成 JSON を定義する](#define-configuration-json)方法の詳細を参照してください。

- [インライン構成 JSON のサンプル](#a-sample-inline-configuration-json)を参照してください。
- [JSON スキーマ](#json-schema)を確認してください。

#### <a name="configuration-json-file-path"></a>構成 JSON ファイルのパス

SSIS カタログ構成 JSON ファイルのパス。 このプロパティは、構成ファイル ソースとして [ファイル パス] を選択した場合にのみ表示されます。

構成 JSON ファイルで[パイプライン変数](/azure/devops/pipelines/process/variables)を使用するには、このタスクの前に [File Transform タスク](/azure/devops/pipelines/tasks/utility/file-transform?view=azure-devops)を追加して、構成値をパイプライン変数に置き換える必要があります。 詳細については、「[JSON 変数置換](/azure/devops/pipelines/tasks/transforms-variable-substitution?tabs=Classic&view=azure-devops#json-variable-substitution)」を参照してください。

#### <a name="inline-configuration-json"></a>インライン構成 JSON

SSIS カタログ構成のインライン JSON。 このプロパティは、構成ファイル ソースとして "インライン" を選択した場合にのみ表示されます。 パイプライン変数は直接使用できます。

#### <a name="roll-back-configuration-when-error-occurs"></a>エラーが発生したときに構成をロールバックする

エラーが発生したときに、このタスクによって行われた構成をロールバックするかどうか。

#### <a name="target-server"></a>ターゲット サーバー

ターゲット SQL Server の名前。 これは、オンプレミスの SQL Server、Azure SQL Database、または Azure SQL Managed Instance の名前にすることができます。

#### <a name="authentication-type"></a>認証の種類

指定されたターゲット サーバーにアクセスするための認証の種類。 一般に、以下の認証の種類がサポートされています。

- Windows 認証
- SQL Server 認証
- Active Directory - パスワード
- Active Directory - 統合

しかし、特定の種類の認証がサポートされるかどうかは、宛先サーバーの種類やエージェントの種類によって異なります。 サポート マトリックスの詳細を一覧にしたものが下の表になります。

|宛先サーバーの種類|Microsoft によってホストされるエージェント|自己ホスト エージェント|
|---------|---------|---------|
|オンプレミスの SQL サーバーまたは VM |該当なし|Windows 認証|
|Azure SQL|SQL Server 認証 <br> Active Directory - パスワード|SQL Server 認証 <br> Active Directory - パスワード <br> Active Directory - 統合|

#### <a name="username"></a>ユーザー名

ターゲット SQL Server にアクセスするためのユーザー名。 このプロパティは、認証の種類が SQL Server 認証またはアクティブ ディレクトリ - パスワードの場合にのみ表示されます。

#### <a name="password"></a>Password

ターゲット SQL Server にアクセスするためのパスワード。 このプロパティは、認証の種類が SQL Server 認証またはアクティブ ディレクトリ - パスワードの場合にのみ表示されます。

### <a name="define-configuration-json"></a>構成 JSON を定義する

構成 JSON スキーマには、次の 3 つの層があります。

- catalog
- folder
- project と environment

![カタログ構成スキーマ](media/catalog-configuration-schema.png)

#### <a name="a-sample-inline-configuration-json"></a>インライン構成 JSON のサンプル

```json
{
  "folders": [
    {
      "name": "devopsdemo",
      "description": "devops demo folder",
      "projects": [
        {
          "name": "catalog devops",
          "parameters": [
            {
              "name": "password",
              "container": "Package.dtsx",
              "value": "passwd",
              "valueType": "referenced"
            },
            {
              "name": "serverName",
              "container": "catalog devops",
              "value": "localhost",
              "valueType": "literal"
            }
          ],
          "references": [
            {
              "environmentName": "test",
              "environmentFolder": "devopsdemo"
            },
            {
              "environmentName": "test",
              "environmentFolder": "."
            }
          ]
        }
      ],
      "environments": [
        {
          "name": "test",
          "description": "test",
          "variables": [
            {
              "name": "passwd",
              "type": "string",
              "description": "",
              "value": "$(SSISDBServerAdminPassword)",
              "sensitive": true
            },
            {
              "name": "serverName",
              "type": "string",
              "description": "",
              "value": "$(TargetServerName)",
              "sensitive": false
            }
          ]
        }
      ]
    }
  ]
}
```

#### <a name="json-schema"></a>JSON スキーマ

##### <a name="catalog-attributes"></a>カタログ属性

|プロパティ  |説明  |Notes  |
|---------|---------|---------|
|フォルダー  |フォルダー オブジェクトの配列。 各オブジェクトには、カタログ フォルダーの構成情報が含まれています。|フォルダー オブジェクトのスキーマについては、「 *フォルダー属性* 」を参照してください。|

##### <a name="folder-attributes"></a>フォルダー属性

|プロパティ  |説明  |メモ  |
|---------|---------|---------|
|name  |カタログ フォルダーの名前。|フォルダーが存在しない場合は作成されます。|
|description|カタログ フォルダーの説明。|*null* の値はスキップされます。|
|projects|プロジェクト オブジェクトの配列。 各オブジェクトには、プロジェクトの構成情報が含まれています。|プロジェクト オブジェクトのスキーマについては、「 *プロジェクト属性* 」を参照してください。|
|環境|環境オブジェクトの配列。 各オブジェクトには、環境の構成情報が含まれています。|環境オブジェクトのスキーマについては、「 *環境属性* 」を参照してください。|

##### <a name="project-attributes"></a>プロジェクト属性

|プロパティ  |説明  |メモ  |
|---------|---------|---------|
|name|プロジェクトの名前。 |プロジェクトが親フォルダーに存在しない場合、プロジェクト オブジェクトはスキップされます。|
|parameters|パラメーター オブジェクトの配列です。 各オブジェクトには、パラメーターの構成情報が含まれています。|パラメーター オブジェクトのスキーマについては、「 *パラメーター属性* 」を参照してください。|
|references|参照オブジェクトの配列。 各オブジェクトは、ターゲット プロジェクトへの環境参照を表します。|参照オブジェクトのスキーマについては、「 *参照属性* 」を参照してください。|

##### <a name="parameter-attributes"></a>パラメーター属性

|プロパティ  |説明  |メモ  |
|---------|---------|---------|
|name|パラメーターの名前。|<li>パラメーターには、プロジェクト パラメーターまたはパッケージ パラメーターを使用できます。 <li>存在しない場合は、パラメーターはスキップされます。 <li>パラメーターが接続マネージャー プロパティの場合、名前は **CM.\<Connection Manager Name>.\<Property Name>** の形式である必要があります。 |
|container|パラメーターのコンテナー。|<li>パラメーターがプロジェクト パラメーターの場合、 *container* はプロジェクト名である必要があります。 <li>パッケージ パラメーターの場合、 *container* は、拡張子が **.dtsx** のパッケージ名である必要があります。|
|value|パラメーターの値。|<li>*valueType* が *referenced* の場合: 値は *string* 型の環境変数への参照です。 <li> *valueType* が *literal* の場合: この属性では、任意の有効な " *ブール値* "、" *数値* "、および " *文字列* " の JSON 値がサポートされます。 <li> 値は、ターゲット パラメーターの型に変換されます。 変換できない場合はエラーが発生します。<li> *null* の値は無効です。 タスクではこのパラメーター オブジェクトがスキップされ、警告が示されます。|
|valueType|パラメーター値の型。|有効な型は次のとおりです。 <br> *literal* : *value* 属性はリテラル値を表します。 <br> *referenced* : *value* 属性は、環境変数への参照を表します。|

##### <a name="reference-attributes"></a>参照属性

|プロパティ  |説明  |Notes  |
|---------|---------|---------|
|environmentFolder|環境のフォルダー名。|フォルダーが存在しない場合は作成されます。 <br> 値は "." にすることができます。これは、環境を参照する、プロジェクトの親フォルダーを表します。|
|environmentName|参照先環境の名前。|存在しない場合は、指定された環境が作成されます。|

##### <a name="environment-attributes"></a>環境属性

|プロパティ  |説明  |メモ  |
|---------|---------|---------|
|name|環境の名前。|環境が存在しない場合は作成されます。|
|description|環境の説明。|*null* の値はスキップされます。|
|variables|変数オブジェクトの配列。|各オブジェクトには、環境変数の構成情報が含まれています。変数オブジェクトのスキーマについては、「 *変数属性* 」を参照してください。|

##### <a name="variable-attributes"></a>変数属性

|プロパティ  |説明  |メモ  |
|---------|---------|---------|
|name|環境変数の名前。|環境変数が存在しない場合は作成されます。|
|type|環境変数のデータ型。|有効な型は次のとおりです。 <br> *boolean* <br> *byte* <br> *datetime* <br> decimal <br> *double* <br> *int16* <br> *int32* <br> *int64* <br> *sbyte* <br> *single* <br> *string* <br> *uint32* <br> *uint64*|
|description|環境変数の説明。|*null* の値はスキップされます。|
|value|環境変数の値。|この属性では、任意の有効なブール値、数値、および文字列の JSON 値がサポートされます。<br> 値は **type** 属性によって指定された型に変換されます。 変換に失敗すると、エラーが発生します。<br>*null* の値は無効です。 タスクではこの環境変数オブジェクトがスキップされ、警告が示されます。|
|sensitive|環境変数の値が機微であるかどうか。|有効な入力は次のとおりです。 <br> *true* <br> *false*|

## <a name="release-notes"></a>リリース ノート

### <a name="version-103"></a>バージョン 1.0.3

リリース日:2020 年 10 月 21 日

- SSIS Deploy タスクと SSIS Catalog Configuration タスクに接続文字列サフィックスを指定できます。

### <a name="version-102"></a>バージョン 1.0.2

リリース日:2020 年 5 月 26 日

- 構成作業が完了した後に SSIS Catalog Configuration タスクが失敗する場合があるという問題を修正しました。

### <a name="version-101"></a>Version 1.0.1

リリース日:2020 年 5 月 9 日

- プロジェクト パスとして 1 つの dtproj ファイルのみが指定されている場合でも、SSIS ビルド タスクによって常にソリューション全体がビルドされる問題を修正しました。

### <a name="version-100"></a>バージョン 1.0.0

リリース日:2020 年 5 月 8 日

- 一般公開 (GA) リリース。
- エージェントに対する .NET Framework の最小バージョンに制限が追加されました。 現在、.NET Framework の最小バージョンは 4.6.2 です。
- SSIS Build タスクと SSIS Deploy タスクの説明が改善されました。

### <a name="version-020-preview"></a>バージョン 0.2.0 プレビュー

リリース日:2020 年 3 月 31 日

- SSIS Catalog Configuration タスクを追加します。

### <a name="version-013-preview"></a>バージョン 0.1.3 プレビュー

リリース日:2020 年 1 月 19 日

- 元のファイル名が変更された場合に、ispac を展開できない問題を修正しました。

### <a name="version-012-preview"></a>バージョン 0.1.2 Preview

リリース日:2020 年 1 月 13 日

- 宛先の種類が SSISDB である場合、SSIS Deploy タスク ログにより詳細な例外情報が追加されていましす。
- SSIS Deploy タスクのプロパティ Destination パスのヘルプ テキスト内の宛先パスの例が修正されています。

### <a name="version-011-preview"></a>バージョン 0.1.1 プレビュー

リリース日:2020 年 1 月 6 日

- 最小エージェント バージョン要件の制約が追加されました。 現在、この製品の最小エージェント バージョンは 2.144.0 です。
- SSIS Deploy タスクの表示テキストの間違いがいくつか修正されました。
- エラー メッセージがいくつか改善されました。

### <a name="version-010-preview"></a>バージョン 0.1.0 プレビュー

リリース日:2019 年 12 月 5 日

SSIS DevOps ツールの初回リリース。 これはプレビュー リリースです。

## <a name="next-steps"></a>次のステップ

- [SSIS DevOps 拡張機能](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)を入手してください
