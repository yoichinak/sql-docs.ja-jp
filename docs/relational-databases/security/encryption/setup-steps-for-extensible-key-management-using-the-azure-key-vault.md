---
title: Azure Key Vault を使用した Transparent Data Encryption (TDE) 拡張キー管理を設定する
description: SQL Server コネクタ for Azure Key Vault をインストールして構成します。
ms.custom: seo-lt-2019
ms.date: 10/08/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: Rupp29
ms.author: arupp
ms.openlocfilehash: 4df1fb243b2e811b216b03ec453164ae1a00b1af
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130211"
---
# <a name="set-up-sql-server-tde-extensible-key-management-by-using-azure-key-vault"></a>Azure Key Vault を使用した SQL Server TDE 拡張キー管理を設定する

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

この記事では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタ for Azure Key Vault をインストールして構成します。  
  
## <a name="prerequisites"></a>前提条件

SQL Server インスタンスで Azure Key Vault の使用を開始する前に、次の前提条件を満たしていることを確認してください。  
  
- Azure サブスクリプションが必要です。
  
- [Azure PowerShell バージョン 5.2.0 以降](/powershell/azure/)をインストールしておくこと。  

- Azure Active Directory (Azure AD) インスタンスを作成しておくこと。

- 「[Azure Key Vault を使用する拡張キー管理 (SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)」を読んで、Azure Key Vault を使用した拡張キー管理 (EKM) の保存の原理について熟知していること。  

- 実行中の SQL Server のバージョンに応じた Visual Studio C++ 再頒布可能パッケージのバージョンをインストールしておくこと。
  
  SQL Server のバージョン  | Visual Studio C++ 再頒布可能パッケージのバージョン
  ---------|---------
  2008、2008 R2、2012、2014 | [Visual Studio 2013 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=40784)
  2016 | [Visual Studio 2015 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=48145)

## <a name="step-1-set-up-an-azure-ad-service-principal"></a>手順 1:Azure AD サービス プリンシパルを設定する

SQL Server インスタンスのアクセス権を Azure Key Vault に付与するためには、Azure AD にサービス プリンシパル アカウントが必要です。  
  
1. [Azure portal](https://ms.portal.azure.com/) にサインインして、以下のいずれかを実行します。

    - **[Azure Active Directory]** ボタンを選択します。

      ![[Azure サービス] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-login-portal.png)

    - **[その他のサービス]** を選択してから、 **[すべてのサービス]** ボックスに「**Azure Active Directory**」と入力します。

      ![[All Azure services]\(すべての Azure サービス\) ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-select-aad.png)  

1. 次の手順に従って、Azure Active Directory にアプリケーションを登録します。 (詳しい手順については、[Azure Key Vault のブログ記事](/archive/blogs/kv/azure-key-vault-step-by-step)の「Get an identity for the application (アプリケーションの ID を取得する)」を参照してください。)

    a. Azure Active Directory の **[概要]** ウィンドウで、 **[アプリの登録]** を選択します。

    ![Azure Active Directory の [概要] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-app-register.png)

    b. **[アプリの登録]** ウィンドウで、 **[新規登録]** を選択します。

    ![[アプリの登録] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-registration.png)  

    c. **[アプリケーションの登録]** ウィンドウで、アプリのユーザー向け表示名を入力してから、 **[登録]** を選択します。

    ![[アプリケーションの登録] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-register.png)

    d. 左側のウィンドウで、 **[証明書とシークレット]** を選択してから、 **[新しいクライアント シークレット]** を選択します。

    ![[証明書とシークレット] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-certs-secrets.png)  

    e. **[クライアント シークレットの追加]** で、説明と適切な有効期限を入力してから、 **[追加]** を選択します。

    ![[クライアント シークレットの追加] セクションのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-add-secret.png)  

    f. **[証明書とシークレット]** ウィンドウの **[値]** で、SQL Server で非対称キーを作成するために使用するクライアント シークレットの値の横にある **コピー** ボタンを選択します。

    ![シークレット値のスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-secret.png)  

    g. 左側のウィンドウで **[概要]** を選択してから、 **[アプリケーション (クライアント) ID]** ボックスで、SQL Server で非対称キーを作成するために使用する値をコピーします。

    ![[概要] ウィンドウの [アプリケーション (クライアント) ID] のスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-appid.png)  

## <a name="step-2-create-a-key-vault"></a>手順 2:Key Vault を作成します

キー コンテナーの作成方法を選択します。

## <a name="azure-portal"></a>[Azure Portal](#tab/portal)

### <a name="create-a-key-vault-by-using-the-azure-portal"></a>Azure portal を使用してキー コンテナーを作成する

Azure portal を使用してキー コンテナーを作成し、そのキー コンテナーに Azure AD プリンシパルを追加できます。

1. リソース グループを作成します。

   Azure portal で作成するすべての Azure リソースは、キー コンテナーを格納するために作成するリソース グループに含まれている必要があります。 この例でのリソース名は *ContosoDevRG* です。 すべてのキー コンテナー名はグローバルに一意である必要があるため、リソース グループとキー コンテナーには独自の名前を選択します。

   **[リソースグループを作成します]** ウィンドウの **[プロジェクトの詳細]** で、値を入力してから、 **[確認および作成]** を選択します。

      ![[リソース グループを作成します] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-resource-group.png)  

1. Key Vault を作成します。

    **[キー コンテナーの作成]** ウィンドウで、 **[基本]** タブを選択し、適切な値を入力してから、 **[確認および作成]** を選択します。

    ![[確認および作成] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-key-vault.png)  

1. **[アクセス ポリシー]** ウィンドウで、 **[アクセス ポリシーの追加]** をクリックします。

    ![[アクセス ポリシー] ウィンドウの [アクセス ポリシーの追加] リンクのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-access-policy.png)  

1. **[アクセス ポリシーの追加]** ウィンドウで、次の操作を行います。
  
    a. **[テンプレートからの構成 (省略可能)]** ドロップダウン リストで、 **[キーの管理]** を選択します。

    b. 左側のウィンドウで、 **[キーのアクセス許可]** タブを選択し、 **[取得]** 、 **[一覧]** 、 **[キーの折り返しを解除]** 、および **[キーを折り返す]** チェック ボックスがオンになっていることを確認します。

    c. **[追加]** を選択します。

    ![[アクセス ポリシーの追加] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-access-policy-permission.png)

1. 左側のウィンドウで、 **[プリンシパルの選択]** タブを選択し、次の操作を行います。

    a. **[プリンシパル]** ウィンドウの **[選択]** で、Azure AD アプリケーション名の最初の数文字を入力した後、結果の一覧で追加するアプリケーションを選択します。

    ![[プリンシパル] ウィンドウのアプリケーション検索ボックスのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal.png)  

    b. **[選択]** ボタンを選択して、キー コンテナーにプリンシパルを追加します。

    ![[プリンシパル] ウィンドウの [選択] ボタンのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-principal.png)

    c. 左下の **[追加]** を選択して変更を保存します。

    ![[アクセス ポリシーの追加] ウィンドウの [追加] ボタンのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal-new.png)

1. **[Key Vault]** ウィンドウで、 **[キー]** を選択してキー コンテナー名を入力します。 キーの種類は **[RSA]** を、RSA キー サイズは **[2048]** を使用します。 アクティブ化と有効期限の日付を適宜設定し、 **[有効?]** を **[はい]** に設定します。

   ![[キーの作成] ウィンドウのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-key-vault-key.png)  

1. **[アクセス ポリシー]** ウィンドウで、 **[保存]** をクリックします。
  
   ![[アクセス ポリシーの追加] ウィンドウの [保存] ボタンのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-access-policy.png)  

## <a name="powershell"></a>[PowerShell](#tab/powershell)

### <a name="create-a-key-vault-and-key-by-using-powershell"></a>PowerShell を使用してキー コンテナーとキーを作成する

ここで作成するキー コンテナーとキーは、SQL Server データベース エンジンで暗号化キーを保護するために使用されます。  
  
> [!IMPORTANT]
> キー コンテナーが作成されるサブスクリプションは、Azure AD サービス プリンシパルの作成先と同じ既定の Azure AD インスタンスに存在している必要があります。 SQL Server コネクタのサービス プリンシパルを作成する際に既定のインスタンス以外の Azure AD インスタンスを使用する場合は、キー コンテナーを作成する前に Azure アカウントの既定の Azure AD インスタンスを変更する必要があります。 既定の Azure AD インスタンスを使用するインスタンスに変更する方法については、「[SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)」の「よく寄せられる質問」を参照してください。  
  
1. [Azure PowerShell 5.2.0 以降](/powershell/azure/)をインストールし、次のコマンドを使用してサインインします。  
  
    ```powershell  
    Connect-AzAccount  
    ```  
  
    このステートメントからは次の情報が返されます。  
  
    ```console  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    > 複数のサブスクリプションの中からキー コンテナーで使用する特定のサブスクリプションを指定する場合は、`Get-AzSubscription` を実行してサブスクリプションを表示し、`Select-AzSubscription` を実行して正しいサブスクリプションを選択します。 指定しなかった場合、いずれかのサブスクリプションが PowerShell によって既定で選択されます。  
  
1. リソース グループを作成します。

    PowerShell で作成するすべての Azure リソースは、キー コンテナーを格納するために作成するリソース グループに含まれている必要があります。 この例でのリソース名は *ContosoDevRG* です。 すべてのキー コンテナー名はグローバルに一意である必要があるため、リソース グループとキー コンテナーには独自の名前を選択します。  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
    このステートメントからは次の情報が返されます。  
  
    ```console
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]
    > `-Location` パラメーターについては、コマンド `Get-AzureLocation` を使用して、この例とは別の場所を指定する方法を確認してください。 詳細情報が必要な場合は、「**Get-Help Get-AzureLocation**」と入力してください。  
  
1. Key Vault を作成します。

    `New-AzKeyVault` コマンドレットには、リソース グループ名、Key Vault 名、地理的位置を指定する必要があります。 たとえば、`ContosoEKMKeyVault` という名前のキー コンテナーの場合は、次のコマンドを実行します。  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoEKMKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
    Key Vault の名前を記録しておきます。  
  
    このステートメントからは次の情報が返されます。

    ```console
    Vault Name                       : ContosoEKMKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoEKMKeyVault  
    Vault URI: https://ContosoEKMKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
1. Azure Active Directory サービス プリンシパルが Azure Key Vault にアクセスするための権限を付与します。  
  
    Key Vault の使用を他のユーザーやアプリケーションに承認することができます。  この例では、「[手順 1: Azure AD サービス プリンシパルを設定する](#step-1-set-up-an-azure-ad-service-principal)」で作成した Azure Active Directory サービス プリンシパルを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを承認してみましょう。  
  
    > [!IMPORTANT]
    > Azure AD サービス プリンシパルには、キー コンテナーに対して少なくとも *get*、*list*、*wrapKey*、および *unwrapKey* の権限が必要です。  
  
    次のコマンドに示すように、`ServicePrincipalName` パラメーターには「[手順 1: Azure AD サービス プリンシパルを設定する](#step-1-set-up-an-azure-ad-service-principal)」でコピーした **アプリ (クライアント) ID** を使用します。 `Set-AzKeyVaultAccessPolicy` は、メッセージを伴わずに実行されます。正常に実行されたとしても何も出力されません。  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoEKMKeyVault' `  
      -ServicePrincipalName 9A57CBC5-4C4C-40E2-B517-EA677 `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
    権限を確認するには、 `Get-AzKeyVault` コマンドレットを呼び出します。 このステートメントから返された出力結果の `Access Policies` に、このキー コンテナーにアクセスできるもう 1 つのテナントとして Azure AD アプリケーションの名前が表示されます。  
  
1. キー コンテナーに非対称キーを生成します。 これを行う方法は 2 つあります。既存のキーをインポートする方法と、新しいキーを作成する方法です。  

     > [!NOTE]
     > SQL Server は、2048 ビットの RSA キーのみをサポートします。

### <a name="best-practices"></a>ベスト プラクティス

すばやいキー復旧を確保し、Azure 以外のデータにアクセスできるようにするには、次のベスト プラクティスをお勧めします。

- ローカル ハードウェア セキュリティ モジュール (HSM) デバイス上で暗号化キーをローカルに作成します。 SQL Server によってサポートされるように、必ず非対称の RSA 2048 キーを作成してください。
- 暗号化キーを Azure Key Vault にインポートします。 このプロセスについては、以降のセクションで説明します。
- Azure Key Vault で初めてキーを使用する前に、Azure Key Vault キーのバックアップを実行します。 詳細については、[Backup-AzureKeyVaultKey]() コマンドをご覧ください。
- キーに何らかの変更を加える場合 (ACL の追加、タグの追加、キー属性の追加など) は、必ずもう一度 Azure Key Vault キーのバックアップを実行してください。

  > [!NOTE]
  > キーのバックアップは、任意の場所に保存できるファイルを返す Azure Key Vault キー操作です。

### <a name="types-of-keys"></a>キーの種類

Azure Key Vault では、SQL Server で動作する 2 種類のキーのいずれかを生成できます。 どちらの種類も、非対称の 2048 ビット RSA キーです。  
  
- **ソフトウェアによる保護**:ソフトウェアで処理され、保存状態で暗号化されます。 ソフトウェアで保護されたキーに対する操作は、Azure 仮想マシン上で行われます。 運用環境のデプロイで使用されないキーには、この種類をお勧めします。  

- **HSM による保護**:より強力なセキュリティを確保するために、ハードウェア セキュリティ モジュールによってキーを作成、保護します。 キーのバージョンごとに約 1 米ドルのコストがかかります。  
  
    > [!IMPORTANT]
    > SQL Server コネクタの場合、使用できる文字は a ～ z、A ～ Z、0 ～ 9、ハイフン (-) に限られます。また、26 文字が長さの上限となります。
    > Azure Key Vault に格納されている同じ名前でバージョンが異なるキーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタでは使用できません。  によって使用されている Azure Key Vault キーをローテーションするには、「SQL Server コネクタのメンテナンスとトラブルシューティング」の「A. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのメンテナンス手順」に記載されている「キーのロールオーバー」の手順を参照してください。  

### <a name="import-an-existing-key"></a>既存のキーをインポートする
  
ソフトウェアで保護された 2048 ビットの RSA キーが既にある場合は、そのキーを Azure Key Vault にアップロードできます。 たとえば PFX ファイルが `C:\\` ドライブに *softkey.pfx* という名前で保存されており、これを Azure Key Vault にアップロードする場合は、次のコマンドを実行して、変数 `securepfxpwd` に PFX ファイルのパスワード `12987553` を設定します。  
  
``` powershell  
$securepfxpwd = ConvertTo-SecureString -String '12987553' `  
  -AsPlainText -Force  
```  

次に、PFX ファイルからキーをインポートするために、次のコマンドを実行できます。このファイルは、Key Vault サービスでハードウェア (推奨) によってキーを保護するファイルです。  
  
``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
      -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
      -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
```  

> [!CAUTION]
> 実稼働のシナリオでは、非対称キーをインポートする方法を強くお勧めします。この方法を使用すると、管理者がキーをキー エスクロー システムに預託できるようになるためです。 コンテナー内で非対称キーを作成する方法の場合、秘密キーはコンテナーの外に出ることがないため、エスクローに預託することができません。 重要なデータの保護に使用するキーはエスクローに預託してください。 非対称キーを紛失すると、データが永久的に失われます。  

### <a name="create-a-new-key"></a>新しいキーを作成する

または、新しい暗号化キーを Azure Key Vault に直接作成し、ソフトウェアまたは HSM で保護することもできます。  この例では、`Add-AzureKeyVaultKey` コマンドレットを使用して、ソフトウェアで保護されるキーを作成しましょう。  

``` powershell  
Add-AzureKeyVaultKey -VaultName 'ContosoEKMKeyVault' `  
  -Name 'ContosoRSAKey0' -Destination 'Software'  
```  
  
このステートメントからは次の情報が返されます。  
  
```console
Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
Key        :  {"kid":"https:contosoekmkeyvault.azure.net/keys/  
                ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
VaultName  : contosodevkeyvault  
Name       : contosoRSAKey0  
Version    : <guid>  
Id         : https://contosoekmkeyvault.vault.azure.net:443/  
              keys/ContosoRSAKey0/<guid>  
```  

> [!IMPORTANT]
> キー コンテナーは、同じ名前を持った複数バージョンのキーをサポートしていますが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタで使用するキーをバージョン管理したりロールしたりすることは避けてください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化に使用するキーをロールしたいと管理者が考える場合は、キー コンテナー内に別の名前で新しいキーを作成し、DEK を暗号化するために使用してください。  

---

## <a name="step-3-install-the-ssnoversion-connector"></a>手順 3:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタをインストールする

[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?LinkId=521700)から SQL Server コネクタをダウンロードします。 このダウンロードは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンピューターの管理者が行う必要があります。  

> [!NOTE]
> - バージョン 1.0.0.440 以前の SQL Server コネクタは置き換えられ、運用環境ではサポートされなくなりました。「[SQL Server コネクタのアップグレード](sql-server-connector-maintenance-troubleshooting.md#upgrade-of--connector)」の「[SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)」ページの手順を使用してください。
> - バージョン 1.0.3.0 以降の SQL Server コネクタでは、関連するエラー メッセージがトラブルシューティングのために Windows イベント ログにレポートされます。
> - バージョン 1.0.4.0 以降では、Azure China、Azure Germany、Azure Government などのプライベート Azure クラウドがサポートされています。
> - バージョン 1.0.5.0 では、サムプリントのアルゴリズムについて破壊的変更があります。 1\.0.5.0 にアップグレードした後、データベースの復元でエラーが発生する可能性があります。 詳細については、[サポート技術情報の記事 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0) を参照してください。
> - **バージョン 1.0.5.0 (タイムスタンプ: 2020 年 9 月) 以降の SQL Server コネクタで、メッセージのフィルター処理とネットワーク要求の再試行ロジックがサポートされます。**
  
  ![SQL Server コネクタ インストール ウィザードのスクリーンショット](../../../relational-databases/security/encryption/media/ekm/ekm-connector-install.png)  
  
既定では、コネクタは C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault にインストールされます。 この場所は、セットアップ中に変更することができます。 変更する場合は、次のセクションでスクリプトを調整します。  
  
コネクタ用のインターフェイスはありませんが、正常にインストールされた場合はコンピューターに *Microsoft.AzureKeyVaultService.EKM.dll* がインストールされます。 このアセンブリは、`CREATE CRYPTOGRAPHIC PROVIDER` ステートメントを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に登録する必要がある暗号化 EKM プロバイダー DLL です。  
  
SQL Server コネクタのインストールでは、必要に応じて、SQL Server の暗号化で使用するサンプル スクリプトをダウンロードすることもできます。  
  
SQL Server コネクタのエラー コードの説明、構成設定、またはメンテナンス タスクを確認するには、以下を参照してください。  
  
- [A.SQL Server コネクタのメンテナンス手順](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
- [C.SQL Server コネクタのエラー コードの説明](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
## <a name="step-4-configure-ssnoversion"></a>手順 4:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を構成する  

このセクションの各操作に最低限必要な権限レベルについては、「[B. よく寄せられる質問](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)」を参照してください。  
  
1. *sqlcmd.exe* を実行するか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio を開きます。  
  
1. 次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを実行して、EKM を使用するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を構成します。  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  

    EXEC sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  

    -- Enable EKM provider  
    EXEC sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に EKM プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを登録します。  
  
    Azure Key Vault の EKM プロバイダーである [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを使用して暗号化サービス プロバイダーを作成します。
    この例では、プロバイダー名は `AzureKeyVault_EKM` です。  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  

    > [!NOTE]
    > ファイル パスは 256 文字以内で指定してください。  
  
1. キー コンテナーを使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン用の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資格情報を設定します。  
  
    キー コンテナーのキーを使用して暗号化を実行する各ログインに対し、資格情報を追加する必要があります。 その例を次に示します。  
  
    - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化シナリオをセットアップして管理するためにキー コンテナーを使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理者のログイン。  
  
    - その他、TDE をはじめとする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化機能を有効にする可能性がある [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン。  
  
    資格情報とログインとの間には一対一の対応関係が存在します。 つまり、各ログインには一意の資格情報が必要です。  
  
    この [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを次のように変更します。  
  
    - `IDENTITY` 引数 (`ContosoEKMKeyVault`) を編集し、Azure Key Vault を参照するようにします。
      - *グローバル Azure* を使用している場合は、`IDENTITY` 引数を「[手順 2: キー コンテナーを作成する](#step-2-create-a-key-vault)」で使用した実際の Azure Key Vault の名前に置き換えます。
      - *プライベート Azure クラウド* (Azure Government、Azure China 21Vianet、Azure Germany など) を使用している場合は、`IDENTITY` 引数を「[PowerShell を使用してキー コンテナーとキーを作成する](#create-a-key-vault-and-key-by-using-powershell)」の手順 3 で返された Vault URI に置き換えます。 Vault URI に "https://" は含めないでください。
    - `SECRET` 引数の最初の部分を、「[手順 1: Azure AD サービス プリンシパルを設定する](#step-1-set-up-an-azure-ad-service-principal)」で使用した Azure Active Directory のクライアント ID に置き換えます。 この例の **クライアント ID** は `9A57CBC54C4C40E2B517EA677E0EFA00` です。  
  
      > [!IMPORTANT]
      > アプリ (クライアント) ID のハイフンは必ず削除してください。  
  
    - `SECRET` 引数の 2 番目の部分を、「[手順 1: Azure AD サービス プリンシパルを設定する](#step-1-set-up-an-azure-ad-service-principal)」で使用した **クライアント シークレット** に置き換えます。  この例のクライアント シークレットは `08:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m` です。 完成した `SECRET` 引数は、ハイフンを含まないアルファベットと数字から成る長い文字列になります。  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred
        WITH IDENTITY = 'ContosoEKMKeyVault',                            -- for public Azure
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.azure.cn',          -- for Azure China 21Vianet
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.microsoftazure.de', -- for Azure Germany
               --<----Application (Client) ID ---><--Azure AD app (Client) ID secret-->
        SECRET = '9A57CBC54C4C40E2B517EA677E0EFA0008:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m'
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM;  
  
    -- Add the credential to the SQL Server administrator's domain login
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
    `CREATE CREDENTIAL` 引数に変数を使用し、プログラムでクライアント ID からハイフンを削除する方法の例については、「[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)」をご覧ください。  
  
1. SQL Server インスタンスで Azure Key Vault キーを開きます。  

    新しいキーを作成したか、「[手順 2: キー コンテナーを作成する](#step-2-create-a-key-vault)」の説明に従って非対称キーをインポートしたかにかかわらず、キーを開く必要があります。 次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトに実際のキー名を指定して、キーを開きます。  
  
    - `EKMSampleASYKey` の部分は、実際に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でキーに割り当てる名前に置き換えます。  
    - `ContosoRSAKey0` の部分は、Azure Key Vault 内の実際のキー名に置き換えます。  
  
    ```sql  
    CREATE ASYMMETRIC KEY EKMSampleASYKey
    FROM PROVIDER [AzureKeyVault_EKM]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  

1. 前の手順で作成した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の非対称キーを使用して、新しいログインを作成します。

     ```sql  
    --Create a Login that will associate the asymmetric key to this login
    CREATE LOGIN TDE_Login
    FROM ASYMMETRIC KEY EKMSampleASYKey;
    ```  

1. SQL Server の非対称キーから新しいログインを作成します。 「手順 4: SQL Server を構成する」で設定した資格情報のマッピングを削除して、資格情報を新しいログインにマップできるようにします。

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN [<domain>\<login>]
    DROP CREDENTIAL sysadmin_ekm_cred;
    ```

1. 新しいログインを変更して、EKM 資格情報を新しいログインにマップします。

     ```sql  
    --Now add the credential mapping to the new Login
    ALTER LOGIN TDE_Login
    ADD CREDENTIAL sysadmin_ekm_cred;
    ```  

1. Azure Key Vault キーを使用して暗号化されるテスト データベースを作成します。

     ```sql
    --Create a test database that will be encrypted with the Azure key vault key
    CREATE DATABASE TestTDE
    ```  

1. 非対称キー (EKMSampleASYKey) を使用してデータベース暗号化キーを作成します。

    ```sql  
    --Create an ENCRYPTION KEY using the ASYMMETRIC KEY (EKMSampleASYKey)
    CREATE DATABASE ENCRYPTION KEY
    WITH ALGORITHM = AES_256
    ENCRYPTION BY SERVER ASYMMETRIC KEY EKMSampleASYKey;
    ```
  
1. テスト データベースを暗号化します。 ENCRYPTION ON を設定して TDE を有効にします。

     ```sql  
    --Enable TDE by setting ENCRYPTION ON
    ALTER DATABASE TestTDE
    SET ENCRYPTION ON;  
     ```  

1. テスト オブジェクトをクリーンアップします。 このテスト スクリプトで作成されたすべてのオブジェクトを削除します。

    ```sql  
    -- CLEAN UP
    USE Master
    ALTER DATABASE [TestTDE] SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    DROP DATABASE [TestTDE]

    ALTER LOGIN [TDE_Login] DROP CREDENTIAL [sysadmin_ekm_cred]
    DROP LOGIN [TDE_Login]

    DROP CREDENTIAL [sysadmin_ekm_cred]  

    USE MASTER
    DROP ASYMMETRIC KEY [EKMSampleASYKey]
    DROP CRYPTOGRAPHIC PROVIDER [AzureKeyVault_EKM]
    ```  

サンプル スクリプトについては、「[SQL Server Transparent Data Encryption and Extensible Key Management with Azure Key Vault (Azure Key Vault を使用した SQL Server Transparent Data Encryption と拡張キー管理)](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549)」のブログをご覧ください。

## <a name="next-steps"></a>次のステップ  
  
以上で基本的な構成は完了です。「[SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)」を参照してください。
  
## <a name="see-also"></a>関連項目  

- [Azure Key Vault を使用する TDE 拡張キー管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)
- [SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
