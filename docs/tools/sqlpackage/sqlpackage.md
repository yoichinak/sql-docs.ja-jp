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
ms.openlocfilehash: ef49071f97d255d98f8086b9ff329c77d7b4afad
ms.sourcegitcommit: 5ceafd29b8f22edb800cec150f0ccddea43313e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "98983665"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

**SqlPackage.exe** は、次のデータベース開発タスクを自動化するコマンド ライン ユーティリティです。  
  
- [バージョン](#version):SqlPackage アプリケーションのビルド番号が返されます。  バージョン 18.6 で追加されました。

- [Extract](sqlpackage-extract.md): 接続されている SQL データベースから、スキーマまたはスキーマとユーザー データを含め、データ層アプリケーション (.dacpac) ファイルを作成します。  
  
- [発行](sqlpackage-publish.md):ソース .dacpac ファイルのスキーマに合わせてデータベース スキーマの増分更新を行います。 データベースがサーバーに存在しない場合は、公開操作によって作成されます。 存在する場合は、既存のデータベースが更新されます。  
  
- [Export](sqlpackage-export.md):接続されている SQL データベースを、データベース スキーマとユーザー データを含め、BACPAC ファイル (.bacpac) にエクスポートします。  
  
- [Import](sqlpackage-import.md):BACPAC ファイルから新しいユーザー データベースにスキーマとテーブル データをインポートします。  
  
- [DeployReport](sqlpackage-deploy-drift-report.md): 公開操作によって行われる変更の XML レポートを作成します。  
  
- [DriftReport](sqlpackage-deploy-drift-report.md):登録されたデータベースに対して最終登録以降に行われた変更に関する XML レポートを作成します。  
  
- [Script](sqlpackage-script.md): ソースのスキーマに合わせてターゲットのスキーマを更新する、Transact-SQL の増分更新スクリプトを作成します。  
  
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


## <a name="exit-codes"></a>終了コード

次の終了コードを返すコマンド:

- 0 = 成功
- 0 以外 = 失敗


## <a name="parameters"></a>パラメーター
SqlPackage アクション間で共有されるパラメーターもあります。 パラメーターについてまとめた表を次に示します。詳細については、特定のアクション ページをクリックしてください。

| パラメーター | 短い形式 | [抽出](sqlpackage-extract.md#parameters-for-the-extract-action) | [発行](sqlpackage-publish.md#parameters-for-the-publish-action) | [エクスポート](sqlpackage-export.md#parameters-for-the-export-action) | [[インポート]](sqlpackage-import.md#parameters-for-the-import-action) | [DeployReport](sqlpackage-deploy-drift-report.md#deployreport-action-parameters) | [DriftReport](sqlpackage-deploy-drift-report.md#driftreport-action-parameters) | [スクリプト](sqlpackage-script.md#parameters-for-the-script-action) |
|---|---|---|---|---|---|---|---|---|
|**/AccessToken:**|**/at**| x | x | x | x | x | x | x |
|**/ClientId:**|**/cid**| | x | | | | | |
|**/DeployScriptPath:**|**/dsp**| | x | | | | | x |
|**/DeployReportPath:**|**/drp**| | x | | | | | x |
|**/Diagnostics:**|**/d**| x | x | x | x | x | x | x |
|**/DiagnosticsFile:**|**/df**| x | x | x | x | x | x | x |
|**/MaxParallelism:**|**/mp**| x | x | x | x | x | x | x |
|**/OutputPath:**|**/op**|  |  |  | | x | x | x |
|**/OverwriteFiles:**|**/of**| x | x | x | | x | x | x |
|**/Profile:**|**/pr**| | x | | | x | | x |
|**/Properties:**|**/p**| x | x | x | x | x | | x |
|**/Quiet:**|**/q**| x | x | x | x | x | x | x |
|**/Secret:**|**/secr**| | x | | | | | |
|**/SourceConnectionString:**|**/scs**| x | x | x | | x | | x | x |
|**/SourceDatabaseName:**|**/sdn**| x | x | x | | x | | x |
|**/SourceEncryptConnection:**|**/sec**| x | x | x | | x | | x |
|**/SourceFile:**|**/sf**| | x | | x | x | | x |
|**/SourcePassword:**|**/sp**| x | x | x | | x | | x |
|**/SourceServerName:**|**/ssn**| x | x | x | | x | | x |
|**/SourceTimeout:**|**/st**| x | x | x | | x | | x |
|**/SourceTrustServerCertificate:**|**/stsc**| x | x | x | | x | | x |
|**/SourceUser:**|**/su**| x | x | x | | x | | x |
|**/TargetConnectionString:**|**/tcs**| | | | x | x | x | x |
|**/TargetDatabaseName:**|**/tdn**| | x | | x | x | x | x |
|**/TargetEncryptConnection:**|**/tec**| | x | | x | x | x | x |
|**/TargetFile:**|**/tf**| x | | x | | x | | x |
|**/TargetPassword:**|**/tp**| | x | | x | x | x | x |
|**/TargetServerName:**|**/tsn**| | x | | x | x | x | x |
|**/TargetTimeout:**|**/tt**| | x | | x | x | x | x |
|**/TargetTrustServerCertificate:**|**/ttsc**| | x | | x | x | x | x |
|**/TargetUser:**|**/tu**| | x | | x | x | x | x |
|**/TenantId:**|**/tid**| x | x | x | x | x | x | x |
|**/UniversalAuthentication:**|**/ua**| x | x | x | x | x | x | x |
|**/Variables:**|**/v**| | | | | x | | x |

## <a name="properties"></a>プロパティ
SqlPackage アクション間で共有されるプロパティもあります。  プロパティについてまとめた表を次に示します。詳細については、特定のアクション ページをクリックしてください。

| プロパティ | [抽出](sqlpackage-extract.md#properties-specific-to-the-extract-action) | [発行](sqlpackage-publish.md#properties-specific-to-the-publish-action) | [エクスポート](sqlpackage-export.md#properties-specific-to-the-export-action) | [[インポート]](sqlpackage-import.md#properties-specific-to-the-import-action) | [DeployReport](sqlpackage-deploy-drift-report.md#deployreport-action-properties) | [スクリプト](sqlpackage-script.md#properties-specific-to-the-script-action) |
|---|---|---|---|---|---|---|
|AdditionalDeploymentContributorArguments=(STRING)| | x | | | x | x |
|AdditionalDeploymentContributors=(STRING)| | x | | | x | x |
|AdditionalDeploymentContributorPaths=(STRING)| | x | | | x | x |
|AllowDropBlockingAssemblies=(BOOLEAN)| | x | | | x | x |
|AllowIncompatiblePlatform=(BOOLEAN)| | x | | | x | x |
|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)| | x | | | x | x |
|BackupDatabaseBeforeChanges=(BOOLEAN)| | x | | | x | x |
|BlockOnPossibleDataLoss=(BOOLEAN 'True')| | x | | | x | x |
|BlockWhenDriftDetected=(BOOLEAN 'True')| | x | | | x | x |
|CommandTimeout=(INT32 '60')| x | x | x | x | x | x |
|CommentOutSetVarDeclarations=(BOOLEAN)| | x | | | x | x |
|CompareUsingTargetCollation=(BOOLEAN)| | x | | | x | x |
|CreateNewDatabase=(BOOLEAN)| | x | | | x | x |
|DacApplicationDescription=(STRING)| x | | | | | |
|DacApplicationName=(STRING)| x | | | | | |
|DacMajorVersion=(INT32 '1')| x | | | | | |
|DacMinorVersion=(INT32 '0')| x | | | | | |
|DatabaseEdition=(ENUM 'Default')| | x | | x | x | x |
|DatabaseLockTimeout=(INT32 '60')| x | x | x | | x | x |
|DatabaseMaximumSize=(INT32)| | x | | x | x | x |
|DatabaseServiceObjective=(STRING)| | x | | x | x | x |
|DeployDatabaseInSingleUserMode=(BOOLEAN)| | x | | | x | x |
|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| | x | | | x | x |
|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')| | x | | | x | x |
|DoNotAlterReplicatedObjects=(BOOLEAN 'True')| | x | | | x | x |
|DoNotDropObjectType=(STRING)| | x | | | x | x |
|DoNotDropObjectTypes=(STRING)| | x | | | x | x |
|DropConstraintsNotInSource=(BOOLEAN 'True')| | x | | | x | x |
|DropDmlTriggersNotInSource=(BOOLEAN 'True')| | x | | | x | x |
|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')| | x | | | x | x |
|DropIndexesNotInSource=(BOOLEAN 'True')| | x | | | x | x |
|DropObjectsNotInSource=(BOOLEAN)| | x | | | x | x |
|DropPermissionsNotInSource=(BOOLEAN)| | x | | | x | x |
|DropRoleMembersNotInSource=(BOOLEAN)| | x | | | x | x |
|DropStatisticsNotInSource=(BOOLEAN 'True')| | x | | | x | x |
|ExcludeObjectType=(STRING)| | x | | | x | x |
|ExcludeObjectTypes=(STRING)| | x | | | x | x |
|ExtractAllTableData=(BOOLEAN)| x | | | | | |
|ExtractApplicationScopedObjectsOnly=(BOOLEAN 'True')| x | | | | | |
|ExtractReferencedServerScopedElements=(BOOLEAN 'True')| x | | | | | |
|ExtractUsageProperties=(BOOLEAN)| x | | | | | |
|GenerateSmartDefaults=(BOOLEAN)| | x | | | x | x |
|IgnoreAnsiNulls=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreAuthorizer=(BOOLEAN)| | x | | | x | x |
|IgnoreColumnCollation=(BOOLEAN)| | | | | x | x |
|IgnoreColumnOrder=(BOOLEAN)| | x | | | x | x |
|IgnoreComments=(BOOLEAN)| | x | | | x | x |
|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreDdlTriggerOrder=(BOOLEAN)| | x | | | x | x |
|IgnoreDdlTriggerState=(BOOLEAN)| | x | | | x | x |
|IgnoreDefaultSchema=(BOOLEAN)| | x | | | x | x |
|IgnoreDmlTriggerOrder=(BOOLEAN)| | x | | | x | x |
|IgnoreDmlTriggerState=(BOOLEAN)| | x | | | x | x |
|IgnoreExtendedProperties=(BOOLEAN)| x | x | | | x | x |
|IgnoreFileAndLogFilePath=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreFilegroupPlacement=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreFileSize=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreFillFactor=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreIdentitySeed=(BOOLEAN)| | x | | | x | x |
|IgnoreIncrement=(BOOLEAN)| | x | | | x | x |
|IgnoreIndexOptions=(BOOLEAN)| | x | | | x | x |
|IgnoreIndexPadding=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreKeywordCasing=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreLockHintsOnIndexes=(BOOLEAN)| | x | | | x | x |
|IgnoreLoginSids=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreNotForReplication=(BOOLEAN)| | x | | | x | x |
|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')| | x | | | x | x |
|IgnorePartitionSchemes=(BOOLEAN)| | x | | | x | x |
|IgnorePermissions=(BOOLEAN 'True')| x | x | | | x | x |
|IgnoreQuotedIdentifiers=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreRoleMembership=(BOOLEAN)| | x | | | x | x |
|IgnoreRouteLifetime=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreTableOptions=(BOOLEAN)| | x | | | x | x |
|IgnoreTablePartitionOptions=(BOOLEAN)| | x | | | x | x |
|IgnoreUserLoginMappings=(BOOLEAN)| x | | | | | |
|IgnoreUserSettingsObjects=(BOOLEAN)| | x | | | x | x |
|IgnoreWhitespace=(BOOLEAN 'True')| | x | | | x | x |
|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)| | x | | | x | |
|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)| | x | | | x | |
|ImportContributorArguments=(STRING)| | | | x | | |
|ImportContributors=(STRING)| | | | x | | |
|ImportContributorPaths=(STRING)| | | | x | | |
|IncludeCompositeObjects=(BOOLEAN)| | x | | | x | x |
|IncludeTransactionalScripts=(BOOLEAN)| | x | | | x | x |
|LongRunningCommandTimeout=(INT32)| x | x | x | x | x | x |
|NoAlterStatementsToChangeClrTypes=(BOOLEAN)| | x | | | x | x |
|PopulateFilesOnFileGroups=(BOOLEAN 'True')| | x | | | x | x |
|RegisterDataTierApplication=(BOOLEAN)| | x | | | x | x |
|RunDeploymentPlanExecutors=(BOOLEAN)| | x | | | x | x |
|ScriptDatabaseCollation=(BOOLEAN)| | x | | | x | x |
|ScriptDatabaseCompatibility=(BOOLEAN)| | x | | | x | x |
|ScriptDatabaseOptions=(BOOLEAN 'True')| | x | | | x | x |
|ScriptDeployStateChecks=(BOOLEAN)| | x | | | x | x |
|ScriptFileSize=(BOOLEAN)| | x | | | x | x |
|ScriptNewConstraintValidation=(BOOLEAN 'True')| | x | | | x | x |
|ScriptRefreshModule=(BOOLEAN 'True')| | x | | | x | x |
|Storage=({File&#124;Memory} 'File')| x | x | x | x | x | x |
|TableData=(STRING)| x | | x | | | |
|TargetEngineVersion=(ENUM 'Latest')| | | x | | | |
|TempDirectoryForTableData=(STRING)| x | | x | | | |
|TreatVerificationErrorsAsWarnings=(BOOLEAN)| | x | | | x | x |
|UnmodifiableObjectWarnings=(BOOLEAN 'True')| | x | | | x | x |
|VerifyCollationCompatibility=(BOOLEAN 'True')| | x | | | x | x |
|VerifyDeployment=(BOOLEAN 'True')| | x | | | x | x |
|VerifyExtraction=(BOOLEAN)| x | | | | | |
|VerifyFullTextDocumentTypesSupported=(BOOLEAN)| | | x | | | |


## <a name="next-steps"></a>次のステップ

- [SqlPackage Extract](sqlpackage-extract.md) について詳しく学習する
- [SqlPackage Publish](sqlpackage-publish.md) について詳しく学習する
- [SqlPackage Export](sqlpackage-export.md) について詳しく学習する
- [SqlPackage Import](sqlpackage-import.md) について詳しく学習する
