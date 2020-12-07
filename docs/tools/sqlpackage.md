---
title: SqlPackage.exe
description: SqlPackage.exe を使用してデータベース開発タスクを自動化する方法について説明します。 例と使用可能なパラメーター、プロパティ、および SQLCMD 変数を表示します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: ee78b145965c17ff0a496611c6506d23df1a31a3
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384501"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

**SqlPackage.exe** は、次のデータベース開発タスクを自動化するコマンド ライン ユーティリティです。  
  
- [バージョン](#version):SqlPackage アプリケーションのビルド番号が返されます。  バージョン 18.6 で追加されました。

- [Extract](#extract-parameters-and-properties): ライブ SQL Server または Azure SQL Database からデータベース スナップショット (.dacpac) ファイルを作成します。  
  
- [発行](#publish-parameters-properties-and-sqlcmd-variables):ソース .dacpac ファイルのスキーマに合わせてデータベース スキーマの増分更新を行います。 データベースがサーバーに存在しない場合は、公開操作によって作成されます。 存在する場合は、既存のデータベースが更新されます。  
  
- [Export](#export-parameters-and-properties):SQL Server または Azure SQL Database のライブ データベース (データベース スキーマとユーザー データを含む) を BACPAC パッケージ (.bacpac ファイル) にエクスポートします。  
  
- [Import](#import-parameters-and-properties):BACPAC パッケージのスキーマとテーブル データを、SQL Server または Azure SQL Database インスタンス内の新しいユーザー データベースにインポートします。  
  
- [DeployReport](#deployreport-parameters-and-properties): 公開操作によって行われる変更の XML レポートを作成します。  
  
- [DriftReport](#driftreport-parameters):登録されたデータベースに対して最終登録以降に行われた変更に関する XML レポートを作成します。  
  
- [Script](#script-parameters-and-properties): ソースのスキーマに合わせてターゲットのスキーマを更新する、Transact-SQL の増分更新スクリプトを作成します。  
  
**SqlPackage.exe** コマンド ラインでは、これらの操作と共に、操作固有のパラメーターおよびプロパティを指定できます。  

**[最新バージョンをダウンロード](sqlpackage-download.md)** します。 最新リリースに関する詳細については、[リリース ノート](release-notes-sqlpackage.md)をご覧ください。
  
## <a name="command-line-syntax"></a>コマンド ライン構文

**SqlPackage.exe** は、コマンド ラインで指定されたパラメーター、プロパティ、および SQLCMD 変数を使用して指定された操作を開始します。  
  
```
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```

### <a name="usage-examples"></a>使用例

**SQL スクリプト出力で .dacpac ファイルを使用してデータベース間の比較を生成する**

まず、最新のデータベース変更の .dacpac ファイルを作成します。

```
sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_current_version.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```
 
(変更がない) データベース ターゲットの .dacpac ファイルを作成します。

 ```
 sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```

2 つの .dacpac ファイルの相違点を生成する SQL スクリプトを作成します。

```
sqlpackage.exe /Action:Script /SourceFile:"C:\sqlpackageoutput\output_current_version.dacpac" /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /TargetDatabaseName:"Contoso.Database" /OutputPath:"C:\sqlpackageoutput\output.sql"
 ```


## <a name="version"></a>Version

sqlpackage のバージョンをビルド番号として表示します。  対話型プロンプトだけでなく、[自動化されたパイプライン](sqlpackage-pipelines.md)でも使用できます。

```
sqlpackage.exe /Version
 ```


## <a name="extract-parameters-and-properties"></a>抽出パラメーターとプロパティ
SqlPackage.exe の Extract 操作を実行すると、SQL Server または Azure SQL Database から DACPAC パッケージ (.dacpac ファイル) へのライブ データベースのスキーマが作成されます。 既定では、データは .dacpac ファイルに含まれません。 データを含めるには、[Export アクション](#export-parameters-and-properties)を使用します。 

### <a name="help-for-the-extract-action"></a>抽出アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|Extract|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe が既存のファイルを上書きするかどうかを指定します。 False を指定すると、既存のファイルが検出された場合に sqlpackage.exe の操作が中止します。 既定値は True です。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|操作固有のプロパティの名前と値のペア ({PropertyName}={Value}) を指定します。 操作のプロパティ名については、特定の操作のヘルプを参照してください。 例: sqlpackage.exe /Action:Extract /?。 |
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。 |
|**/SourceConnectionString:**|**/scs**|{string}|ソース データベースの有効な SQL Server または SQL Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのソース パラメーターとも同時には使用できません。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|ソース データベースの名前を定義します。 |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|ソース データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用するパスワードを定義します。 |
|**/SourceServerName:**|**/ssn**|{string}|ソース データベースをホストしているサーバーの名前を定義します。 |
|**/SourceTimeout:**|**/st**|{int}|ソース データベースへの接続を確立する際のタイムアウトを秒単位で指定します。 |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|TLS を使用してソース データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/SourceUser:**|**/su**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TargetFile:**|**/tf**|{string}| データベースではなく、ターゲット ファイル (.dacpac ファイル) をアクションのターゲットとして使用するように指定します。 このパラメーターを使用した場合、他のターゲット パラメーターは無効になります。 このパラメーターは、データベース ターゲットのみをサポートするアクションに対しては無効です。| 
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|

### <a name="properties-specific-to-the-extract-action"></a>抽出アクションに固有のプロパティ

|プロパティ|値|説明|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server に対してクエリを実行するときのコマンドのタイムアウト (秒) を指定します。|
|**/p:**|DacApplicationDescription=(STRING)|DACPAC メタデータに格納されるアプリケーションの説明を定義します。|
|**/p:**|DacApplicationName=(STRING)|DACPAC メタデータに格納されるアプリケーション名を定義します。 既定値は、データベース名です。|
|**/p:**|DacMajorVersion=(INT32 '1')|DACPAC メタデータに格納されるメジャー バージョンを定義します。|
|**/p:**|DacMinorVersion=(INT32 '0')|DACPAC メタデータに格納されるマイナー バージョンを定義します。|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer に対してクエリを実行するときのデータベース ロックのタイムアウトを秒単位で指定します。 無期限に待機するには、-1 を使用します。|
|**/p:**|ExtractAllTableData=(BOOLEAN)|すべてのユーザー テーブルのデータを抽出するかどうかを示します。 "true" の場合、すべてのユーザー テーブルのデータが抽出されます。個々のユーザー テーブルを指定してデータを抽出することはできません。 "false" の場合、データの抽出元ユーザー テーブルを 1 つ以上指定します。|
|**/p:**|ExtractApplicationScopedObjectsOnly=(BOOLEAN 'True')|true の場合、指定されたソースのアプリケーション スコープのオブジェクトのみを抽出します。 false の場合、指定されたソースのすべてのオブジェクトを抽出します。|
|**/p:**|ExtractReferencedServerScopedElements=(BOOLEAN 'True')|true の場合、ソース データベース オブジェクトによって参照されるログイン オブジェクト、サーバー監査オブジェクト、および資格情報オブジェクトを抽出します。|
|**/p:**|ExtractUsageProperties=(BOOLEAN)|テーブル行数やインデックス サイズなどの使用プロパティを、データベースから抽出するかどうかを指定します。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|拡張プロパティを無視するかどうかを指定します。|
|**/p:**|IgnorePermissions=(BOOLEAN 'True')|アクセス許可を無視するかどうかを指定します。|
|**/p:**|IgnoreUserLoginMappings=(BOOLEAN)|ユーザーとログイン間のリレーションシップを無視するかどうかを指定します。|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server に対してクエリを実行するときの実行時間の長いコマンドのタイムアウトを秒単位で指定します。 無期限に待機するには、0 を使用します。|
|**/p:**|Storage=({File&#124;Memory} 'File')|抽出時に使用されるスキーマ モデルのバックアップ用ストレージの種類を指定します。|
|**/p:**|TableData=(STRING)|データの抽出元テーブルを示します。 テーブル名は次の形式で指定してください: schema_name.table_identifier。名前部分はかっこで囲んでも囲まなくても構いません。 このオプションは、複数回指定できます。|
|**/p:**| TempDirectoryForTableData=(STRING)|パッケージ ファイルに書き込む前にテーブル データをバッファーするために使用する、一時ディレクトリを指定します。|
|**/p:**|VerifyExtraction=(BOOLEAN)|抽出された DACPAC を検証するかどうかを指定します。|

## <a name="publish-parameters-properties-and-sqlcmd-variables"></a>Publish のパラメーター、プロパティ、および SQLCMD 変数

SqlPackage.exe の公開操作では、ソース データベースの構造に合わせて、ターゲット データベースのスキーマの増分更新を行います。 すべてまたは一部のテーブルのユーザー データを含む配置パッケージを公開すると、スキーマに加え、テーブル データが更新されます。 データの配置により、ターゲット データベースの既存のテーブル内のスキーマとデータが上書きされます。 データの配置では、配置パッケージに含まれていないテーブルについて、ターゲット データベース内の既存のスキーマまたはデータは変更されません。  

### <a name="help-for-publish-action"></a>公開アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|発行|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/AzureKeyVaultAuthMethod:**|**/akv**|{Interactive&#124;ClientIdSecret}|公開操作に暗号化されているテーブルや列の変更が含まれている場合、Azure Key Vault にアクセスするためにどの認証方法を使用するかを指定します。 |
|**/ClientId:**|**/cid**|{string}|必要な場合、Azure Key Vault に対する認証に使用されるクライアント ID を指定します |
|**/DeployScriptPath:**|**/dsp**|{string}|配置スクリプトを出力する省略可能なファイル パスを指定します。 Azure の配置では、master データベースを作成または変更するための TSQL コマンドがある場合、スクリプトは同じパスに書き込まれますが、出力ファイル名として "Filename_Master.sql" が使用されます。 |
|**/DeployReportPath:**|**/drp**|{string}|配置レポートの xml ファイルを出力する省略可能なファイル パスを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe が既存のファイルを上書きするかどうかを指定します。 False を指定すると、既存のファイルが検出された場合に sqlpackage.exe の操作が中止します。 既定値は True です。 |
|**/Profile:**|**/pr**|{string}|DAC 公開プロファイルのファイル パスを指定します。 出力の生成時に使用するプロパティと変数のコレクションをプロファイルで定義します。|
|**/Properties:**|**/p**|{PropertyName}={Value}|操作固有のプロパティの名前と値のペア ({PropertyName}={Value}) を指定します。 操作のプロパティ名については、特定の操作のヘルプを参照してください。 例: sqlpackage.exe /Action:Publish /?。|
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。|
|**/Secret:**|**/secr**|{string}|必要な場合、Azure Key Vault に対する認証に使用されるクライアント シークレットを指定します |
|**/SourceConnectionString:**|**/scs**|{string}|ソース データベースの有効な SQL Server または SQL Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのソース パラメーターとも同時には使用できません。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|ソース データベースの名前を定義します。 |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|ソース データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/SourceFile:**|**/sf**|{string}|データベースではなく、ソース ファイルを操作のソースとして使用するように指定します。 このパラメーターを使用した場合、他のソース パラメーターは無効になります。 |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用するパスワードを定義します。 |
|**/SourceServerName:**|**/ssn**|{string}|ソース データベースをホストしているサーバーの名前を定義します。 |
|**/SourceTimeout:**|**/st**|{int}|ソース データベースへの接続を確立する際のタイムアウトを秒単位で指定します。 |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|TLS を使用してソース データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/SourceUser:**|**/su**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TargetConnectionString:**|**/tcs**|{string}|ターゲット データベースの有効な SQL Server または Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのターゲット パラメーターとも同時には使用できません。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe の動作のターゲットとなるデータベースの名前のオーバーライドを指定します。 |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|ターゲット データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/TargetPassword:**|**/tp**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用するパスワードを定義します。 |
|**/TargetServerName:**|**/tsn**|{string}|ターゲット データベースをホストしているサーバーの名前を定義します。 |
|**/TargetTimeout:**|**/tt**|{int}|ターゲット データベースへの接続を確立するためのタイムアウトを秒単位で指定します。 Azure AD の場合、この値は 30 秒以上にすることをお勧めします。|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|TLS を使用してターゲット データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/TargetUser:**|**/tu**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/Variables:**|**/v**|{PropertyName}={Value}|操作固有の変数の名前と値のペア ({VariableName}={Value}) を指定します。 DACPAC ファイルには、有効な SQLCMD 変数の一覧が含まれます。 すべての変数に値を指定しないと、エラーが発生します。 |

### <a name="properties-specific-to-the-publish-action"></a>公開アクションに固有のプロパティ

|プロパティ|値|説明|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|配置コントリビューターに追加の配置コントリビューター引数を指定します。 複数の値を指定する場合は、セミコロンで区切ります。|
|**/p:**|AdditionalDeploymentContributors=(STRING)|dacpac を配置するときに実行する必要がある、追加の配置コントリビューターを指定します。 このとき、セミコロン区切りで、完全修飾ビルド コントリビューター名または ID を指定する必要があります。|
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| 追加の配置コントリビューターを読み込むためのパスを指定します。 複数の値を指定する場合は、セミコロンで区切ります。 | 
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|このプロパティは、ブロックしているアセンブリを配置計画から削除する際に SqlClr の配置によって使用されます。 既定では、参照しているアセンブリを削除する必要がある場合、ブロックまたは参照しているアセンブリによって、アセンブリの更新がブロックされます。|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|互換性がない SQL Server プラットフォームであっても操作を試行するかどうかを指定します。|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|このプロパティが true に設定されている場合は、行レベル セキュリティを使用するテーブルに対するデータ モーションをブロックしません。 既定値は false です。|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|変更を配置する前にデータベースをバックアップします。|
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|公開操作によるデータ損失の可能性がある場合に、公開を終了するかどうかを指定します。|
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|スキーマがその登録と一致しないか、スキーマが登録されていないデータベースの更新をブロックするかどうかを指定します。|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server に対してクエリを実行するときのコマンドのタイムアウト (秒) を指定します。|
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|生成する公開スクリプトで SETVAR 変数の宣言をコメント アウトするかどうかを指定します。 このようなコメント アウトが必要になるのは、SQLCMD.EXE などのツールを使用して、公開時にコマンド ラインで値を指定する予定がある場合などです。|
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|この設定では、配置の際にデータベースの照合順序をどのように処理するかを指定します。既定では、ソースで指定されている照合順序と異なる場合にターゲット データベースの照合順序が更新されます。 このオプションを設定した場合、ターゲット データベース (またはサーバー) の照合順序が使用されます。|
|**/p:**|CreateNewDatabase=(BOOLEAN)|データベースへの公開時に、ターゲット データベースを更新するか、削除して再作成するかを指定します。|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database のエディションを定義します。|
|**/p:**|DatabaseLockTimeout=(INT32 '60')|SQLServer に対してクエリを実行するときのデータベース ロックのタイムアウトを秒単位で指定します。 無期限に待機するには、-1 を使用します。|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database の最大サイズを GB 単位で定義します。|
|**/p:**|DatabaseServiceObjective=(STRING)|Azure SQL Database のパフォーマンス レベル ("P0" や "S1" など) を定義します。|
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|true の場合、データベースは配置前にシングル ユーザー モードに設定されます。|
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')|公開プロセスの開始時にデータ定義言語 (DDL) トリガーを無効にして、公開操作の最後に再度有効にするかどうかを指定します。|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|true の場合、Change Data Capture オブジェクトは変更されません。|
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|レプリケートされたオブジェクトが、検証時に識別されるかどうかを指定します。|
|**/p:**|DoNotDropObjectType=(STRING)|DropObjectsNotInSource が true の場合、削除されないオブジェクトの種類。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|DoNotDropObjectTypes=(STRING)|DropObjectsNotInSource が true の場合に削除されない、オブジェクトの種類のセミコロン区切りリスト。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しない制約を削除するかどうかを指定します。|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しない DML トリガーを削除するかどうかを指定します。|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない拡張プロパティをターゲット データベースから削除するかどうかを指定します。|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しないインデックスを削除するかどうかを指定します。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|データベースへの公開時に、データベース スナップショット (.dacpac) ファイルに存在しないオブジェクトをターゲット データベースから削除するかどうかを指定します。 この値は DropExtendedProperties よりも優先されます。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|データベースへの更新の公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しないアクセス許可を削除するかどうかを指定します。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|データベースへの更新の公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルで定義されていないロール メンバーを削除するかどうかを指定します。|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない統計をターゲット データベースから削除するかどうかを指定します。|
|**/p:**|ExcludeObjectType=(STRING)|配置時に無視するオブジェクトの種類。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|ExcludeObjectTypes=(STRING)|配置時に無視するオブジェクトの種類のセミコロン区切りリスト。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|null 値が許可されない列を含むデータが格納されているテーブルを更新する際に、自動的に既定値が設定されます。|
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|データベースに公開するとき、ANSI NULLS 設定の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|データベースに公開するとき、Authorizer の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|データベースに公開するとき、列の照合順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|データベースに公開するときに、テーブル列の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreComments=(BOOLEAN)|データベースに公開するとき、コメントの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|データベースに公開するとき、暗号化プロバイダーのファイル パスの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|データベースまたはサーバーに公開するとき、Data Definition Language (DDL) triggers の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|データベースに公開するとき、Data Definition Language (DDL) triggers の有効または無効にされた状態の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|データベースに公開するとき、既定のスキーマの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|データベースに公開するとき、Data Manipulation Language (DML) triggers の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|データベースに公開するとき、DML triggers の有効または無効にされた状態の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|データベースに公開するとき、拡張プロパティの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|データベースに公開するとき、ファイルおよびログ ファイルのパスの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|データベースに公開するとき、FILEGROUP 内のオブジェクトの位置の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|データベースに公開するとき、ファイル サイズの相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|データベースに公開するとき、インデックス格納の FILL FACTOR の相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|データベースに公開するとき、フルテキスト カタログのファイル パスの相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|データベースに公開するとき、Identity 列のシードの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreIncrement=(BOOLEAN)|データベースに公開するとき、Identity 列のインクリメントの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|データベースに公開するとき、インデックス オプションの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|データベースに公開するとき、インデックス パディングの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|データベースに公開するとき、キーワードの大文字と小文字の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|データベースに公開するとき、インデックスのロック ヒントの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')|データベースに公開するとき、セキュリティ ID 番号 (SID) の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|データベースに公開するとき、レプリケーションでは使わない設定を無視するか、更新するかを指定します。|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|データベースに公開するとき、パーティション構成でのオブジェクトの位置を無視するか、更新するかを指定します。|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|データベースに公開するとき、パーティション構成と関数の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnorePermissions=(BOOLEAN)|データベースに公開するとき、権限の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|データベースに公開するとき、引用符で囲まれた識別子の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|データベースへの公開時に、ログインのロール メンバーシップの相違を無視するか更新するかを指定します。|
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|データベースへの公開時に、SQL Server がルーティング テーブルにルートを保持する時間の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|データベースに公開するとき、T-SQL ステートメント間のセミコロンの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|データベースに公開するとき、テーブル オプションの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|データベースに公開するとき、テーブル パーティション オプションの相違を無視するか、更新するかを指定します。  このオプションは、Azure Synapse Analytics SQL プール (データ ウェアハウス) データベースにのみ適用されます。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|データベースに公開するとき、ユーザー設定オブジェクトの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|データベースに公開するとき、空白の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|公開時に、CHECK 制約の WITH NOCHECK 句の値の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|データベースに公開するとき、外部キーの WITH NOCHECK 句の値の相違を無視するか、更新するかを指定します。|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|単一の公開操作の一部としてすべての複合要素を含めます。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|データベースに公開するとき、可能であればトランザクション ステートメントを使用するかどうかを指定します。|
|**/p:**|LongRunningCommandTimeout=(INT32)|SQL Server に対してクエリを実行するときの実行時間の長いコマンドのタイムアウトを秒単位で指定します。 無期限に待機するには、0 を使用します。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|公開で、相違がある場合に ALTER ASSEMBLY ステートメントを発行するのではなく、常にアセンブリを削除して再作成することを指定します。|
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|ターゲット データベースで新しい FileGroup が作成されたときに新しいファイルも作成するかどうかを指定します。|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|スキーマがデータベース サーバーに登録されるかどうかを指定します。|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|他の操作が実行されるときに DeploymentPlanExecutor コントリビューターを実行する必要があるかどうかを指定します。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|データベースに公開するとき、データベース照合順序の相違を無視するか、更新するかを指定します。|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|データベースに公開するとき、データベース互換性の相違を無視するか、更新するかを指定します。|
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|ターゲット データベースのプロパティを公開操作の一部として設定するか、更新するかを指定します。|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|データベース名とサーバー名がデータベース プロジェクトで指定された名前と一致していることを確認するステートメントを公開スクリプトで生成するかどうかを指定します。|
|**/p:**|ScriptFileSize=(BOOLEAN)|ファイル グループにファイルを追加するときに、サイズを指定するかどうかを制御します。|
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|公開の最後にすべての制約が 1 つのセットとして検証されるため、公開の途中でチェックまたは外部キー制約によってデータ エラーが発生することを回避できます。 False に設定すると、対応するデータを確認せずに制約が公開されます。|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|公開スクリプトの末尾に更新ステートメントを追加します。|
|**/p:**|Storage=({File&#124;Memory})|データベース モデルの構築時に要素をどのように格納するかを指定します。 パフォーマンス上の理由から、既定値は InMemory です。 大規模なデータベースの場合は、File バックアップ ストレージが必要です。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|公開の検証中に発生したエラーを警告として扱うかどうかを指定します。 配置計画をターゲット データベースに対して実行する前に、生成された配置計画がチェックされます。 計画の検証では、変更を加えるためには取り除く必要のある、ターゲットのみのオブジェクト (インデックスなど) の損失などの問題が検出されます。 また、複合プロジェクトへの参照のためテーブルやビューなどに依存関係が存在するのに、その関係がターゲット データベースに存在しない状況も検出されます。 すべての問題の完全な一覧を取得するには、最初のエラー発生時に公開アクションを停止するのではなく、この方法を使用することをお勧めします。
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|修正できない相違がオブジェクトで見つかった場合 (たとえば、同じファイルのファイル サイズまたはファイル パスが異なる場合) に警告を生成するかどうかを指定します。|
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|照合順序の互換性を検証するかどうかを指定します。|
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|公開前にチェックを実行して、正常な公開をブロックする可能性のある問題が存在する場合は公開操作を停止するかどうかを指定します。 たとえば、ターゲット データベースの外部キーがデータベース プロジェクトに存在せず、公開時にエラーが発生する場合は、公開操作が停止することがあります。|
|

### <a name="sqlcmd-variables"></a>SQLCMD 変数

公開操作の実行時に使用された SQL コマンド (**sqlcmd**) 変数の値をオーバーライドするために使用できるオプションの形式を次の表で説明します。 コマンド ラインで指定された変数の値は、(たとえば、公開プロファイル内で) その変数に割り当てられている他の値をオーバーライドします。  
  
|パラメーター|Default|説明|  
|-------------|-----------|---------------|  
|**/Variables:{PropertyName}={Value}**||操作固有の変数の名前と値のペア ({VariableName}={Value}) を指定します。 DACPAC ファイルには、有効な SQLCMD 変数の一覧が含まれます。 すべての変数に値を指定しないと、エラーが発生します。|  
  
## <a name="export-parameters-and-properties"></a>エクスポート パラメーターとスクリプト プロパティ

SqlPackage.exe の Export 操作を実行すると、SQL Server または Azure SQL Database のライブ データベースが BACPAC パッケージ (.bacpac ファイル) にエクスポートされます。 既定では、すべてのテーブルのデータが .bacpac ファイルに含まれます。 必要に応じて、データをエクスポートする対象のテーブルの一部のみを指定できます。 Export 操作の検証によって、エクスポート対象にテーブルの一部を指定した場合でも、完全な対象データベースに対する Azure SQL Database の互換性が維持されます。  
  
### <a name="help-for-export-action"></a>エクスポート アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|エクスポート|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe が既存のファイルを上書きするかどうかを指定します。 False を指定すると、既存のファイルが検出された場合に sqlpackage.exe の操作が中止します。 既定値は True です。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|操作固有のプロパティの名前と値のペア ({PropertyName}={Value}) を指定します。 操作のプロパティ名については、特定の操作のヘルプを参照してください。 例: sqlpackage.exe /Action:Export /?。|
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。|
|**/SourceConnectionString:**|**/scs**|{string}|ソース データベースの有効な SQL Server または SQL Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのソース パラメーターとも同時には使用できません。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|ソース データベースの名前を定義します。 |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|ソース データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用するパスワードを定義します。 |
|**/SourceServerName:**|**/ssn**|{string}|ソース データベースをホストしているサーバーの名前を定義します。 |
|**/SourceTimeout:**|**/st**|{int}|ソース データベースへの接続を確立する際のタイムアウトを秒単位で指定します。 |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|TLS を使用してソース データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/SourceUser:**|**/su**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TargetFile:**|**/tf**|{string}| データベースではなく、ターゲット ファイル (.dacpac ファイル) をアクションのターゲットとして使用するように指定します。 このパラメーターを使用した場合、他のターゲット パラメーターは無効になります。 このパラメーターは、データベース ターゲットのみをサポートするアクションに対しては無効です。|
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|

### <a name="properties-specific-to-the-export-action"></a>エクスポート アクションに固有のプロパティ

|プロパティ|値|説明|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server に対してクエリを実行するときのコマンドのタイムアウト (秒) を指定します。|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer に対してクエリを実行するときのデータベース ロックのタイムアウトを秒単位で指定します。 無期限に待機するには、-1 を使用します。|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server に対してクエリを実行するときの実行時間の長いコマンドのタイムアウトを秒単位で指定します。 無期限に待機するには、0 を使用します。|
|**/p:**|Storage=({File&#124;Memory} 'File')|抽出時に使用されるスキーマ モデルのバックアップ用ストレージの種類を指定します。|
|**/p:**|TableData=(STRING)|データの抽出元テーブルを示します。 テーブル名は次の形式で指定してください: schema_name.table_identifier。名前部分はかっこで囲んでも囲まなくても構いません。 このオプションは、複数回指定できます。|
|**/p:**|TempDirectoryForTableData=(STRING)|パッケージ ファイルに書き込む前にテーブル データをバッファーするために使用する、一時ディレクトリを指定します。|
|**/p:**|TargetEngineVersion=({Default&#124;Latest&#124;V11&#124;V12} 'Latest')|予期されるターゲット エンジンのバージョンを指定します。 これにより、生成された bacpac で、メモリ最適化テーブルなどの V12 機能を持つ Azure SQL Database サーバーによってサポートされるオブジェクトを許可するかどうかが決まります。|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|Microsoft Azure SQL Database v12 のサポートされているフルテキスト ドキュメントの種類を確認するかどうかを指定します。|
  
## <a name="import-parameters-and-properties"></a>インポート パラメーターとプロパティ

SqlPackage.exe の Import 操作を実行すると、BACPAC パッケージ (.bacpac ファイル) のスキーマとテーブル データが、SQL Server または Azure SQL Database の新規または空のデータベースにインポートされます。 既存のデータベースへのインポート操作時に、ターゲット データベースにユーザー定義のスキーマ オブジェクトを含めることはできません。  
  
### <a name="help-for-command-actions"></a>コマンド アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|[インポート]|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|操作固有のプロパティの名前と値のペア ({PropertyName}={Value}) を指定します。 操作のプロパティ名については、特定の操作のヘルプを参照してください。 例: sqlpackage.exe /Action:Import /?。|
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。|
|**/SourceFile:**|**/sf**|{string}|ソース ファイルを操作のソースとして使用するように指定します。 このパラメーターを使用した場合、他のソース パラメーターは無効になります。 |
|**/TargetConnectionString:**|**/tcs**|{string}|ターゲット データベースの有効な SQL Server または Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのターゲット パラメーターとも同時には使用できません。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe の動作のターゲットとなるデータベースの名前のオーバーライドを指定します。 |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|ターゲット データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/TargetPassword:**|**/tp**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用するパスワードを定義します。 |
|**/TargetServerName:**|**/tsn**|{string}|ターゲット データベースをホストしているサーバーの名前を定義します。 |
|**/TargetTimeout:**|**/tt**|{int}|ターゲット データベースへの接続を確立するためのタイムアウトを秒単位で指定します。 Azure AD の場合、この値は 30 秒以上にすることをお勧めします。|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|TLS を使用してターゲット データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/TargetUser:**|**/tu**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|

インポート アクションに固有のプロパティ:

|プロパティ|値|説明|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server に対してクエリを実行するときのコマンドのタイムアウト (秒) を指定します。|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database のエディションを定義します。|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer に対してクエリを実行するときのデータベース ロックのタイムアウトを秒単位で指定します。 無期限に待機するには、-1 を使用します。|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database の最大サイズを GB 単位で定義します。|
|**/p:**|DatabaseServiceObjective=(STRING)|Azure SQL Database のパフォーマンス レベル ("P0" や "S1" など) を定義します。|
|**/p:**|ImportContributorArguments=(STRING)|配置コントリビューターに配置コントリビューター引数を指定します。 複数の値を指定する場合は、セミコロンで区切ります。|
|**/p:**|ImportContributors=(STRING)|bacpac をインポートするときに実行する配置コントリビューターを指定します。 このとき、セミコロン区切りで、完全修飾ビルド コントリビューター名または ID を指定する必要があります。|
|**/p:**|ImportContributorPaths=(STRING)|追加の配置コントリビューターを読み込むためのパスを指定します。 複数の値を指定する場合は、セミコロンで区切ります。 |
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server に対してクエリを実行するときの実行時間の長いコマンドのタイムアウトを秒単位で指定します。 無期限に待機するには、0 を使用します。|
|**/p:**|Storage=({File&#124;Memory})|データベース モデルの構築時に要素をどのように格納するかを指定します。 パフォーマンス上の理由から、既定値は InMemory です。 大規模なデータベースの場合は、File バックアップ ストレージが必要です。|
  
## <a name="deployreport-parameters-and-properties"></a>DeployReport のパラメーターおよびプロパティ

**SqlPackage.exe** レポート操作では、公開操作によって行われる変更の XML レポートを作成します。  
  
### <a name="help-for-deployreport-action"></a>DeployReport アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|DeployReport|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/OutputPath:**|**/op**|{string}|出力ファイルが生成されるファイル パスを指定します。 |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe が既存のファイルを上書きするかどうかを指定します。 False を指定すると、既存のファイルが検出された場合に sqlpackage.exe の操作が中止します。 既定値は True です。 |
|**/Profile:**|**/pr**|{string}|DAC 公開プロファイルのファイル パスを指定します。 出力の生成時に使用するプロパティと変数のコレクションをプロファイルで定義します。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|操作固有のプロパティの名前と値のペア ({PropertyName}={Value}) を指定します。 操作のプロパティ名については、特定の操作のヘルプを参照してください。 例: sqlpackage.exe /Action:DeployReport /?。 |
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。 |
|**/SourceConnectionString:**|**/scs**|{string}|ソース データベースの有効な SQL Server または SQL Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのソース パラメーターとも同時には使用できません。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|ソース データベースの名前を定義します。 |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|ソース データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/SourceFile:**|**/sf**|{string}|データベースではなく、ソース ファイルを操作のソースとして使用するように指定します。 このパラメーターを使用した場合、他のソース パラメーターは無効になります。 |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用するパスワードを定義します。 |
|**/SourceServerName:**|**/ssn**|{string}|ソース データベースをホストしているサーバーの名前を定義します。 |
|**/SourceTimeout:**|**/st**|{int}|ソース データベースへの接続を確立する際のタイムアウトを秒単位で指定します。 |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|TLS を使用してソース データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/SourceUser:**|**/su**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TargetConnectionString:**|**/tcs**|{string}|ターゲット データベースの有効な SQL Server または Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのターゲット パラメーターとも同時には使用できません。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe の動作のターゲットとなるデータベースの名前のオーバーライドを指定します。 |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|ターゲット データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/TargetFile:**|**/tf**|{string}|データベースではなく、ターゲット ファイル (.dacpac ファイル) をアクションのターゲットとして使用するように指定します。 このパラメーターを使用した場合、他のターゲット パラメーターは無効になります。 このパラメーターは、データベース ターゲットのみをサポートするアクションに対しては無効です。|
|**/TargetPassword:**|**/tp**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用するパスワードを定義します。 |
|**/TargetServerName:**|**/tsn**|{string}|ターゲット データベースをホストしているサーバーの名前を定義します。 |
|**/TargetTimeout:**|**/tt**|{int}|ターゲット データベースへの接続を確立するためのタイムアウトを秒単位で指定します。 Azure AD の場合、この値は 30 秒以上にすることをお勧めします。|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|TLS を使用してターゲット データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/TargetUser:**|**/tu**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/Variables:**|**/v**|{PropertyName}={Value}|操作固有の変数の名前と値のペア ({VariableName}={Value}) を指定します。 DACPAC ファイルには、有効な SQLCMD 変数の一覧が含まれます。 すべての変数に値を指定しないと、エラーが発生します。 |

## <a name="properties-specific-to-the-deployreport-action"></a>DeployReport アクションに固有のプロパティ

|プロパティ|値|説明|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|配置コントリビューターに追加の配置コントリビューター引数を指定します。 複数の値を指定する場合は、セミコロンで区切ります。|
|**/p:**|AdditionalDeploymentContributors=(STRING)|dacpac を配置するときに実行する必要がある、追加の配置コントリビューターを指定します。 このとき、セミコロン区切りで、完全修飾ビルド コントリビューター名または ID を指定する必要があります。|
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| 追加の配置コントリビューターを読み込むためのパスを指定します。 複数の値を指定する場合は、セミコロンで区切ります。 | 
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|このプロパティは、ブロックしているアセンブリを配置計画から削除する際に SqlClr の配置によって使用されます。 既定では、参照しているアセンブリを削除する必要がある場合、ブロックまたは参照しているアセンブリによって、アセンブリの更新がブロックされます。|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|互換性がない SQL Server プラットフォームであっても操作を試行するかどうかを指定します。|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|このプロパティが true に設定されている場合は、行レベル セキュリティを使用するテーブルに対するデータ モーションをブロックしません。 既定値は false です。|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|変更を配置する前にデータベースをバックアップします。|
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|公開操作によるデータ損失の可能性がある場合に、公開を終了するかどうかを指定します。|
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|スキーマがその登録と一致しないか、スキーマが登録されていないデータベースの更新をブロックするかどうかを指定します。 |
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server に対してクエリを実行するときのコマンドのタイムアウト (秒) を指定します。 |
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|生成する公開スクリプトで SETVAR 変数の宣言をコメント アウトするかどうかを指定します。 このようなコメント アウトが必要になるのは、SQLCMD.EXE などのツールを使用して、公開時にコマンド ラインで値を指定する予定がある場合などです。 |
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|この設定では、配置の際にデータベースの照合順序をどのように処理するかを指定します。既定では、ソースで指定されている照合順序と異なる場合にターゲット データベースの照合順序が更新されます。 このオプションを設定した場合、ターゲット データベース (またはサーバー) の照合順序が使用されます。 |
|**/p:**|CreateNewDatabase=(BOOLEAN)|データベースへの公開時に、ターゲット データベースを更新するか、削除して再作成するかを指定します。 |
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database のエディションを定義します。|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer に対してクエリを実行するときのデータベース ロックのタイムアウトを秒単位で指定します。 無期限に待機するには、-1 を使用します。|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database の最大サイズを GB 単位で定義します。|
|**/p:**|DatabaseServiceObjective=(STRING)|Azure SQL Database のパフォーマンス レベル ("P0" や "S1" など) を定義します。 |
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|true の場合、データベースは配置前にシングル ユーザー モードに設定されます。 |
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| 公開プロセスの開始時にデータ定義言語 (DDL) トリガーを無効にして、公開操作の最後に再度有効にするかどうかを指定します。|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|true の場合、Change Data Capture オブジェクトは変更されません。|
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|レプリケートされたオブジェクトが、検証時に識別されるかどうかを指定します。|
|**/p:**|DoNotDropObjectType=(STRING)|DropObjectsNotInSource が true の場合、削除されないオブジェクトの種類。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。 |
|**/p:**|DoNotDropObjectTypes=(STRING)|DropObjectsNotInSource が true の場合に削除されない、オブジェクトの種類のセミコロン区切りリスト。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しない制約を削除するかどうかを指定します。|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しない DML トリガーを削除するかどうかを指定します。|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない拡張プロパティをターゲット データベースから削除するかどうかを指定します。|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しないインデックスを削除するかどうかを指定します。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|データベースへの公開時に、データベース スナップショット (.dacpac) ファイルに存在しないオブジェクトをターゲット データベースから削除するかどうかを指定します。 この値は DropExtendedProperties よりも優先されます。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|データベースへの更新の公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しないアクセス許可を削除するかどうかを指定します。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|データベースへの更新の公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルで定義されていないロール メンバーを削除するかどうかを指定します。|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない統計をターゲット データベースから削除するかどうかを指定します。|
|**/p:**|ExcludeObjectType=(STRING)|配置時に無視するオブジェクトの種類。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|ExcludeObjectTypes=(STRING)|配置時に無視するオブジェクトの種類のセミコロン区切りリスト。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|null 値が許可されない列を含むデータが格納されているテーブルを更新する際に、自動的に既定値が設定されます。|
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|データベースに公開するとき、ANSI NULLS 設定の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|データベースに公開するとき、Authorizer の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|データベースに公開するとき、列の照合順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|データベースに公開するときに、テーブル列の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreComments=(BOOLEAN)|データベースに公開するとき、コメントの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|データベースに公開するとき、暗号化プロバイダーのファイル パスの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|データベースまたはサーバーに公開するとき、Data Definition Language (DDL) triggers の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|データベースに公開するとき、Data Definition Language (DDL) triggers の有効または無効にされた状態の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|データベースに公開するとき、既定のスキーマの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|データベースに公開するとき、Data Manipulation Language (DML) triggers の順序の相違を無視するか、更新するかを指定します。| 
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|データベースに公開するとき、DML triggers の有効または無効にされた状態の相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|データベースに公開するとき、拡張プロパティの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|データベースに公開するとき、ファイルおよびログ ファイルのパスの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|データベースに公開するとき、FILEGROUP 内のオブジェクトの位置の相違を無視するか、更新するかを指定します。| 
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|データベースに公開するとき、ファイル サイズの相違を無視するか、または警告を発するかを指定します。 |
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|データベースに公開するとき、インデックス格納の FILL FACTOR の相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|データベースに公開するとき、フルテキスト カタログのファイル パスの相違を無視するか、または警告を発するかを指定します。| 
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|データベースに公開するとき、Identity 列のシードの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreIncrement=(BOOLEAN)|データベースに公開するとき、Identity 列のインクリメントの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|データベースに公開するとき、インデックス オプションの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|データベースに公開するとき、インデックス パディングの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|データベースに公開するとき、キーワードの大文字と小文字の相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|データベースに公開するとき、インデックスのロック ヒントの相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')| データベースに公開するとき、セキュリティ ID 番号 (SID) の相違を無視するか、更新するかを指定します。| 
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|データベースに公開するとき、レプリケーションでは使わない設定を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|データベースに公開するとき、パーティション構成でのオブジェクトの位置を無視するか、更新するかを指定します。|
 |**/p:**|IgnorePartitionSchemes=(BOOLEAN)|データベースに公開するとき、パーティション構成と関数の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnorePermissions=(BOOLEAN)|データベースに公開するとき、権限の相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|データベースに公開するとき、引用符で囲まれた識別子の相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|データベースへの公開時に、ログインのロール メンバーシップの相違を無視するか更新するかを指定します。 |
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|データベースに公開するとき、SQL Server がルーティング テーブルにルートを保持する時間の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|データベースに公開するとき、T-SQL ステートメント間のセミコロンの相違を無視するか、更新するかを指定します。| 
|**/p:**|IgnoreTableOptions=(BOOLEAN)|データベースに公開するとき、テーブル オプションの相違を無視するか、更新するかを指定します。| 
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|データベースに公開するとき、テーブル パーティション オプションの相違を無視するか、更新するかを指定します。  このオプションは、Azure Synapse Analytics データ ウェアハウス データベースにのみ適用されます。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|データベースに公開するとき、ユーザー設定オブジェクトの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|データベースに公開するとき、空白の相違を無視するか、更新するかを指定します。 |
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|データベースに公開するとき、CHECK 制約の WITH NOCHECK 句の値の相違を無視するか、更新するかを指定します。| 
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|データベースに公開するとき、外部キーの WITH NOCHECK 句の値の相違を無視するか、更新するかを指定します。| 
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|単一の公開操作の一部としてすべての複合要素を含めます。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|データベースに公開するとき、可能であればトランザクション ステートメントを使用するかどうかを指定します。|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server に対してクエリを実行するときの実行時間の長いコマンドのタイムアウトを秒単位で指定します。 無期限に待機するには、0 を使用します。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|公開で、相違がある場合に ALTER ASSEMBLY ステートメントを発行するのではなく、常にアセンブリを削除して再作成することを指定します。 |
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|ターゲット データベースで新しい FileGroup が作成されたときに新しいファイルも作成するかどうかを指定します。 |
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|スキーマがデータベース サーバーに登録されるかどうかを指定します。 
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|他の操作が実行されるときに DeploymentPlanExecutor コントリビューターを実行する必要があるかどうかを指定します。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|データベースに公開するとき、データベース照合順序の相違を無視するか、更新するかを指定します。 |
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|データベースに公開するとき、データベース互換性の相違を無視するか、更新するかを指定します。 |
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|ターゲット データベースのプロパティを公開操作の一部として設定するか、更新するかを指定します。 |
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|データベース名とサーバー名がデータベース プロジェクトで指定された名前と一致していることを確認するステートメントを公開スクリプトで生成するかどうかを指定します。|
|**/p:**|ScriptFileSize=(BOOLEAN)|ファイル グループにファイルを追加するときに、サイズを指定するかどうかを制御します。 |
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|公開の最後にすべての制約が 1 つのセットとして検証されるため、公開の途中でチェックまたは外部キー制約によってデータ エラーが発生することを回避できます。 False に設定すると、対応するデータを確認せずに制約が公開されます。|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|公開スクリプトの末尾に更新ステートメントを追加します。|
|**/p:**|Storage=({File&#124;Memory})|データベース モデルの構築時に要素をどのように格納するかを指定します。 パフォーマンス上の理由から、既定値は InMemory です。 大規模なデータベースの場合は、File バックアップ ストレージが必要です。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|公開の検証中に発生したエラーを警告として扱うかどうかを指定します。 配置計画をターゲット データベースに対して実行する前に、生成された配置計画がチェックされます。 計画の検証では、変更を加えるためには取り除く必要のある、ターゲットのみのオブジェクト (インデックスなど) の損失などの問題が検出されます。 また、複合プロジェクトへの参照のためテーブルやビューなどに依存関係が存在するのに、その関係がターゲット データベースに存在しない状況も検出されます。 すべての問題の完全な一覧を取得するには、最初のエラー発生時に公開アクションを停止するのではなく、この方法を使用することをお勧めします。 |
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|修正できない相違がオブジェクトで見つかった場合 (たとえば、同じファイルのファイル サイズまたはファイル パスが異なる場合) に警告を生成するかどうかを指定します。| 
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|照合順序の互換性を検証するかどうかを指定します。| 
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|公開前にチェックを実行して、正常な公開をブロックする可能性のある問題が存在する場合は公開操作を停止するかどうかを指定します。 たとえば、ターゲット データベースの外部キーがデータベース プロジェクトに存在せず、公開時にエラーが発生する場合は、公開操作が停止することがあります。 |
  
## <a name="driftreport-parameters"></a>DriftReport のパラメーター

**SqlPackage.exe** レポート操作では、前回データベースが登録されてから以降に、登録されたデータベースに対して行われた変更の XML レポートが作成されます。  
  
### <a name="help-for-driftreport-action"></a>DriftReport アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|DriftReport|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/OutputPath:**|**/op**|{string}|出力ファイルが生成されるファイル パスを指定します。 |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe が既存のファイルを上書きするかどうかを指定します。 False を指定すると、既存のファイルが検出された場合に sqlpackage.exe の操作が中止します。 既定値は True です。 |
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。|
|**/TargetConnectionString:**|**/tcs**|{string}|ターゲット データベースの有効な SQL Server または Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのターゲット パラメーターとも同時には使用できません。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe の動作のターゲットとなるデータベースの名前のオーバーライドを指定します。 |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|ターゲット データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/TargetPassword:**|**/tp**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用するパスワードを定義します。 |
|**/TargetServerName:**|**/tsn**|{string}|ターゲット データベースをホストしているサーバーの名前を定義します。 |
|**/TargetTimeout:**|**/tt**|{int}|ターゲット データベースへの接続を確立するためのタイムアウトを秒単位で指定します。 Azure AD の場合、この値は 30 秒以上にすることをお勧めします。|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|TLS を使用してターゲット データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/TargetUser:**|**/tu**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|

## <a name="script-parameters-and-properties"></a>スクリプト パラメーターとスクリプト プロパティ

**SqlPackage.exe** のスクリプト操作では、ソース データベースのスキーマに合わせてターゲット データベースのスキーマを更新する、Transact-SQL の増分更新スクリプトを作成します。  
  
### <a name="help-for-the-script-action"></a>スクリプト アクションのヘルプ

|パラメーター|短い形式|値|説明|
|---|---|---|---|
|**/Action:**|**/a**|スクリプト|実行する操作を指定します。 |
|**/AccessToken:**|**/at**|{string}| ターゲット データベースに接続するときに使用するトークン ベースの認証アクセス トークンを指定します。 |
|**/DeployScriptPath:**|**/dsp**|{string}|配置スクリプトを出力する省略可能なファイル パスを指定します。 Azure の配置では、master データベースを作成または変更するための TSQL コマンドがある場合、スクリプトは同じパスに書き込まれますが、出力ファイル名として "Filename_Master.sql" が使用されます。 |
|**/DeployReportPath:**|**/drp**|{string}|配置レポートの xml ファイルを出力する省略可能なファイル パスを指定します。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|診断ログがコンソールへの出力かどうかを指定します。 既定値は False です。 |
|**/DiagnosticsFile:**|**/df**|{string}|診断ログを保存するファイルを指定します。 |
|**/MaxParallelism:**|**/mp**|{int}| 1 つのデータベースに対して実行される同時実行操作の並列処理の次数を指定します。 既定値は 8 です。 |
|**/OutputPath:**|**/op**|{string}|出力ファイルが生成されるファイル パスを指定します。 |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe が既存のファイルを上書きするかどうかを指定します。 False を指定すると、既存のファイルが検出された場合に sqlpackage.exe の操作が中止します。 既定値は True です。 |
|**/Profile:**|**/pr**|{string}|DAC 公開プロファイルのファイル パスを指定します。 出力の生成時に使用するプロパティと変数のコレクションをプロファイルで定義します。|
|**/Properties:**|**/p**|{PropertyName}={Value}|操作固有のプロパティの名前と値のペア ({PropertyName}={Value}) を指定します。 操作のプロパティ名については、特定の操作のヘルプを参照してください。 例: sqlpackage.exe /Action:Script /?。|
|**/Quiet:**|**/q**|{True&#124;False}|詳細なフィードバックを非表示にするかどうかを指定します。 既定値は False です。|
|**/SourceConnectionString:**|**/scs**|{string}|ソース データベースの有効な SQL Server または SQL Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのソース パラメーターとも同時には使用できません。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|ソース データベースの名前を定義します。 |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|ソース データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/SourceFile:**|**/sf**|{string}|ソース ファイルを操作のソースとして使用するように指定します。 このパラメーターを使用した場合、他のソース パラメーターは無効になります。 |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用するパスワードを定義します。 |
|**/SourceServerName:**|**/ssn**|{string}|ソース データベースをホストしているサーバーの名前を定義します。 |
|**/SourceTimeout:**|**/st**|{int}|ソース データベースへの接続を確立する際のタイムアウトを秒単位で指定します。 |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|TLS を使用してソース データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/SourceUser:**|**/su**|{string}|SQL Server 認証シナリオでは、ソース データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TargetConnectionString:**|**/tcs**|{string}|ターゲット データベースの有効な SQL Server または Azure 接続文字列を指定します。 このパラメーターを指定する場合、他のどのターゲット パラメーターとも同時には使用できません。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe の動作のターゲットとなるデータベースの名前のオーバーライドを指定します。 |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|ターゲット データベース接続に SQL 暗号化を使用するかどうかを指定します。 |
|**/TargetFile:**|**/tf**|{string}| データベースではなく、ターゲット ファイル (.dacpac ファイル) をアクションのターゲットとして使用するように指定します。 このパラメーターを使用した場合、他のターゲット パラメーターは無効になります。 このパラメーターは、データベース ターゲットのみをサポートするアクションに対しては無効です。|
|**/TargetPassword:**|**/tp**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用するパスワードを定義します。 |
|**/TargetServerName:**|**/tsn**|{string}|ターゲット データベースをホストしているサーバーの名前を定義します。 |
|**/TargetTimeout:**|**/tt**|{int}|ターゲット データベースへの接続を確立するためのタイムアウトを秒単位で指定します。 Azure AD の場合、この値は 30 秒以上にすることをお勧めします。|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|TLS を使用してターゲット データベースへの接続を暗号化し、証明書チェーンを検証せずに信頼を確認するかどうかを指定します。 |
|**/TargetUser:**|**/tu**|{string}|SQL Server 認証シナリオでは、ターゲット データベースへのアクセスに使用する SQL Server ユーザーを定義します。 |
|**/TenantId:**|**/tid**|{string}|Azure AD のテナント ID またはドメイン名を表します。 このオプションは、ゲスト、またはインポートされた Azure AD ユーザーと Microsoft アカウント (outlook.com、hotmail.com、live.com など) をサポートする必要があります。 このパラメーターを省略すると、Azure AD の既定のテナント ID が、認証済みユーザーがこの AD のネイティブ ユーザーであることを前提として使用されます。 ただし、この場合、ゲスト、またはこの Azure AD でホストされているインポートされたユーザーと Microsoft アカウントはサポートされず、操作は失敗します。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|ユニバーサル認証を使用するかどうかを指定します。 True に設定すると、対話型認証プロトコルがアクティブになり、MFA がサポートされます。 このオプションは、ユーザーによるユーザー名とパスワードの入力を必要とする対話型プロトコルまたは統合認証 (Windows 資格情報) を使用した、MFA なしの Azure AD 認証に使用することもできます。 /UniversalAuthentication が True に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定することはできません。 /UniversalAuthentication が False に設定されているときは、SourceConnectionString (scs) で Azure AD 認証を指定する必要があります。 <br/> Active Directory ユニバーサル認証の詳細については、[SQL Database と Azure Synapse Analytics を使用したユニバーサル認証 (SSMS での MFA のサポート)](/azure/sql-database/sql-database-ssms-mfa-authentication) に関するページをご覧ください。|
|**/Variables:**|**/v**|{PropertyName}={Value}|操作固有の変数の名前と値のペア ({VariableName}={Value}) を指定します。 DACPAC ファイルには、有効な SQLCMD 変数の一覧が含まれます。 すべての変数に値を指定しないと、エラーが発生します。 |

### <a name="properties-specific-to-the-script-action"></a>スクリプト アクションに固有のプロパティ

|プロパティ|値|説明|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|配置コントリビューターに追加の配置コントリビューター引数を指定します。 複数の値を指定する場合は、セミコロンで区切ります。
|**/p:**|AdditionalDeploymentContributors=(STRING)|dacpac を配置するときに実行する必要がある、追加の配置コントリビューターを指定します。 このとき、セミコロン区切りで、完全修飾ビルド コントリビューター名または ID を指定する必要があります。
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| 追加の配置コントリビューターを読み込むためのパスを指定します。 複数の値を指定する場合は、セミコロンで区切ります。 | 
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|このプロパティは、ブロックしているアセンブリを配置計画から削除する際に SqlClr の配置によって使用されます。 既定では、参照しているアセンブリを削除する必要がある場合、ブロックまたは参照しているアセンブリによって、アセンブリの更新がブロックされます。
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|互換性がない SQL Server プラットフォームであっても操作を試行するかどうかを指定します。
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|このプロパティが true に設定されている場合は、行レベル セキュリティを使用するテーブルに対するデータ モーションをブロックしません。 既定値は false です。
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|変更を配置する前にデータベースをバックアップします。
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|公開操作によるデータ損失の可能性がある場合に、公開を終了するかどうかを指定します。
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|スキーマがその登録と一致しないか、スキーマが登録されていないデータベースの更新をブロックするかどうかを指定します。
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server に対してクエリを実行するときのコマンドのタイムアウト (秒) を指定します。
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|生成する公開スクリプトで SETVAR 変数の宣言をコメント アウトするかどうかを指定します。 このようなコメント アウトが必要になるのは、SQLCMD.EXE などのツールを使用して、公開時にコマンド ラインで値を指定する予定がある場合などです。
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|この設定では、配置の際にデータベースの照合順序をどのように処理するかを指定します。既定では、ソースで指定されている照合順序と異なる場合にターゲット データベースの照合順序が更新されます。 このオプションを設定した場合、ターゲット データベース (またはサーバー) の照合順序が使用されます。|
|**/p:**|CreateNewDatabase=(BOOLEAN)|データベースへの公開時に、ターゲット データベースを更新するか、削除して再作成するかを指定します。
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database のエディションを定義します。|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer に対してクエリを実行するときのデータベース ロックのタイムアウトを秒単位で指定します。 無期限に待機するには、-1 を使用します。|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database の最大サイズを GB 単位で定義します。
|**/p:**|DatabaseServiceObjective=(STRING)|Azure SQL Database のパフォーマンス レベル ("P0" や "S1" など) を定義します。
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|true の場合、データベースは配置前にシングル ユーザー モードに設定されます。
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| 公開プロセスの開始時にデータ定義言語 (DDL) トリガーを無効にして、公開操作の最後に再度有効にするかどうかを指定します。|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|true の場合、Change Data Capture オブジェクトは変更されません。
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|レプリケートされたオブジェクトが、検証時に識別されるかどうかを指定します。
|**/p:**|DoNotDropObjectType=(STRING)|DropObjectsNotInSource が true の場合、削除されないオブジェクトの種類。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。
|**/p:**|DoNotDropObjectTypes=(STRING)|DropObjectsNotInSource が true の場合に削除されない、オブジェクトの種類のセミコロン区切りリスト。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない制約をターゲット データベースから削除するかどうかを指定します。|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない DML triggers が、ターゲット データベースから削除されるかどうかを指定します。|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない拡張プロパティをターゲット データベースから削除するかどうかを指定します。|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しないインデックスをターゲット データベースから削除するかどうかを指定します。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しないオブジェクトをターゲット データベースから削除するかどうかを指定します。 この値は DropExtendedProperties よりも優先されます。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|データベースへの更新の公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルに存在しないアクセス許可を削除するかどうかを指定します。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|データベースへの更新の公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) ファイルで定義されていないロール メンバーを削除するかどうかを指定します。|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|データベースに公開するとき、データベース スナップショット (.dacpac) ファイルに存在しない統計をターゲット データベースから削除するかどうかを指定します。|
|**/p:**|ExcludeObjectType=(STRING)|配置時に無視するオブジェクトの種類。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。
|**/p:**|ExcludeObjectTypes=(STRING)|配置時に無視するオブジェクトの種類のセミコロン区切りリスト。 有効なオブジェクトの種類名は、Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers です。
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|null 値が許可されない列を含むデータが格納されているテーブルを更新する際に、自動的に既定値が設定されます。
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|データベースに公開するとき、ANSI NULLS 設定の相違を無視するか、更新するかを指定します。
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|データベースに公開するとき、Authorizer の相違を無視するか、更新するかを指定します。
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|データベースに公開するとき、列の照合順序の相違を無視するか、更新するかを指定します。
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|データベースに公開するときに、テーブル列の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreComments=(BOOLEAN)|データベースに公開するとき、コメントの相違を無視するか、更新するかを指定します。
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|データベースに公開するとき、暗号化プロバイダーのファイル パスの相違を無視するか、更新するかを指定します。
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|データベースまたはサーバーに公開するとき、Data Definition Language (DDL) triggers の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|データベースに公開するとき、Data Definition Language (DDL) triggers の有効または無効にされた状態の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|データベースに公開するとき、既定のスキーマの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|データベースに公開するとき、Data Manipulation Language (DML) triggers の順序の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|データベースに公開するとき、DML triggers の有効または無効にされた状態の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|データベースに公開するとき、拡張プロパティの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|データベースに公開するとき、ファイルおよびログ ファイルのパスの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|データベースに公開するとき、FILEGROUP 内のオブジェクトの位置の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|データベースに公開するとき、ファイル サイズの相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|公開時に、インデックス格納の FILL FACTOR の相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|データベースに公開するとき、フルテキスト カタログのファイル パスの相違を無視するか、または警告を発するかを指定します。|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|データベースに公開するとき、Identity 列のシードの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreIncrement=(BOOLEAN)|データベースに公開するとき、Identity 列のインクリメントの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|データベースに公開するとき、インデックス オプションの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|データベースに公開するとき、インデックス パディングの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|データベースに公開するとき、キーワードの大文字と小文字の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|データベースに公開するとき、インデックスのロック ヒントの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')| データベースに公開するとき、セキュリティ ID 番号 (SID) の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|データベースに公開するとき、レプリケーションでは使わない設定を無視するか、更新するかを指定します。|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|データベースに公開するとき、パーティション構成でのオブジェクトの位置を無視するか、更新するかを指定します。|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|データベースに公開するとき、パーティション構成と関数の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnorePermissions=(BOOLEAN)|データベースに公開するとき、権限の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|データベースに公開するとき、引用符で囲まれた識別子の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|データベースへの公開時に、ログインのロール メンバーシップの相違を無視するか更新するかを指定します。|
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|データベースへの公開時に、SQL Server がルーティング テーブルにルートを保持する時間の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|データベースに公開するとき、T-SQL ステートメント間のセミコロンの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|データベースに公開するとき、テーブル オプションの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|データベースに公開するとき、テーブル パーティション オプションの相違を無視するか、更新するかを指定します。  このオプションは、Azure Synapse Analytics データ ウェアハウス データベースにのみ適用されます。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|データベースに公開するとき、ユーザー設定オブジェクトの相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|データベースに公開するとき、空白の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|公開時に、CHECK 制約の WITH NOCHECK 句の値の相違を無視するか、更新するかを指定します。|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|データベースに公開するとき、外部キーの WITH NOCHECK 句の値の相違を無視するか、更新するかを指定します。|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|単一の公開操作の一部としてすべての複合要素を含めます。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|データベースに公開するとき、可能であればトランザクション ステートメントを使用するかどうかを指定します。|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server に対してクエリを実行するときの実行時間の長いコマンドのタイムアウトを秒単位で指定します。 無期限に待機するには、0 を使用します。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|公開で、相違がある場合に ALTER ASSEMBLY ステートメントを発行するのではなく、常にアセンブリを削除して再作成することを指定します。|
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|ターゲット データベースで新しい FileGroup が作成されたときに新しいファイルも作成するかどうかを指定します。|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|スキーマがデータベース サーバーに登録されるかどうかを指定します。|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|他の操作が実行されるときに DeploymentPlanExecutor コントリビューターを実行する必要があるかどうかを指定します。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|データベースに公開するとき、データベース照合順序の相違を無視するか、更新するかを指定します。|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|データベースに公開するとき、データベース互換性の相違を無視するか、更新するかを指定します。|
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|ターゲット データベースのプロパティを公開操作の一部として設定するか、更新するかを指定します。|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|データベース名とサーバー名がデータベース プロジェクトで指定された名前と一致していることを確認するステートメントを公開スクリプトで生成するかどうかを指定します。|
|**/p:**|ScriptFileSize=(BOOLEAN)|ファイル グループにファイルを追加するときに、サイズを指定するかどうかを制御します。|
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|公開の最後にすべての制約が 1 つのセットとして検証されるため、公開の途中でチェックまたは外部キー制約によってデータ エラーが発生することを回避できます。 False に設定すると、対応するデータを確認せずに制約が公開されます。|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|公開スクリプトの末尾に更新ステートメントを追加します。|
|**/p:**|Storage=({File&#124;Memory})|データベース モデルの構築時に要素をどのように格納するかを指定します。 パフォーマンス上の理由から、既定値は InMemory です。 大規模なデータベースの場合は、File バックアップ ストレージが必要です。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|公開の検証中に発生したエラーを警告として扱うかどうかを指定します。 配置計画をターゲット データベースに対して実行する前に、生成された配置計画がチェックされます。 計画の検証では、変更を加えるためには取り除く必要のある、ターゲットのみのオブジェクト (インデックスなど) の損失などの問題が検出されます。 また、複合プロジェクトへの参照のためテーブルやビューなどに依存関係が存在するのに、その関係がターゲット データベースに存在しない状況も検出されます。 すべての問題の完全な一覧を取得するには、最初のエラー発生時に公開アクションを停止するのではなく、この方法を使用することをお勧めします。|
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|修正できない相違がオブジェクトで見つかった場合 (たとえば、同じファイルのファイル サイズまたはファイル パスが異なる場合) に警告を生成するかどうかを指定します。|
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|照合順序の互換性を検証するかどうかを指定します。
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|公開前にチェックを実行して、正常な公開をブロックする可能性のある問題が存在する場合は公開操作を停止するかどうかを指定します。 たとえば、ターゲット データベースの外部キーがデータベース プロジェクトに存在せず、公開時にエラーが発生する場合は、公開操作が停止することがあります。|

## <a name="exit-codes"></a>終了コード

次の終了コードを返すコマンド:

- 0 = 成功
- 0 以外 = 失敗
