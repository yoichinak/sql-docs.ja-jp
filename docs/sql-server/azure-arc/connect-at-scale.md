---
title: SQL Server インスタンスを大規模に Azure Arc に接続する
titleSuffix: ''
description: この記事では、サービス プリンシパルを使用して、Azure Arc 対応 SQL Server サーバー (プレビュー) として SQL Server インスタンスを接続する方法について学習します。
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 0bd60864615e1ffbf2aecac5eb41efa86407ba68
ms.sourcegitcommit: b09f069c6bef0655b47e9953a4385f1b52bada2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92734383"
---
# <a name="connect-sql-server-instances-to-azure-arc-at-scale"></a>SQL Server インスタンスを大規模に Azure Arc に接続する

複数の Windows または Linux マシンにインストールされている複数の SQL Server インスタンスは、[単一のマシンに対して生成したスクリプト](connect.md)と同じものを使用して、Azure Arc に接続することができます。 このスクリプトを使用すると、各マシンとそこにインストールされている SQL Server インスタンスが Azure Arc に接続されて登録されます。最適なエクスペリエンスを得るために、Azure Active Directory [サービス プリンシパル](/azure/active-directory/develop/app-objects-and-service-principals)を使用することをお勧めします。 サービス プリンシパルは、マシンを Azure に接続する場合や、Azure Arc 対応サーバーと Azure Arc 対応 SQL Server サーバー用の Azure リソースを作成する場合に必要な最小限のアクセス許可のみが付与される、特殊な制限付きの管理用 ID です。 これは、テナント管理者のような、より高い特権を持つアカウントを使用するよりも安全で、アクセス制御セキュリティのベスト プラクティスに従っています。  

Connected Machine エージェントをインストールして構成するためのインストール方法を使用するには、使用する自動化された方法に、マシンでの管理者のアクセス許可が付与されている必要があります。 Linux ではルート アカウントを使用し、Windows ではローカルの Administrators グループのメンバーとして実行します。

作業を開始する前に、必ず、[前提条件](overview.md#prerequisites)を確認し、必要なアクセス許可を満たすカスタム ロールを作成したことを確認してください。

## <a name="connecting-multiple-sql-server-instances-on-windows-using-azure-powershell"></a>Azure PowerShell を使用した Windows での複数の SQL Server インスタンスの接続

各マシンには [Azure PowerShell](/powershell/azure/install-az-ps) がインストールされている必要があります。

1. PowerShell を使用してサービス プリンシパルを作成するには、[`New-AzADServicePrincipal`](/powershell/module/az.resources/new-azadserviceprincipal) コマンドレットを使用します。 必ず、出力を変数に格納してください。 そうしないと、後で必要なパスワードを取得できなくなります。

    ```azurepowershell-interactive
    $sp = New-AzADServicePrincipal -DisplayName "Arc-for-servers" -Role <your custom role>
    $sp
    ```

    ```output
    Secret                : System.Security.SecureString
    ServicePrincipalNames : {ad9bcd79-be9c-45ab-abd8-80ca1654a7d1, https://Arc-for-servers}
    ApplicationId         : ad9bcd79-be9c-45ab-abd8-80ca1654a7d1
    ObjectType            : ServicePrincipal
    DisplayName           : Hybrid-RP
    Id                    : 5be92c87-01c4-42f5-bade-c1c10af87758
    Type                  :
    ```

   > [!NOTE]
   > サービス プリンシパルを作成するときのアカウントは、オンボーディングに使用したいサブスクリプションの所有者またはユーザー アクセス管理者であることが必要です。 ロールの割り当てを作成する十分なアクセス許可がない場合、サービス プリンシパルは作成されますが、マシンをオンボードすることはできません。 カスタム ロールの作成手順については、「[必要なアクセス許可](overview.md#required-permissions)」を参照してください。

2. `$sp` 変数に格納されているパスワードを取得します。

   ```azurepowershell-interactive
   $credential = New-Object pscredential -ArgumentList "temp", $sp.Secret
   $credential.GetNetworkCredential().password
   ```
3. サービス プリンシパルのテナント ID の値を取得します。
 
   ```azurepowershell-interactive
   $tenantId= (Get-AzContext).Tenant.Id
   ```
4. 適切なセキュリティ プラクティスを使用して、パスワード、アプリケーション ID およびテナント ID の値をコピーして保存します。 サービス プリンシパルのパスワードを忘れたり紛失したりした場合は、[`New-AzADSpCredential`](/powershell/module/azurerm.resources/new-azurermadspcredential) コマンドレットを使用してリセットできます。

   > [!NOTE]
   > Azure Arc for servers では現在、証明書を使用したサインインがサポートされていないため、サービス プリンシパルには認証のためのシークレットが必要であることに注意してください。

5. 「[SQL Server を Azure Arc に接続する](connect.md)」の手順に従って、ポータルから PowerShell スクリプトをダウンロードします。

6. PowerShell ISE の管理者インスタンスでスクリプトを開き、前述のサービス プリンシパルのプロビジョニング時に生成された値を使用して、次の環境変数を置き換えます。 これらの変数は最初は空になっています。

   ```azurepowershell-interactive
   $servicePrincipalAppId="{serviceprincipalAppID}"
   $servicePrincipalSecret="{serviceprincipalPassword}"
   $servicePrincipalTenantId="{serviceprincipalTenantId}"
   ```

7. 各ターゲット マシンでスクリプトを実行します

## <a name="connecting-multiple-sql-server-instances-on-linux-using-azure-cli"></a>Azure CLI を使用した Linux での複数の SQL Server インスタンスの接続

各ターゲット マシンには、[Azure CLI がインストールされている](/cli/azure/install-azure-cli)必要があります。 サービス プリンシパルの資格情報が提供されており、他のユーザーがまだサインインしていない場合は、登録スクリプトにより、その資格情報で自動的に Azure へのサインインが行われます。 複数の Linux マシン上の SQL Server インスタンスに接続するには、次の手順を使用します。

1. ['az ad sp create-for-rbac'](/cli/azure/ad/sp#az_ad_sp_create_for_rbac) コマンドを使用して、サービス プリンシパルを作成します。

   ```azurecli-interactive
   az ad sp create-for-rbac --name <your service principal name> --role <your custom role name>
   ```

   ```output
   { "appId": "d2ff754a-e10a-4eb6-9cdc-ce6e7a4687db",
     "displayName": "Arc-for-servers",
     "name": "http://Arc-for-servers",
     "password": {SomeRandomlyGeneratedPassword}",
     "tenant": "2530e75f-673b-4841-8270-47ca6a34ef4f"
   }
   ```

   > [!NOTE]
   > サービス プリンシパルを作成するときのアカウントは、オンボーディングに使用したいサブスクリプションの所有者またはユーザー アクセス管理者であることが必要です。 ロールの割り当てを作成する十分なアクセス許可がない場合、サービス プリンシパルは作成されますが、マシンをオンボードすることはできません。 カスタム ロールの作成手順については、「[必要なアクセス許可](overview.md#required-permissions)」を参照してください。

2. 「[SQL Server を Azure Arc に接続する](connect.md)」の手順に従って、ポータルから Linux シェル スクリプトをダウンロードします。

3. スクリプト内の次の変数を、'az ad sp create-for-rbac' コマンドによって返された値を使用して置き換えます。 これらの変数は最初は空になっています。

   ```bash
   servicePrincipalAppId="{serviceprincipalAppID}"
   servicePrincipalSecret="{serviceprincipalPassword}"
   servicePrincipalTenant="{serviceprincipalTenant}"
   ```

3. 各ターゲット マシンでスクリプトを実行します
 
   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="validate-successful-onboarding"></a>オンボードが成功したことを確認する

Azure Arc 対応 SQL Server (プレビュー) に SQL Server インスタンスを登録した後、[Azure portal](https://aka.ms/azureportal) に移動し、新しく作成された Azure Arc リソースを表示します。 接続されているマシンごとに新しい __マシン - Azure Arc__ と、登録されている SQL Server インスタンスごとに新しい __SQL Server - Azure Arc__ リソースが表示されます。 

![成功したオンボード](./media/join-at-scale/successful-onboard.png)

## <a name="next-steps"></a>次のステップ

- [Azure Policy](/azure/governance/policy/overview) を使用してマシンを管理する方法を確認します。VM の[ゲスト構成](/azure/governance/policy/concepts/guest-configuration)、マシンの報告先が、予期された Log Analytics ワークスペースであることの確認、[VM での Azure Monitor](/azure/azure-monitor/insights/vminsights-enable-policy) を使用した監視の有効化などの方法です。

- [Log Analytics エージェント](/azure/azure-monitor/platform/log-analytics-agent)の詳細を確認します。 マシン上で実行されている OS とワークロードをプロアクティブに監視したい場合、それを Automation Runbook やソリューション (Update Management など) を使用して管理したい場合、または他の Azure サービス ([Azure Security Center](/azure/security-center/security-center-intro) など) を使用したい場合は、Windows 用および Linux 用の Log Analytics エージェントが必要となります。

- [オンデマンドの SQL 評価を使用して、環境の正常性チェックを定期的に行うように SQL Server インスタンスを構成する](assess.md)方法について学習します

- [SQL Server インスタンスの高度なデータ セキュリティを構成する](configure-advanced-data-security.md)方法について学習します