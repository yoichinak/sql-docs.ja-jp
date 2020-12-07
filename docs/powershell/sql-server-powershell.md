---
title: SQL Server PowerShell
description: PowerShell プロバイダーとコマンドレットを含む 2 つの SQL Server PowerShell モジュール (SqlServer と SQLPS) について説明します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 968bcd1560fd4fd24dddfaf45cfe606518235b60
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081891"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)**

SQL Server PowerShell モジュールには、 **[SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)** と **[SQLPS](https://docs.microsoft.com/powershell/module/sqlps)** の 2 つがあります。

**SqlServer** モジュールは、使用する現在の PowerShell モジュールです。

**SQLPS** モジュールは、(後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。

**SqlServer** モジュールには、**SQLPS** のコマンドレットの更新バージョンに加え、最新の SQL 機能をサポートする新しいコマンドレットが含まれています。

[SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) には前のバージョンの **SqlServer** モジュールが含まれて "*いました*" が、それは SSMS の 16.x バージョンのみでした。

SSMS 17.0 以降で PowerShell を使用するには、**SqlServer** モジュールを [PowerShell ギャラリー](https://www.powershellgallery.com/packages/SqlServer)からインストールします。

[Azure Data Studio で PowerShell](../azure-data-studio/extensions/powershell-extension.md) を使用することもできます。

**モジュールが SQLPS から SqlServer に変更された理由**

SQL PowerShell の更新プログラムを出荷するには、SQL PowerShell モジュールの ID と、*SQLPS.exe* で知られるラッパーを変更する必要がありました。 この変更によって、SQL PowerShell モジュールが **SqlServer** モジュールと **SQLPS** モジュールの 2 つになりました。  

**SQLPS モジュールをインポートする場合は、ご利用の PowerShell スクリプトを更新してください。**

`Import-Module -Name SQLPS` を実行する PowerShell スクリプトがあり、新しいプロバイダーの機能と新しいコマンドレットを活用したい場合は、これらを `Import-Module -Name SqlServer` に変更する必要があります。 新しいモジュールは `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer` フォルダーにインストールされます。 そのため、$env:PSModulePath 変数を更新する必要はありません。 **SqlServer** という名前の、サード パーティ製またはコミュニティ バージョンのモジュールを使用するスクリプトがある場合は、名前の競合を避けるため Prefix パラメーターを使用してください。

SQLPS モジュールが同じコンピューターにインストールされている場合、サイド バイ サイドの問題を回避するために、*Import-Module SQLServer* を使用してスクリプトを開始することをお勧めします。

このセクションは、SQL Agent ではなく、PowerShell から実行されるスクリプトに適用されます。 [#NOSQLPS](#sql-server-agent) を使用すれば、新しいモジュールを SQL Agent のジョブ ステップで使用できます。

## <a name="sql-server-powershell-components"></a>SQL Server PowerShell のコンポーネント

**SqlServer** モジュールには、次のものが付属しています。

- [PowerShell プロバイダー](/powershell/module/microsoft.powershell.core/about/about_providers)。これにより、ファイル システム パスと同様の簡単なナビゲーション メカニズムを使用できるようになります。 ファイル システム パスと同様に、ドライブが SQL Server 管理オブジェクト モデルに関連付けられ、ノードがオブジェクト モデルのクラスに基づくパスを構築できます。 その後、 **cd** や **dir** などのなじみのあるコマンドを使用して、コマンド プロンプト ウィンドウでフォルダーを操作するのと同様の方法でパスを操作できます。 **ren** や **del**などの他のコマンドを使用すると、パスのノードで操作を実行できます。

- Transact-SQL または XQuery ステートメントを含む **sqlcmd** コマンドレットの実行などの操作をサポートする、コマンドレットのセット。  

- AS プロバイダーとコマンドレットは、以前は個別にインストールされていました。

## <a name="sql-server-versions"></a>SQL Server のバージョン

SQL PowerShell コマンドレットは、Azure SQL Database、Azure Synapse Analytics、およびすべての[サポートされる SQL Server 製品](https://support.microsoft.com/lifecycle/search/1044)のインスタンスを管理するために使用できます。

## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>PowerShell パスではサポートされない文字を含んだ SQL Server 識別子

**Encode-Sqlname** コマンドレットと **Decode-Sqlname** コマンドレットでは、PowerShell パスではサポートされていない文字を含んだ SQL Server 識別子を指定できます。 詳細については、「 [PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)」を参照してください。

**Convert-UrnToPath** コマンドレットを使用して、Database Engine オブジェクトの Unique Resource Name を SQL Server PowerShell プロバイダーのパスに変換します。 詳細については、「 [URN から SQL Server プロバイダー パスへの変換](/powershell/module/sqlserver/Convert-UrnToPath)」を参照してください。
  
## <a name="query-expressions-and-unique-resource-names"></a>クエリ式および Unique Resource Name  

クエリ式は、オブジェクト モデル階層内の 1 つまたは複数のオブジェクトを列挙する条件のセットを指定するために XPath と同様の構文を使用する文字列です。 URN (Unique Resource Name) は、単一のオブジェクトを一意に識別する特定の種類のクエリ式文字列です。 詳細については、「 [クエリ式と Uniform Resource Name](query-expressions-and-uniform-resource-names.md)」を参照してください。

## <a name="sql-server-agent"></a>SQL Server エージェント

SQL Server エージェントで使用されるモジュールに対する変更はありません。 そのため、PowerShell 型のジョブ ステップを持つ SQL Server エージェント ジョブでは、SQLPS モジュールが使用されます。 詳細については、[SQL Server エージェントで PowerShell を実行する方法](run-windows-powershell-steps-in-sql-server-agent.md)に関する記事を参照してください。 ただし、SQL Server 2019 以降では、SQLPS を無効にすることができます。 そのためには、PowerShell 型のジョブ ステップの最初の行に `#NOSQLPS` を追加します。これにより、SQL Agent による SQLPS モジュールの自動読み込みは停止されます。 これを行うと、コンピューターにインストールされている PowerShell のバージョンがご利用の SQL Agent ジョブによって実行されます。その後、希望する他の任意の PowerShell モジュールを使用できるようになります。

ご利用の SQL Agent ジョブ ステップ内で **SqlServer** モジュールを使用したい場合は、スクリプトの最初の 2 行に次のコードを配置します。

```powershell
#NOSQLPS
Import-Module -Name SqlServer
```

## <a name="cmdlet-reference"></a>コマンドレット リファレンス

- [SqlServer のコマンドレット](/powershell/module/sqlserver)
- [SQLPS のコマンドレット](/powershell/module/sqlps)

## <a name="next-steps"></a>次のステップ

- [SQL Server PowerShell モジュールのダウンロード](download-sql-server-ps-module.md)
- [SQL Server PowerShell コマンドレット](/powershell/module/sqlserver)
- [Azure Data Studio で PowerShell を使用する](../azure-data-studio/extensions/powershell-extension.md)
