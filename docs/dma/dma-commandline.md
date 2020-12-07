---
title: コマンドラインから Data Migration Assistant を実行する
description: コマンドラインから Data Migration Assistant を実行して、移行用の SQL Server データベースを評価する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 846c44ff4655fbdc9d508b59b7d637023b4c4ca5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726275"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>コマンドラインから Data Migration Assistant を実行する

バージョン2.1 以降では、Data Migration Assistant をインストールすると、 *% ProgramFiles% \\ Microsoft Data Migration Assistant \\ *に dmacmd.exe もインストールされます。 dmacmd.exe を使用して、データベースを無人モードで評価し、結果を JSON または CSV ファイルに出力します。 この方法は、複数のデータベースや大規模なデータベースを評価する場合に特に役立ちます。 

> [!NOTE]
> Dmacmd.exe は、評価の実行のみをサポートしています。 現時点では移行はサポートされていません。

## <a name="assessments-using-the-command-line-interface-cli"></a>コマンドラインインターフェイス (CLI) を使用した評価

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|引数  |説明  | 必須 (Y/N)
|---------|---------|---------------|
| `/help or /?`     | dmacmd.exe のヘルプテキストの使用方法        | N
|`/AssessmentName`     |   評価プロジェクトの名前   | Y
|`/AssessmentDatabases`     | 空白で区切られた接続文字列の一覧です。 データベース名 (初期カタログ) では大文字と小文字が区別されます。 | Y
|`/AssessmentSourcePlatform`     | 評価のソースプラットフォーム: <br>評価でサポートされる値: SqlOnPrem、RdsSqlServer (既定) <br>ターゲット準備状態評価でサポートされる値: SqlOnPrem、RdsSqlServer (既定)、Cassandra (プレビュー)   | N
|`/AssessmentTargetPlatform`     | 評価のターゲットプラットフォーム:  <br> 評価でサポートされている値: AzureSqlDatabase、ManagedSqlServer、SqlServer2012、SqlServer2014、Sqlserver2016-ssei-expr、SqlServerLinux2017、および SqlServerWindows2017 (既定)  <br> ターゲット準備評価でサポートされる値: ManagedSqlServer (既定値)、CosmosDB (プレビュー)   | N
|`/AssessmentEvaluateFeatureParity`  | 機能のパリティルールを実行します。 ソースプラットフォームが RdsSqlServer の場合、ターゲットプラットフォーム AzureSqlDatabase では、機能のパリティ評価はサポートされていません。  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 互換性規則の実行  | Y <br> (AssessmentEvaluateCompatibilityIssues または AssessmentEvaluateRecommendations のいずれかが必要です。)
|`/AssessmentEvaluateRecommendations`     | 機能に関する推奨事項の実行        | Y <br> (AssessmentEvaluateCompatibilityIssues または AssessmentEvaluateRecommendations のいずれかが必要です)
|`/AssessmentOverwriteResult`     | 結果ファイルを上書きする    | N
|`/AssessmentResultJson`     | JSON 結果ファイルへの完全パス     | Y <br> (AssessmentResultJson または AssessmentResultCsv のいずれかが必要です)
|`/AssessmentResultCsv`    | CSV 結果ファイルへの完全パス   | Y <br> (AssessmentResultJson または AssessmentResultCsv のいずれかが必要です)
|`/AssessmentResultDma`    | Dma 結果ファイルへの完全パス   | N
|`/Action`    | SKU の推奨事項を取得するには、SkuRecommendation を使用します。 <br> AssessTargetReadiness を使用して、ターゲットの準備状態の評価を実行します。 <br> AzureMigrateUpload を使用して、Azzess/Action のすべての DMA 評価ファイルをアップロードして Azure Migrate に一括アップロードします。アクションの種類の使用法 = AzureMigrateUpload   | N
|`/SourceConnections`    | 空白で区切られた接続文字列の一覧です。 データベース名 (初期カタログ) は省略可能です。 データベース名が指定されていない場合は、ソースのすべてのデータベースが評価されます。   | Y <br> (Action が ' AssessTargetReadiness ' の場合に必要です)
|`/TargetReadinessConfiguration`    | 名前、ソース接続、および結果ファイルの値を記述する XML ファイルへの完全パスです。   | Y <br> (TargetReadinessConfiguration または SourceConnections のいずれかが必要です)
|`/FeatureDiscoveryReportJson`    | 機能検出の JSON レポートへのパス。 このファイルが生成された場合は、ソースに接続せずに、ターゲット準備の評価を再実行するために使用できます。 | N
|`/ImportFeatureDiscoveryReportJson`    | 前に作成した機能検出 JSON レポートのパス。 ソース接続ではなく、このファイルが使用されます。   | N
|`/EnableAssessmentUploadToAzureMigrate`    | 評価結果をアップロードして Azure Migrate に発行できるようにします   | N
|`/AzureCloudEnvironment`    |接続先の Azure クラウド環境を選択します。既定値は Azure パブリッククラウドです。 サポートされている値: Azure (既定)、AzureChina、AzureGermany、AzureUSGovernment。   | N 
|`/SubscriptionId`    |Azure サブスクリプション ID。   | Y <br> (EnableAssessmentUploadToAzureMigrate 引数が指定されている場合は必須)
|`/AzureMigrateProjectName`    |評価結果をアップロードする Azure Migrate プロジェクト名。   | Y <br> (EnableAssessmentUploadToAzureMigrate 引数が指定されている場合は必須)
|`/ResourceGroupName`    |Azure Migrate リソースグループ名。   | Y <br> (EnableAssessmentUploadToAzureMigrate 引数が指定されている場合は必須)
|`/AssessmentResultInputFolder`    |を格納している入力フォルダーのパス。Azure Migrate にアップロードする DMA 評価ファイル。   | Y <br> (アクションが AzureMigrateUpload の場合は必須)



## <a name="examples-of-assessments-using-the-cli"></a>CLI を使用した評価の例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Windows 認証を使用した単一データベース評価と互換性規則の実行**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**SQL Server 認証と実行機能の推奨事項を使用した単一データベース評価**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**ターゲットプラットフォームの単一データベース評価 SQL Server 2012、結果を json および .csv ファイルに保存する**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**ターゲットプラットフォームの Azure SQL Database に対する単一データベース評価、結果を json および .csv ファイルに保存する**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**複数データベースの評価**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**Windows 認証を使用した単一データベースのターゲット準備状態評価**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**SQL Server 認証を使用した単一データベースのターゲット準備状態評価**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**ターゲットプラットフォームの Azure SQL Database に対する単一データベース評価、結果を json および .csv ファイルに保存する**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**複数データベースのターゲット準備の評価**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true"
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**Windows 認証を使用したサーバー上のすべてのデータベースのターゲット準備状態評価**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**前に作成した機能検出レポートをインポートすることによるターゲット準備の評価**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**構成ファイルを指定したターゲット準備状態評価**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

ソース接続を使用する場合の構成ファイルの内容:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

機能検出レポートをインポートするときの構成ファイルの内容:

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```
**Azure パブリッククラウドでの Azure Migrate の評価とアップロード (既定)**
```
DmaCmd.exe
/Action="Assess" 
/AssessmentSourcePlatform=SqlOnPrem 
/AssessmentTargetPlatform=ManagedSqlServer
/AssessmentEvaluateCompatibilityIssues 
/AssessmentEvaluateRecommendations 
/AssessmentEvaluateFeatureParity 
/AssessmentOverwriteResult 
/AssessmentName="assess-myDatabase"
/AssessmentDatabases="Server=myServer;Initial Catalog=myDatabase;Integrated Security=true" 
/AssessmentResultDma="C:\assessments\results\assess-1.dma"
/SubscriptionId="Subscription Id" 
/AzureMigrateProjectName="Azure Migrate project ame" 
/ResourceGroupName="Resource Group name" 
/AzureAuthenticationInteractiveAuthentication
/AzureAuthenticationTenantId="Azure Tenant Id"
/EnableAssessmentUploadToAzureMigrate

```
**Batch upload DMA 評価ファイルを Azure パブリッククラウドの Azure Migrate にアップロードする (既定)**
```
DmaCmd.exe 
/Action="AzureMigrateUpload" 
/AssessmentResultInputFolder="C:\assessments\results" 
/SubscriptionId="Subscription Id" 
/AzureMigrateProjectName="Azure Migrate project name" 
/ResourceGroupName="Resource Group name" 
/AzureAuthenticationInteractiveAuthentication
/AzureAuthenticationTenantId="Azure Tenant Id"
/EnableAssessmentUploadToAzureMigrate

```
## <a name="azure-sql-database--azure-sql-managed-instance-sku-recommendations-using-the-cli"></a>CLI を使用した Azure SQL Database/Azure SQL Managed Instance SKU の推奨事項

これらのコマンドは、Azure SQL Database 単一データベースと Azure SQL Managed Instance デプロイオプションの両方の推奨事項をサポートしています。

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|引数  |説明  | 必須 (Y/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | DMA コマンドラインを使用して SKU 評価を実行する | Y
|`/SkuRecommendationInputDataFilePath` | データベースをホストしているコンピューターから収集されたパフォーマンスカウンターファイルの完全パス | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV の結果ファイルの完全パス | Y <br> (TSV、JSON、または HTML ファイルパスが必要です)
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 結果ファイルへの完全パス | Y <br> (TSV、JSON、または HTML ファイルパスが必要です)
|`/SkuRecommendationHtmlResultsFilePath` | HTML 結果ファイルへの完全パス | Y <br> (TSV、JSON、または HTML ファイルパスが必要です)
|`/SkuRecommendationPreventPriceRefresh` | 価格更新が行われないようにします。 オフラインモード (true など) で実行している場合は、を使用します。 | Y <br> (静的な価格にはこの引数を選択します。最新の価格を取得するには、以下のすべての引数を選択する必要があります)
|`/SkuRecommendationCurrencyCode` | 価格を表示する通貨 (例: "USD") | Y <br> (最新の価格の場合)
|`/SkuRecommendationOfferName` | プラン名 (例: "MS-AZR-0003P")。 詳細については、 [Microsoft Azure プランの詳細](https://azure.microsoft.com/support/legal/offer-details/) に関するページを参照してください。 | Y <br> (最新の価格の場合)
|`/SkuRecommendationRegionName` | リージョン名 (例: "WestUS") | Y <br> (最新の価格の場合)
|`/SkuRecommendationSubscriptionId` | サブスクリプション ID です。 | Y <br> (最新の価格の場合)
|`/SkuRecommendationDatabasesToRecommend` | 推奨するデータベースのスペース区切りの一覧 (例: "Database1" "Database2" "Database3")。 名前は大文字と小文字が区別され、二重引用符で囲む必要があります。 省略した場合、すべてのデータベースの推奨事項が表示されます。 | N
|`/AzureAuthenticationTenantId` | 認証テナント。 | Y <br> (最新の価格の場合)
|`/AzureAuthenticationClientId` | 認証に使用される Azure AD アプリのクライアント ID。 | Y <br> (最新の価格の場合)
|`/AzureAuthenticationInteractiveAuthentication` | ウィンドウをポップアップ表示するには true に設定します。 | Y <br> (最新の価格の場合) <br>(3 つの認証オプションのいずれかを選択してください-オプション 1)
|`/AzureAuthenticationCertificateStoreLocation` | 証明書ストアの場所 (例: "CurrentUser") に設定します。 | Y <br>(最新の価格の場合) <br> (3 つの認証オプションのいずれかを選択します。オプション 2)
|`/AzureAuthenticationCertificateThumbprint` | 証明書の拇印に設定します。 | Y <br> (最新の価格の場合) <br>(3 つの認証オプションのいずれかを選択します。オプション 2)
|`/AzureAuthenticationToken` | を証明書トークンに設定します。 | Y <br> (最新の価格の場合) <br>(3 つの認証オプションのいずれかを選択します-オプション 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>CLI を使用した SKU 評価の例

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL Database/Azure SQL Managed Instance SKU の推奨価格更新 (最新価格の取得)-対話型認証** 

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**価格更新を使用した Azure SQL Database/Azure SQL Managed Instance SKU の推奨事項 (最新価格を取得)-証明書認証**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**価格更新を使用した Azure SQL Database/Azure SQL Managed Instance 推奨事項 (最新の価格を取得)-トークン認証と推奨するデータベースの指定**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Azure SQL Database/Azure SQL Managed Instance SKU の推奨事項 (価格更新なし) (静的な価格を使用)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>参照
- [Data Migration Assistant](https://aka.ms/get-dma) ダウンロードします。
- この記事では、 [オンプレミスデータベースの適切な AZURE SQL DATABASE SKU を特定](./dma-sku-recommend-sql-db.md)します。