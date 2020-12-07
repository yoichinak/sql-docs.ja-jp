---
title: SQL Server PowerShell モジュールのダウンロード
description: SqlServer PowerShell モジュールをインストールする方法について説明します。これには、最新の SQL 機能をサポートするコマンドレットが用意されており、SQLPS モジュールのコマンドレットの更新済みバージョンも含まれています。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 21730bf32e66c5954b2447037286dfdc10717e9c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081541"
---
# <a name="install-the-sql-server-powershell-module"></a>SQL Server PowerShell モジュールをインストールする

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

この記事は、**SqlServer** PowerShell モジュールをインストールする手順を説明しています。

## <a name="powershell-modules-for-sql-server"></a>SQL Server 用の PowerShell モジュール

2 つの SQL Server PowerShell モジュールがあります。

- **SqlServer**: SqlServer モジュールには、最新の SQL 機能をサポートする新しいコマンドレットが含まれています。 モジュールには、**SQLPS** 内のコマンドレットの更新バージョンも含まれています。 SqlServer モジュールをダウンロードするには、[PowerShell ギャラリーの SqlServer モジュール](https://www.powershellgallery.com/packages/Sqlserver)にアクセスします。

- **SQLPS**: SQLPS は、[SQL Agent](sql-server-powershell.md#sql-server-agent) によって、PowerShell サブシステムを使用してエージェント ジョブ ステップでエージェント ジョブを実行するために使用されるモジュールです。

> [!NOTE]
> PowerShell ギャラリーの **SqlServer** モジュールのバージョンは、バージョン管理をサポートし、PowerShell バージョン 5.0 以降が必要です。

ヘルプ トピックについては、次を参照してください。

- [SqlServer](/powershell/module/sqlserver) のコマンドレット。
- [SQLPS](/powershell/module/sqlps) のコマンドレット。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

[SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) では、どちらの PowerShell モジュールもインストールされません。 PowerShell を SSMS で使用するには、**SqlServer** モジュールを [PowerShell ギャラリー](https://www.powershellgallery.com/packages/Sqlserver)からインストールします。

> [!NOTE]
> SSMS 16.x では、前のバージョンの **SqlServer** モジュールが SQL Server Management Studio (SSMS) に含まれています

## <a name="azure-data-studio"></a>Azure Data Studio

[Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) では、どちらの PowerShell モジュールもインストールされません。 PowerShell を Azure Data Studio で使用するには、**SqlServer** モジュールを [PowerShell ギャラリー](https://www.powershellgallery.com/packages/Sqlserver)からインストールします。

[PowerShell 拡張機能](../azure-data-studio/extensions/powershell-extension.md)を使用できます。これにより、Azure Data Studio に高機能な PowerShell エディターのサポートが提供されます。

## <a name="installing-or-updating-the-sqlserver-module"></a>SqlServer モジュールのインストールまたは更新

PowerShell ギャラリーから **SqlServer** モジュールをインストールするには、[PowerShell](/powershell/scripting/overview) セッションを管理者として開始します。 管理者として Azure Data Studio を開始し、統合ターミナルの PowerShell セッションでこれらのコマンドを実行することもできます。

さらに、*Install-Module SQLServer -Scope CurrentUser* を使用して、管理者特権のアクセス許可を実行することもできます。 このコマンドレットは、環境の管理者ではないユーザーに役立ちます。 ただし、スコープは現在のユーザーに制限されるため、同じコンピューター上の他のユーザーはモジュールを使用できません。

### <a name="install-the-sqlserver-module"></a>SqlServer モジュールをインストールする

すべてのユーザー用に SqlServer モジュールをインストールするには、PowerShell セッションで次のコマンドを実行します。

```powershell
Install-Module -Name SqlServer
```

### <a name="to-view-the-versions-of-the-sqlserver-module-installed"></a>インストールされている SqlServer モジュールのバージョンを表示するには

インストールされている SqlServer モジュールのバージョンを確認するには、次のコマンドを実行します。

```powershell
Get-Module SqlServer -ListAvailable
```

### <a name="install-for-the-current-user-rather-than-as-an-administrator"></a>管理者としてではなく、現在のユーザー用にインストールする

管理者として PowerShell セッションを実行できない場合は、次のコマンドを使用して現在のユーザー用にインストールします。

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### <a name="to-overwrite-a-previous-version-of-the-sqlserver-module"></a>SqlServer モジュールの前のバージョンを上書きするには

`Install-Module` コマンドを使用して、前のバージョンを上書きすることもできます。

```powershell
Install-Module -Name SqlServer -AllowClobber
```

> [!Note]
> PowerShell では、インストールされている最新のモジュールが常に使用されます。

### <a name="update-the-installed-version-of-the-sqlserver-module"></a>SqlServer モジュールのインストールされているバージョンを更新する

**SqlServer** モジュールの更新されたバージョンを使用できる場合は、次のコマンドを使用して新しいバージョンをインストールできます。

```powershell
Install-Module -Name SqlServer -AllowClobber
```

`Update-Module` コマンドを使用して、SQLServer PowerShell モジュールの最新バージョンをインストールできますが、古いバージョンは削除されません。 新しいバージョンをサイドバイサイドでインストールすることで、古いモジュールをインストールしたまま、最新バージョンを試すことができます。

ただし、古いバージョンのモジュールを保持しない場合は、`Uninstall-Module` コマンドを使用して前のバージョンを削除できます。

次のコマンドを使用して、複数のバージョンがインストールされているかどうかを一覧表示できます。

```powershell
Get-Module SqlServer -ListAvailable
```

次のコマンドを使用して、古いバージョンを削除できます。

```powershell
Uninstall-module -Name SQLServer -RequiredVersion "<version number>" -AllowClobber
```

### <a name="troubleshooting"></a>トラブルシューティング

インストールに問題が発生した場合は、[Install-module のドキュメント](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1)と [Install-Module の参照](/powershell/module/powershellget/Install-Module)をご覧ください。

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>SqlServer モジュールの特定のバージョンの使用

モジュールの特定のバージョンを使用するには、次のようなコマンドで、特定のバージョン番号を指定してインポートできます。

```powershell
Import-Module SqlServer -Version 21.1.18218
```

## <a name="pre-release-versions-of-the-sqlserver-module"></a>SqlServer モジュールのプレリリース版

SqlServer モジュールのプレリリース ("プレビュー") 版は、PowerShell ギャラリーで入手できます。

> [!IMPORTANT]
> [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) モジュールの一部である更新された *Find-Module* コマンドレットと *Install-Module* コマンドレットを使用して *-AllowPrerelease* スイッチを渡すことで、これらのバージョンを検出してインストールできます。 これらのコマンドレットを使用するには、PowerShellGet モジュールをインストールしてから、新しいセッションを開きます。

### <a name="to-discover-pre-release-versions-of-the-sqlserver-module"></a>SqlServer モジュールのプレリリース版を検出するには

SqlServer モジュールのプレリリース (プレビュー) 版を検出するには、次のコマンドを実行できます。

```powershell
Find-Module SqlServer -AllowPrerelease
```

### <a name="to-install-a-specific-pre-release-version-of-the-sqlserver-module"></a>SqlServer モジュールの特定のプレリリース版をインストールするには

モジュールの特定のプレリリース版をインストールするには、特定のバージョン番号を指定してインストールします。

次のコマンドの使用を試すことができます。

```powershell
Install-Module SqlServer -RequiredVersion 21.1.18218-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>SQL Server PowerShell on Linux

SQL Server PowerShell on Linux をインストールする方法については、「[PowerShell Core で SQL Server on Linux を管理する](../linux/sql-server-linux-manage-powershell-core.md)」を参照してください。

## <a name="other-modules"></a>その他のモジュール

- [Az.Sql](https://www.powershellgallery.com/packages/Az.Sql/) - Windows PowerShell と PowerShell Core の Azure Resource Manager 用 SQL サービス コマンドレット。

- [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc/) - Microsoft SQL Server のデプロイと構成用の DSC リソースを含むモジュール。

## <a name="cmdlet-reference"></a>コマンドレット リファレンス

- [SqlServer のコマンドレット](https://docs.microsoft.com/powershell/module/sqlserver)
- [SQLPS のコマンドレット](https://docs.microsoft.com/powershell/module/sqlps)

## <a name="next-steps"></a>次のステップ

- [SQL Server PowerShell](sql-server-powershell.md)
- [SQL Server PowerShell コマンドレット](https://docs.microsoft.com/powershell/module/sqlserver)
- [Azure Data Studio で PowerShell を使用する](../azure-data-studio/extensions/powershell-extension.md)