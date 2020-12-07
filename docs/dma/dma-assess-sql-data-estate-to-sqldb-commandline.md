---
title: 'DMACMD: Azure SQL に移行するための SQL Server の準備を評価する'
titleSuffix: Data Migration Assistant
description: Data Migration Assistant コマンドラインツール (DMACMD) を使用して、Azure SQL に移行するための SQL Server データ資産を評価する方法について説明します
ms.date: 10/02/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: ''
ms.openlocfilehash: 35465a761258fb5a7865e711e2809d740b9b9fee
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496810"
---
# <a name="dmacmd-assess-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql"></a>DMACMD: SQL Server のデータ資産の準備状態を評価して Azure SQL に移行する 

多くの組織が Azure に移行しようとしている場合は、既存のオンプレミスの SQL Server インスタンスを評価し、適切な Azure SQL ターゲット Azure SQL Database、Azure SQL Managed Instance、または Azure Vm での SQL Server を特定することが重要です。 

[Data Migration Assistant (DMA)](dma-overview.md) を使用すると、特定の azure sql ターゲットの SQL Server インスタンスを評価し、azure sql に移行する SQL Server データベースの準備状況を測定できます。 DMA 評価の結果を Azure Migrate hub にアップロードして、データ資産全体の集中型の準備状況を表示します。 

この記事では、大規模な評価を実行し、DMA コマンドラインインターフェイス (DMACMD) を使用して結果を Azure Migrate hub にアップロードする方法について説明します。 代わりに、 [DMA GUI](dma-assess-sql-data-estate-to-sqldb.md) を使用して評価を実行することもできます。

詳細については、次の Channel9 ビデオを参照してください。

>
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-to-Assess-Readiness-of-SQL-Server-Data-Estate-Migrating-to-Azure-SQL/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>前提条件 

DMACMD を使用して評価を実行し、結果を Azure Migrate hub にアップロードするには、次のものが必要です。 

- [Data Migration Assistant (DMA) の最新バージョン](https://www.microsoft.com/en-us/download/details.aspx?id=53595)。
- [Azure Migrate プロジェクト](dma-assess-sql-data-estate-to-sqldb.md#create-a-project-and-add-a-tool)。 
- 共同作成者ロールは、Azure Migrate プロジェクトリソースにアクセスします。

## <a name="use-dmacmd"></a>DMACMD を使用する

コマンドラインインターフェイス (DMACMD.exe) を使用して大規模に評価を実行するには、入力として XML ファイルを使用します。 

次のサンプルコマンドを使用して、XML ファイルを DMACMD に渡し、評価を開始します。

```console
C:\Program Files\Microsoft Data Migration Assistant\DmaCmd.exe /Action=Assess /AssessmentConfiguration= C:\Demo\ScaleAssessment\Assess-for-AzureSQLMI.xml
```

サンプルの内容では、 `Assess-for-AzureSQLMI.xml` SQL Managed Instance ターゲットの SQL Server インスタンスを評価する要素を定義します。 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AssessmentConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/AssessmentConfiguration">
   <AssessmentName>Scale-Assessment-for-AzureSQLManagedInstance</AssessmentName>
   <AssessmentSourcePlatform>SqlOnPrem</AssessmentSourcePlatform>
   <AssessmentTargetPlatform>ManagedSqlServer</AssessmentTargetPlatform>
   <AssessmentDatabases>
      <AssessmentDatabase>Server=ServerName\SQL2017;Integrated Security=true</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=AdventureWorks2016</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=TestDB</AssessmentDatabase>
   </AssessmentDatabases>
   <AssessmentResultDma>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.dma</AssessmentResultDma>
   <AssessmentResultJson>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.json</AssessmentResultJson>
   <AssessmentResultCsv>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.csv</AssessmentResultCsv>
   <AssessmentOverwriteResult>true</AssessmentOverwriteResult>
   <AssessmentEvaluateCompatibilityIssues>true</AssessmentEvaluateCompatibilityIssues>
   <AssessmentEvaluateFeatureParity>true</AssessmentEvaluateFeatureParity>
   <AzureCloudEnvironment>Azure</AzureCloudEnvironment>
   <SubscriptionId>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx</SubscriptionId>
   <AzureMigrateProjectName>Scale-Assessment-for-AzureSQLMI</AzureMigrateProjectName>
   <ResourceGroupName>Resource-Group-Name</ResourceGroupName>
   <AzureAuthenticationInteractiveAuthentication>true</AzureAuthenticationInteractiveAuthentication>
   <AzureAuthenticationTenantId>xxxxxxxx-xxxx-xxxxxxxx</AzureAuthenticationTenantId>
   <EnableAssessmentUploadToAzureMigrate>true</EnableAssessmentUploadToAzureMigrate>
</AssessmentConfiguration>
```



## <a name="xml-elements"></a>XML 要素 

DMACMD に渡される XML 要素は、次の表で定義されています。 


|**XML 要素** |**定義**  |
|---------|---------|
|`AssessmentName`|評価の名前|
|`AssessmentSourcePlatform`|ソース SQL Server プラットフォーム。 既定値は `SqlOnPrem` です。|
|`AssessmentTargetPlatform`|ターゲット SQL Server プラットフォーム。  </br> `AzureSqlDatabase` は Azure SQL Database 対象のです。 </br> `ManagedSqlServer` は、Azure SQL Managed Instance ターゲットを対象としています。 </br></br>**AzureSQLMI**サンプルでは、SQL Managed Instance ターゲットを評価します。|
|`AssessmentDatabases`|インスタンス内のすべてのデータベースを評価する必要がある場合は、インスタンス名だけを指定します。それ以外の場合は、各行に特定のデータベースを一覧表示します。 </br></br>**AzureSQLMI**サンプルでは、インスタンス内のすべてのデータベース `Servername\SQL2017` と、インスタンス内の2つの特定のデータベースを評価し `Servername\SQL2016` ます。  |
|`AssessmentResultDma` </br> `AssessmentResultJson` </br> `AssessmentResultCsv` | 結果ファイルの形式を指定します。 `.DMA`、 `.JSON` 、および `.CSV` 。 ダブルクリックし `.DMA` て、DMA UI で開きます。 <br> `AssessmentResultDma` は、評価結果を Azure Migrate hub にアップロードするために必要です。  |
|`AssessmentOverwriteResult`| 、、またはと同じパスの既存の評価結果ファイルを上書きするかどうかを示し `AssessmentResultJson` `AssessmentResultDma` `AssessmentResultCsv` ます。|
|`AssessmentEvaluateCompatibilityIssues` </br> `AssessmentEvaluateFeatureParity` |評価を実行して、互換性の問題と機能のパリティに関する問題をそれぞれ評価します。|
|`AzureCloudEnvironment`|接続先の azure クラウド環境、既定値は Azure パブリッククラウドです。 </br></br> サポートされる値: </br>`Azure (default)`, `AzureChina`, `AzureGermany`, `AzureUSGovernment`.|
|`SubscriptionId`|Azure サブスクリプション ID。|
|`AzureMigrateProjectName`|評価結果をアップロードするプロジェクト名 Azure Migrate ます。|
|`ResourceGroupName`|Azure Migrate リソースグループ名。|
|`AzureAuthenticationInteractiveAuthentication`|認証ウィンドウをポップアップ表示するには、に設定し `true` ます。|
|`AzureAuthenticationTenantId`|Azure Active Directory テナント ID。 </br></br>これは、 [Azure portal](https://portal.azure.com)の Azure Active Directory の**概要**ブレードから取得します。 |
|`EnableAssessmentUploadToAzureMigrate`| `true`評価結果をアップロードして Azure Migrate hub に発行するには、に設定します。|
|   |   |


## <a name="results"></a>結果 

DMACMD は、正常に終了したときに状態を出力します。 


結果出力の例を次に示します。 

```console
Assessment finished for project: Scale-Assessment-for-AzureSQLManagedInstance
DATABASES:
Succeeded             : 4
Failed                : 0
SERVER INSTANCES:
Succeeded             : 2
Failed                : 0
CSV result file       : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.csv
JSON result file      : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.json
--------------------------------------------------------------------------------
```

データ資産全体を一元的に表示するために、 [Azure Migrate](dma-assess-sql-data-estate-to-sqldb.md#view-target-readiness-assessment-results) にアップロードされた結果を表示します。 . 

## <a name="best-practices"></a>ベスト プラクティス 

DMACMD を使用する場合は、次のベストプラクティスについて検討してください。 

- データ資産全体のすべての SQL Server インスタンスを評価するのではなく、アプリケーションに基づいてターゲット SQL Server インスタンスとデータベースを論理的にグループ化します。 
- 結果が上書きされないように、Azure SQL ターゲットごとに個別の Azure Migrate プロジェクトを作成します。 
- 評価を実行する時間は、データベースオブジェクトの数によって異なります。 可能であれば、実稼働システムでの評価の実行と、仮想マシンまたはステージングサーバーへのオフロードを避けてください。特に、多数のオブジェクトがあるデータベースの場合に使用します。 


## <a name="see-also"></a>関連項目

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: ベストプラクティス](../dma/dma-bestpractices.md)

