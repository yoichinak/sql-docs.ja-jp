---
title: SQL Server PowerShell プロバイダー | Microsoft Docs
description: ファイル システム パスと同様のパスを使用して SQL Server オブジェクトへのアクセスを実現する、Windows PowerShell 用の SQL Server プロバイダーについて説明します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 07/31/2019
ms.openlocfilehash: 68546680f73674b416aa42d141c7ea5d2f8b51b7
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081911"
---
# <a name="sql-server-powershell-provider"></a>SQL Server PowerShell Provider

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Windows PowerShell 用の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーは、ファイル システム パスと同様のパスで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトの階層を公開します。 このパスを使用してオブジェクトの場所を指定し、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) モデルのメソッドを使用してオブジェクトの操作を実行できます。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

## <a name="benefits-of-the-sql-server-powershell-provider"></a>SQL Server PowerShell プロバイダーの利点

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーによって実装されているパスを使用すると、SQL Server のインスタンス内のすべてのオブジェクトを簡単に対話的に確認できます。 ファイル システムのパスの操作に一般的に使用されているコマンドと同様の Windows PowerShell の別名を使用して、パスを操作できます。  
  
## <a name="the-sql-server-powershell-hierarchy"></a>SQL Server PowerShell の階層

データまたはオブジェクトのモデルを階層で表すことができる製品は、Windows PowerShell プロバイダーを使用して階層を公開できます。 階層は、Windows ファイル システムで使用されるものに似たドライブおよびパス構造を使用して公開されます。  
  
 それぞれの Windows PowerShell プロバイダーは 1 つ以上のドライブを実装します。 各ドライブは、関連するオブジェクトの階層のルート ノードです。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーは、SQLSERVER: ドライブを実装します。 プロバイダーは、SQLSERVER: ドライブの主要フォルダーのセットも定義します。 各フォルダーおよびそのサブフォルダーは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト モデルを使用してアクセスできるオブジェクトのセットを表します。 これらのいずれかの主要フォルダーで始まるパスでサブフォルダーにフォーカスを設定すると、関連付けられたオブジェクト モデルのメソッドを使用して、このノードによって表されるオブジェクトの操作を実行できます。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] プロバイダーが実装する Windows PowerShell フォルダーを次の表に示します。  
  
|Folder|SQL Server オブジェクト モデルの名前空間|Objects|  
|------------|---------------------------------------|-------------|  
|`SQLSERVER:\SQL`|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|データベース オブジェクト (テーブル、ビュー、ストアド プロシージャなど)|  
|`SQLSERVER:\SQLPolicy`|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|ポリシー ベースの管理オブジェクト (ポリシーやファセットなど)|  
|`SQLSERVER:\SQLRegistration`|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|登録済みサーバー オブジェクト (サーバー グループや登録済みサーバーなど)|  
|`SQLSERVER:\Utility`|<xref:Microsoft.SqlServer.Management.Utility>|ユーティリティ オブジェクト ( [!INCLUDE[ssDE](../includes/ssde-md.md)]のマネージド インスタンスなど)|  
|`SQLSERVER:\DAC`|[Microsoft.SqlServer.Management.Dac](/previous-versions/sql/sql-server-2012/ee212127(v=sql.110))|データ層アプリケーション オブジェクト (DAC パッケージなど) と操作 (DAC の配置など)|  
|`SQLSERVER:\DataCollection`|<xref:Microsoft.SqlServer.Management.Collector>|コレクション セットや構成ストアなどのデータ コレクター オブジェクト|  
|`SQLSERVER:\SSIS`|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクト、パッケージ、環境などのオブジェクト。|  
|`SQLSERVER:\XEvent`|<xref:Microsoft.SqlServer.Management.XEvent>|SQL Server 拡張イベント|
|`SQLSERVER:\DatabaseXEvent`|[Microsoft.SqlServer.Management.XEventDbScoped](/dotnet/api/microsoft.sqlserver.management.xeventdbscoped)|SQL Server 拡張イベント|
|`SQLSERVER:\SQLAS`|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] キューブ、集計、ディメンションなどのオブジェクト。|  
  
 たとえば、SQLSERVER:\SQL フォルダーを使用して、SMO オブジェクト モデルでサポートされる任意のオブジェクトを表すパスを開始することができます。 SQLSERVER:\SQL パスの先頭部分は、SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*です。 インスタンス名の後のノードは、オブジェクト コレクション ( *Databases* 、 *Views*など) とオブジェクト名 (AdventureWorks2012 など) で切り替わります。 スキーマはオブジェクト クラスとしては表されません。 スキーマ内の最上位レベルのオブジェクト (テーブルやビューなど) のノードを指定する場合、オブジェクト名を *SchemaName.ObjectName*の形式で指定する必要があります。  
  
 次の例は、ローカル コンピューター上の [!INCLUDE[ssDE](../includes/ssde-md.md)] の既定のインスタンスにある AdventureWorks2012 データベースの Purchasing スキーマ内の Vendor テーブルのパスを示しています。  
  
```powershell
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```
  
 SMO オブジェクト モデルの階層の詳細については、「 [SMO オブジェクト モデル ダイアグラム](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)」を参照してください。  
  
 パスに含まれるコレクション ノードは、関連付けられたオブジェクト モデルのコレクション クラスに関連付けられます。 オブジェクト名ノードは、次の表に示すように、関連付けられたオブジェクト モデルのオブジェクト クラスに関連付けられます。  
  
|Path|SMO クラス|  
|----------|---------------|  
|`SQLSERVER:\SQL\MyComputer\DEFAULT\Databases`|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|`SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012`|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a>SQL Server プロバイダーのタスク  
  
|タスクの説明|[アーティクル]|  
|----------------------|-----------|  
|パス内のノードを移動し、各ノードでそのノードのオブジェクトの一覧を取得するために Windows PowerShell コマンドレットを使用する方法について説明します。|[SQL Server PowerShell パスの移動](navigate-sql-server-powershell-paths.md)|  
|パス内のノードによって表されているオブジェクトに対するレポート作成や操作を行うための SMO メソッドおよびプロパティを使用する方法について説明します。 また、そのノードの SMO メソッドおよびプロパティの一覧を取得する方法についても説明します。|[SQL Server PowerShell パスの操作](work-with-sql-server-powershell-paths.md)|  
|SMO URN (Uniform Resource Name) を SQL Server プロバイダー パスに変換する方法について説明します。|[URN から SQL Server プロバイダー パスへの変換](/powershell/module/sqlserver/Convert-UrnToPath)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーを使用して SQL Server 認証接続を開く方法について説明します。 既定では、プロバイダーは、Windows PowerShell セッションを実行している Windows アカウントの資格情報を使用して確立された Windows 認証接続を使用します。|[データベース エンジン PowerShell での認証の管理](manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="next-steps"></a>次のステップ

[SQL Server PowerShell](sql-server-powershell.md)