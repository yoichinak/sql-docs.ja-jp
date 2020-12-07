---
description: PowerShell を使用して SSIS パッケージを実行する
title: PowerShell を使用して SSIS パッケージを実行する | Microsoft Docs
ms.date: 09/17/2020
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a876164579679802c5dc0335d01dd5ec8839e95b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "90989925"
---
# <a name="run-an-ssis-package-with-powershell"></a>PowerShell を使用して SSIS パッケージを実行する

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


このクイックスタートでは、PowerShell スクリプトを使用してデータベース サーバーに接続し、SSIS パッケージを実行する方法を示します。

## <a name="prerequisites"></a>前提条件

Azure SQL Database サーバーは、ポート 1433 でリッスンします。 企業のファイアウォール内から Azure SQL Database サーバーに接続しようとする場合、正常に接続するには、このポートを企業のファイアウォールで開ける必要があります。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を使用して、次のプラットフォームで SSIS パッケージを実行することができます。

-   SQL Server on Windows。

-   Azure Data Factory (ADF) の SSIS 統合ランタイム (IR)。SSIS カタログ (SSISDB) は Azure SQL Managed Instance (MI) によってホストされます。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

Linux で SSIS パッケージを実行する場合は、このクイックスタートの情報を使用することはできません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

Azure SQL Database でパッケージを実行するには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure portal](https://portal.azure.com/) にサインインします。
2. 左側のメニューから **[SQL Databases]** を選択し、**[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。
5. **[データベース接続文字列の表示]** をクリックします。
6. 完全な **ADO.NET** 接続文字列を確認します。

## <a name="ssis-powershell-provider"></a>SSIS PowerShell プロバイダー
SSIS PowerShell プロバイダーを使用すると、SSIS カタログに接続し、その中のパッケージを実行することができます。

SSIS PowerShell プロバイダーを使用してパッケージ カタログ内の SSIS パッケージを実行する方法の基本的な例を次に示します。

```powershell
(Get-ChildItem SQLSERVER:\SSIS\localhost\Default\Catalogs\SSISDB\Folders\Project1Folder\Projects\'Integration Services Project1'\Packages\ |
WHERE { $_.Name -eq 'Package.dtsx' }).Execute("false", $null)
```

## <a name="powershell-script"></a>PowerShell スクリプト
次のスクリプトの一番上で変数の適切な値を指定し、スクリプトを実行して SSIS パッケージを実行します。

> [!NOTE]
> 次の例では、Windows 認証を使用します。 SQL Server 認証を使用するには、`Integrated Security=SSPI;` 引数を `User ID=<user name>;Password=<password>;` に置き換えます。 Azure SQL Database サーバーに接続する場合、Windows 認証を使用できません。 

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>次のステップ
- パッケージを実行する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md) 
