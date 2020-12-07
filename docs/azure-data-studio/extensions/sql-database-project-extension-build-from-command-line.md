---
title: コマンド ラインからプロジェクトをビルドする
description: コマンド ラインから SQL Server データベース プロジェクトをビルドします
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 08/07/2020
ms.openlocfilehash: 060039496d5877951e5255fce5e6cac2321731c6
ms.sourcegitcommit: 31f3405be08441471f441395f1d0f0017ebc0ad5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94617930"
---
# <a name="build-a-database-project-from-command-line"></a>コマンド ラインからデータベース プロジェクトをビルドする

Azure Data Studio 用の SQL Database プロジェクト拡張機能では、[データベース プロジェクトをビルドする](sql-database-project-extension-build.md)ためのグラフィカル ユーザー インターフェイスが提供されていますが、Windows、macOS、Linux 環境では、コマンド ラインのビルド エクスペリエンスも使用できます。 この記事では、コマンド ラインで SQL プロジェクトをビルドして DACPAC を作成するために必要な前提条件と構文について説明します。

## <a name="prerequisites"></a>前提条件

1. [Azure Data Studio の SQL データベース プロジェクトの拡張機能](sql-database-project-extension.md)のインストールと構成。

2. SQL Database プロジェクト用の Azure Data Studio 拡張機能でサポートされているすべてのプラットフォームでコマンド ラインから SQL データベース プロジェクトをビルドするには、次の .NET Core DLL とターゲット ファイル `Microsoft.Data.Tools.Schema.SqlTasks.targets` が必要です。 これらのファイルは、Azure Data Studio インターフェイスで実行された最初のビルドの間に拡張機能によって作成され、`BuildDirectory` の下の拡張機能のフォルダーに配置されます。  たとえば、Linux では、これらのファイルは `~\.azuredatastudio\extensions\microsoft.sql-database-projects-x.x.x\BuildDirectory\` に配置されます。  これら 10 個のファイルを新しいアクセス可能なフォルダーにコピーするか、場所を記録しておきます。  このドキュメントでは、この場所を `DotNet Core build folder` と呼びます。

    - Microsoft.Data.Tools.Schema.Sql.dll
    - Microsoft.Data.Tools.Schema.Tasks.Sql.dll
    - Microsoft.Data.Tools.Utilities.dll
    - System.Io.Packaging.dll
    - Microsoft.SqlServer.Dac.dll
    - Microsoft.SqlServer.Dac.Extensions.dll
    - Microsoft.SqlServer.TransactSql.ScriptDom.dll
    - Microsoft.SqlServer.Types.dll
    - Microsoft.Data.Tools.Schema.SqlTasks.targets
    - System.ComponentModel.Composition.dll
    - Microsoft.Data.SqlClient.dll

3. プロジェクトが Azure Data Studio で作成された場合は、「[コマンド ラインからプロジェクトをビルドする](#build-the-project-from-the-command-line)」に進みます。 プロジェクトが SQL Server Data Tools (SSDT) で作成された場合は、Azure Data Studio SQL Database プロジェクト拡張機能でプロジェクトを開きます。  Azure Data Studio でプロジェクトを開くと、以下に示す 3 つの編集で `sqlproj` ファイルが自動的に更新されます。

    1. インポート条件

    ```console
    <Import Condition="'$(NetCoreBuild)' == 'true'" Project="$(NETCoreTargetsPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' != ''" Project="$(SQLDBExtensionsRefPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/>
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' == ''" Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets"/>
    ```

    2. パッケージ リファレンス

    ```console
    <ItemGroup>
        <PackageReference Condition="'$(NetCoreBuild)' == 'true'" Include="Microsoft.NETFramework.ReferenceAssemblies" Version="1.0.0" PrivateAssets="All"/>
    </ItemGroup>
    ```

    3. SQL Server Data Tools (SSDT) と Azure Data Studio でのデュアル編集をサポートするために必要なクリーン ターゲット

        ```console
        <Target Name="AfterClean">
            <Delete Files="$(BaseIntermediateOutputPath)\project.assets.json"/>
        </Target>
        ```

## <a name="build-the-project-from-the-command-line"></a>コマンド ラインからプロジェクトをビルドする

完全な .NET フォルダーから、次のコマンドを使用します。

```console
dotnet build "<sqlproj file path>" /p:NetCoreBuild=true /p:NETCoreTargetsPath="<DotNet Core build folder>"
```

たとえば、Linux では `/usr/share/dotnet` からです。

```console
dotnet build "/home/myuser/Documents/DatabaseProject1/DatabaseProject1.sqlproj" /p:NetCoreBuild=true /p:NETCoreTargetsPath="/home/myuser/.azuredatastudio-insiders/extensions/microsoft.sql-database-projects-0.1.2/BuildDirectory"  
```

## <a name="next-steps"></a>次のステップ

- [Azure Data Studio の SQL データベース プロジェクトの拡張機能](sql-database-project-extension.md)
- [SQL データベース プロジェクトを発行する](sql-database-project-extension-build.md#publish-a-database-project)
