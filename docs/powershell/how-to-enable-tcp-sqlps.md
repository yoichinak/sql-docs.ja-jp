---
title: SQLPS を使用して TCP プロトコルを有効化する方法
description: SQLPS を使用して TCP プロトコルを有効化する方法について説明します
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 08/06/2020
ms.openlocfilehash: ba4b1362a3f435617f36c75fbcf0e8371169f990
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005156"
---
# <a name="how-to-enable-the-tcp-protocol"></a>TCP プロトコルを有効化する方法

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-with-sqlps"></a>SQLPS を使用してコンソールに接続するとき、TCP プロトコルを有効にする方法

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

1. コマンド プロンプトを開いて、次のように入力します。

    ```console
    C:\> SQLPS.EXE
    ```

    > [!TIP]
    > SQLPS が見つからないときは、場合によっては、新しいコマンド プロンプトを開くか、ログオフして再びログオンする必要があります。

2. PowerShell コマンド プロンプトで次のように入力します。

    ```powershell
    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-not-using-sqlps"></a>SQLPS を使用せずにコンソールに接続するとき、TCP プロトコルを有効にする方法

1. コマンド プロンプトを開いて、次のように入力します。

    ```console
    C:\> PowerShell.exe
    ```

2. PowerShell コマンド プロンプトで次のように入力します。

    ```powershell
    # Get access to SqlWmiManagement DLL on the machine with SQL
    # we are on, which is where SQL Server was installed.
    # Note: this is installed in the GAC by SQL Server Setup.

    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SqlWmiManagement')

    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```

## <a name="next-steps"></a>次のステップ

- [SQL Server PowerShell モジュールをインストールする](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)
- [サーバー ネットワーク プロトコルの有効化または無効化](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
- [Server Core インストールでの SQL Server の構成](../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md)
