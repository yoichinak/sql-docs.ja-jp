---
title: SQL Server サービスの開始、停止、一時停止、再開、再起動
description: さまざまな SQL Server サービスを開始、停止、一時停止、再開、または再起動する方法を確認します。 これらのアクションに対して Transact-SQL、PowerShell、その他のツールを使用する方法をご覧ください。
ms.custom: ''
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e971592b20dd2321e4265752cb8b01c38387b639
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670755"
---
# <a name="start-stop-pause-resume-restart-sql-server-services"></a>SQL Server サービスの開始、停止、一時停止、再開、再起動

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

このトピックでは、SQL Server 構成マネージャー、SQL Server Management Studio (SSMS)、コマンド プロンプトからの net コマンド、Transact-SQL、または PowerShell を使用して、SQL Server データベース エンジン、SQL Server エージェント、または SQL Server Browser サービスを、開始、停止、一時停止、再開、または再起動する方法について説明します。

## <a name="identify-the-service"></a>サービスを識別する

SQL Server コンポーネントは、Windows サービスとして実行される実行可能プログラムです。 Windows サービスとして実行されるプログラムは、コンピューター画面にアクティビティを表示することなく動作を続行できます。

### <a name="database-engine-service"></a>データベース エンジン サービス

SQL Server データベース エンジンである実行可能プロセス。 データベース エンジンは、既定のインスタンス (1 台のコンピューターにつき 1 つのみ) にすることも、データベース エンジンの多数の名前付きインスタンスの 1 つにすることもできます。 コンピューターにインストールされているデータベース エンジンのインスタンスを判別するには、SQL Server 構成マネージャーを使用します。 既定のインスタンス (インストールした場合) は、**SQL Server (MSSQLSERVER)** として表示されます。 名前付きインスタンス (インストールした場合) は、**SQL Server (<インスタンス名>)** として表示されます。 既定では、SQL Server Express は **SQL Server (SQLEXPRESS)** としてインストールされます。

### <a name="sql-server-agent-service"></a>SQL Server エージェント サービス

ジョブおよび警告と呼ばれる管理タスクをスケジュールに従って実行する Windows サービスです。 詳しくは、「 [SQL Server Agent](../../ssms/agent/sql-server-agent.md)」をご覧ください。 SQL Server エージェントは、SQL Server のすべてのエディションで使用できるわけではありません。 SQL Server の各エディションでサポートされる機能の一覧については、[SQL Server 2019 の各エディションでサポートされる機能](../../sql-server/editions-and-components-of-sql-server-version-15.md)に関する記事を参照してください。

### <a name="sql-server-browser-service"></a>SQL Server Browser サービス

SQL Server の各種リソースに関する着信要求を受信し、コンピューターにインストールされている SQL Server インスタンスに関するクライアント情報を提供する Windows サービスです。 コンピューターにインストールされている SQL Server のすべてのインスタンスに対して、SQL Server Browser サービスのインスタンスが 1 つ使用されます。

### <a name="additional-information"></a>追加情報

- データベース エンジン サービスを一時停止すると、新しいユーザーはデータベース エンジンに接続できなくなりますが、既に接続しているユーザーは接続が切断されるまで処理を続行できます。 ユーザーの処理の完了を待ってからサービスを停止する場合は、一時停止を使用してください。 これにより、ユーザーが実行中のトランザクションを完了できます。 "*再開*" すると、データベース エンジンが再び新しい接続を受け入れられるようになります。 SQL Server エージェント サービスを一時停止および再開することはできません。  

- SQL Server 構成マネージャーおよび SSMS では、次のアイコンを使用してサービスの現在の状態が表示されます。  

    **SQL Server 構成マネージャー**

  - サービス名の隣にあるアイコン上の緑色の矢印は、サービスが開始されていることを示します。

  - サービス名の隣にあるアイコン上の赤い四角形は、サービスが停止していることを示します。

  - サービス名の隣にあるアイコン上の 2 本の青い縦線は、サービスが一時停止していることを示します。

  - データベース エンジンを再起動すると、サービスが停止したことが赤い四角形によって示された後、サービスが正常に開始されたことが緑色の矢印によって示されます。

    **SQL Server Management Studio (SSMS)**

  - サービス名の隣にある緑色の円形のアイコン上の白い矢印は、サービスが開始されていることを示します。  

  - サービス名の隣にある赤い円形のアイコン上の白い四角形は、サービスが停止していることを示します。  

  - サービス名の隣にある青い円形のアイコン上の 2 本の白い縦線は、サービスが一時停止していることを示します。  

- SQL Server 構成マネージャーまたは SSMS の使用時は、実行できるオプションのみが利用可能になります。 たとえば、サービスが既に開始されている場合、 **[開始]** は利用できません。

- クラスターで実行中の SQL Server データベース エンジン サービスを管理するには、クラスター アドミニストレーターを使用するのが最適です。  

### <a name="security"></a>セキュリティ

#### <a name="permissions"></a>アクセス許可

サービスを開始、停止、一時停止、再開、または再起動できるのは、既定ではローカル管理者グループのメンバーだけです。 管理者以外のユーザーがサービスを管理できるようにする方法については、「 [[HOWTO] Windows Server 2003 でサービスを管理する権利をユーザーに付与する](https://support.microsoft.com/kb/325349)」をご覧ください (Windows Server の他のバージョンでも処理は同じです)。

Transact-SQL の **SHUTDOWN** コマンドを使用してデータベース エンジンを停止するには、**sysadmin** または **serveradmin** の固定サーバー ロールのメンバーシップが必要です。この権限を譲渡することはできません。

## <a name="sql-server-configuration-manager"></a>SQL Server 構成マネージャー

### <a name="starting-sql-server-configuration-manager"></a>SQL Server 構成マネージャーの開始

**[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。

SQL Server 構成マネージャーは Microsoft 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、SQL Server 構成マネージャーはアプリケーションとして表示されません。 最新の 4 つのバージョンへのパスを次に示します (Windows が C ドライブにインストールされている場合)。  

|Version|Path|
|-|-|
|SQL Server 2019|C:\Windows\SysWOW64\SQLServerManager15.msc|
|SQL Server 2017|C:\Windows\SysWOW64\SQLServerManager14.msc|
|SQL Server 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|
|SQL Server 2014|C:\Windows\SysWOW64\SQLServerManager12.msc|
|SQL Server 2012|C:\Windows\SysWOW64\SQLServerManager11.msc|

#### <a name="to-start-stop-pause-resume-or-restart-an-instance-of-the-sql-server-database-engine"></a><a name="configmande"></a> SQL Server データベース エンジンのインスタンスを開始、停止、一時停止、再開、または再起動するには

1. 上記の手順を使用して、SQL Server 構成マネージャーを開始します。

2. **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。

3. SQL Server 構成マネージャーの左側のペインで、 **[SQL Server のサービス]** をクリックします。

4. 結果ペインで **[SQL Server (MSSQLServer)]** または名前付きインスタンスを右クリックし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。

5. **[OK]** をクリックして、SQL Server 構成マネージャーを閉じます。

> [!NOTE]
> スタートアップ オプションを指定して SQL Server データベース エンジンのインスタンスを開始する方法については、[サーバー起動オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md) に関する記事をご覧ください。  

#### <a name="to-start-stop-pause-resume-or-restart-the-sql-server-browser-or-an-instance-of-the-sql-server-agent"></a>SQL Server Browser または SQL Server エージェントのインスタンスを開始、停止、一時停止、再開、または再起動するには

1. 上記の手順を使用して、SQL Server 構成マネージャーを開始します。

2. **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。

3. SQL Server 構成マネージャーの左側のペインで、 **[SQL Server のサービス]** をクリックします。

4. 結果ウィンドウで **[SQL Server Browser]** 、または **[SQL Server エージェント (MSSQLServer)]** (名前付きインスタンスの場合には **[SQL Server エージェント (<インスタンス名)]** ) を右クリックし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。  

5. **[OK]** をクリックして、SQL Server 構成マネージャーを閉じます。  

> [!NOTE]
> SQL Server エージェントは一時停止できません。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

### <a name="to-start-stop-pause-resume-or-restart-an-instance-of-the-sql-server-database-engine"></a><a name="ssmsde"></a> SQL Server データベース エンジンのインスタンスを開始、停止、一時停止、再開、または再起動するには

1. オブジェクト エクスプローラーで、データベース エンジンのインスタンスに接続し、開始するデータベース エンジンのインスタンスを右クリックして、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。

    または、[登録済みサーバー] で、開始するデータベース エンジンのインスタンスを右クリックし、 **[サービス コントロール]** をポイントし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。

2. **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。

3. 操作するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。  

#### <a name="to-start-stop-or-restart-an-instance-of-the-sql-server-agent"></a>SQL Server エージェントのインスタンスを開始、停止、または再起動するには

1. オブジェクト エクスプローラーで、データベース エンジンのインスタンスに接続し、 **[SQL Server エージェント]** を右クリックして、 **[開始]** 、 **[停止]** 、または **[再起動]** をクリックします。

2. **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。

3. 操作するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

## <a name="command-prompt-window-using-net-commands"></a><a name="CommandPrompt"></a> コマンド プロンプト ウィンドウでの net コマンドの使用

Microsoft Windows の **net** コマンドを使用して、Microsoft SQL Server サービスを開始、停止、または一時停止できます。

### <a name="to-start-the-default-instance-of-the-database-engine"></a><a name="dbDefault"></a> データベース エンジンの既定のインスタンスを開始するには

- コマンド プロンプトで、次のいずれかのコマンドを入力します。  
  
    **net start "SQL Server (MSSQLSERVER)"**

   または  

    **net start MSSQLSERVER**

### <a name="to-start-a-named-instance-of-the-database-engine"></a><a name="dbNamed"></a> データベース エンジンの名前付きインスタンスを開始するには

- コマンド プロンプトで、次のいずれかのコマンドを入力します。 *\<instancename>* は、管理するインスタンスの名前に置き換えます。  
  
    **net start "SQL Server (** *instancename* **)"**
  
   または  
  
    **net start MSSQL$** *instancename*  
  
### <a name="to-start-the-database-engine-with-startup-options"></a><a name="dbStartup"></a> スタートアップ オプションを使用してデータベース エンジンを開始するには  

- **net start "SQL Server (MSSQLSERVER)"** ステートメントの末尾に、スタートアップ オプションをスペースで区切って追加します。 **net start**を使用して起動するときは、スタートアップ オプションでハイフン (-) の代わりにスラッシュ (/) を使用します。  
  
    **net start "SQL Server (MSSQLSERVER)" /f /m**
  
   または  
  
    **net start MSSQLSERVER /f /m**
  
  > [!NOTE]
  >  スタートアップ オプションの詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」をご覧ください。  
  
###  <a name="to-start-the-sql-server-agent-on-the-default-instance-of-sql-server"></a><a name="agDefault"></a> SQL Server の既定のインスタンスで SQL Server エージェントを開始するには
  
- コマンド プロンプトで、次のいずれかのコマンドを入力します。  
  
    **net start "SQL Server Agent (MSSQLSERVER)"**
  
   または  
  
    **net start SQLSERVERAGENT**
  
###  <a name="to-start-the-sql-server-agent-on-a-named-instance-of-sql-server"></a><a name="agNamed"></a> SQL Server の名前付きインスタンスで SQL Server エージェントを開始するには  
  
- コマンド プロンプトで、次のいずれかのコマンドを入力します。 *instancename* は、管理するインスタンスの名前に置き換えます。  
  
    **net start "SQL Server Agent(** *instancename* **)"**
  
   または  
  
    **net start SQLAgent$** *instancename*  
  
 トラブルシューティングのために SQL Server エージェントを詳細モードで実行する方法については、「[sqlagent90 アプリケーション](../../tools/sqlagent90-application.md)」をご覧ください。  

### <a name="to-start-the-sql-server-browser"></a><a name="Browser"></a> SQL Server Browser を開始するには  

- コマンド プロンプトで、次のいずれかのコマンドを入力します。  
  
    **net start "SQL Server Browser"**
  
   または  
  
    **net start SQLBrowser**
  
### <a name="to-pause-or-stop-services-from-the-command-prompt-window"></a><a name="pauseStop"></a> コマンド プロンプト ウィンドウからサービスを一時停止または停止するには  

- サービスを一時停止または停止するには、次のようにコマンドを変更します。  

- サービスを一時停止するには、 **net start** を **net pause**に置き換えます。  

- サービスを停止するには、 **net start** を **net stop**に置き換えます。  

## <a name="transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL

**SHUTDOWN** ステートメントを使用して、データベース エンジンを停止できます。  

### <a name="to-stop-the-database-engine-using-transact-sql"></a>Transact-SQL を使用してデータベース エンジンを停止するには

- 現在実行中の Transact-SQL ステートメントおよびストアド プロシージャが終了するまで待機してからデータベース エンジンを停止するには、次のステートメントを実行します。  
  
    ```sql
    SHUTDOWN;
    ```
  
- データベース エンジンを直ちに停止するには、次のステートメントを実行します。  
  
    ```sql
    SHUTDOWN WITH NOWAIT;
    ```

**SHUTDOWN** ステートメントについて詳しくは、「[SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)」をご覧ください。  

## <a name="powershell"></a><a name="PowerShellProcedure"></a> PowerShell

### <a name="to-start-and-stop-database-engine-services"></a>データベース エンジン サービスを開始および停止するには

1. コマンド プロンプト ウィンドウで、次のコマンドを実行して SQL Server PowerShell を開始します。  

    ```cmd
    sqlps
    ```

2. SQL Server PowerShell コマンド プロンプトで、次のコマンドを実行します。 `computername` は自分のコンピューター名に置き換えます。  

    ```powershell
    # Get a reference to the ManagedComputer class.
    CD SQLSERVER:\SQL\computername
    $Wmi = (get-item .).ManagedComputer
    ```

3. 停止または開始するサービスを指定します。 以下のいずれかの行を選択してください。 `instancename` は名前付きインスタンスの名前に置き換えます。

    - データベース エンジンの既定のインスタンスへの参照を取得する場合

        ```powershell
        $DfltInstance = $Wmi.Services['MSSQLSERVER']
        ```

    - データベース エンジンの名前付きインスタンスへの参照を取得する場合

        ```powershell
        $DfltInstance = $Wmi.Services['MSSQL$instancename']
        ```

    - データベース エンジンの既定のインスタンスの SQL Server エージェント サービスへの参照を取得する場合  

        ```powershell
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']
        ```

    - データベース エンジンの名前付きインスタンスの SQL Server エージェント サービスへの参照を取得する場合  

        ```powershell
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']
        ```

    - SQL Server Browser サービスへの参照を取得する場合

        ```powershell
        $DfltInstance = $Wmi.Services['SQLBROWSER']
        ```

4. 例を実行して、選択したサービスを開始し、停止します。
  
    ```powershell
    # Display the state of the service.
    $DfltInstance
    # Start the service.
    $DfltInstance.Start();
    # Wait until the service has time to start.
    # Refresh the cache.  
    $DfltInstance.Refresh();
    # Display the state of the service.
    $DfltInstance
    # Stop the service.
    $DfltInstance.Stop();
    # Wait until the service has time to stop.
    # Refresh the cache.
    $DfltInstance.Refresh();
    # Display the state of the service.
    $DfltInstance
    ```  
  
##  <a name="using-service-controller-class"></a><a name="ServiceController"></a> ServiceController クラスの使用

ServiceController クラスを使用して、SQL Server サービスや他の Windows サービスを制御することができます。 これを行う方法の例については、「[ServiceController クラス](/dotnet/api/system.serviceprocess.servicecontroller?view=netframework-4.8)」を参照してください。

## <a name="manage-the-sql-server-service-on-linux"></a>Linux 上の SQL Server サービスを管理する

### <a name="to-start-stop-or-restart-an-instance-of-the-sql-server-database-engine"></a>SQL Server データベース エンジンのインスタンスを開始、停止、または再起動するには

以下では、[Linux 上の SQL Server サービス](../../linux/sql-server-linux-troubleshooting-guide.md#manage-the-sql-server-service)の開始、停止、再起動、および状態の確認を行う方法について説明します。

次のコマンドを使って、SQL Server サービスの状態を確認します。

   ```bash
   sudo systemctl status mssql-server
   ```

必要に応じて、次のコマンドを使って、SQL Server サービスを停止、開始、または再起動することができます。

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

## <a name="next-steps"></a>次のステップ

- [SQL Server セットアップのドキュメントの概要](../install-windows/install-sql-server.md)
- [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)
- [最小構成での SQL Server の起動](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)
- [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)