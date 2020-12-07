---
title: SQL Server コネクタのメンテナンスとトラブルシューティング
description: SQL Server コネクタのメンテナンス手順と一般的なトラブルシューティング手順について説明します。
ms.custom: seo-lt-2019
ms.date: 10/08/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 4c8a74d33e75ab19b283f3b9d1bfdaf47dc69240
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869264"
---
# <a name="sql-server-connector-maintenance--troubleshooting"></a>SQL Server コネクタのメンテナンスとトラブルシューティング

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタに関する補足情報を取り上げます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタの詳細については、「[Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)」、「[Azure Key Vault を使用した拡張キー管理のセットアップ手順](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)」、「[SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)」を参照してください。  
  
##  <a name="a-maintenance-instructions-for-ssnoversion-connector"></a><a name="AppendixA"></a> A. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのメンテナンス手順  
  
### <a name="key-rollover"></a>キーのロールオーバー  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを使用する場合、キー名に使用できる文字は、"a ～ z"、"A ～ Z"、"0 ～9"、"-" に限られます。また、26 文字が長さの上限となります。
> Azure Key Vault に格納されている同じ名前でバージョンが異なるキーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタでは使用できません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で使用されている Azure Key Vault のキーをローテーションするには、別の名前の新しいキーを作成する必要があります。  
  
 通常、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化のサーバー非対称キーは 1 年から 2 年おきにバージョン管理する必要があります。 重要なのは、Key Vault ではキーをバージョン管理できますが、顧客がこの機能を使用してバージョン管理を実装してはならない点です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタは、Key Vault でのキーのバージョンの変更に対応できません。 キーのバージョン管理を実装するには、Key Vault に新しいキーを作成してから、[!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] でデータ暗号化キーを再暗号化します。  
  
 TDE では、次の方法でこれを実現します。  
  
- **PowerShell を使用する場合:** 新しい非対称キーを (現在の TDE 非対称キーとは異なる名前で) Key Vault に作成します。  
  
    ```powershell  
    Add-AzKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
- **[!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] または sqlcmd.exe を使用する場合:** 以下のステートメントを使用します。手順 3 (セクション 3) を参照してください。  
  
     新しい非対称キーをインポートします。  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]
    FROM PROVIDER [EKM]
    WITH PROVIDER_KEY_NAME = 'Key2',
    CREATION_DISPOSITION = OPEN_EXISTING
    GO  
    ```  
  
     新しい非対称キーに関連付けられる新しいログインを作成します (TDE の手順で説明しています)。  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     ログインにマップする新しい資格情報を作成します。  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789='
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     データベース暗号化キーを再暗号化するデータベースを選択します。  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     データベース暗号化キーを再暗号化します。  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-ssnoversion-connector"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのアップグレード  

1\.0.0.440 以前のバージョンは置き換えられ、実稼働環境ではサポートされなくなりました。 バージョン 1.0.1.0 以降は実稼働環境でサポートされます。 以下の手順を使用して、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=45344)で利用可能な最新バージョンにアップグレードしてください。

### <a name="upgrade"></a>アップグレード

1. SQL Server 構成マネージャーを使用して、SQL Server サービスを停止します
1. [コントロール パネル] > [プログラム] > [プログラムと機能] を使用して、古いバージョンをアンインストールします
    1. アプリケーション名: SQL Server コネクタ for Microsoft Azure Key Vault
    1. バージョン:15.0.300.96 (またはそれ以前)
    1. DLL ファイルの日付: 01/30/2018 3:00 PM (またはそれ以前)
1. 新しい SQL Server コネクタ for Microsoft Azure Key Vault をインストール (アップグレード) します
    1. バージョン:15.0.2000.367
    1. DLL ファイルの日付: 09/11/2020 ‏‎5:17 AM
1. SQL Server サービスを開始します
1. 暗号化された DB がアクセス可能であることをテストします

### <a name="rollback"></a>ロールバック

1. SQL Server 構成マネージャーを使用して、SQL Server サービスを停止します

1. [コントロール パネル] > [プログラム] > [プログラムと機能] を使用して、新しいバージョンをアンインストールします
    1. アプリケーション名: SQL Server コネクタ for Microsoft Azure Key Vault
    1. バージョン:15.0.2000.367
    1. DLL ファイルの日付: 09/11/2020 ‏‎5:17 AM

1. 古いバージョンの SQL Server コネクタ for Microsoft Azure Key Vault をインストールします
    1. バージョン:15.0.300.96
    1. DLL ファイルの日付: 01/30/2018 3:00 PM
1. SQL Server サービスを開始します

1. TDE が使用されているデータベースにアクセスできることを確認します。  
  
1. 更新が正常に行われたことを確認したら、古い [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタ フォルダーは削除してかまいません (手順 3. で、アンインストールの代わりに名前を変更した場合)。

### <a name="older-versions-of-the-sql-server-connector"></a>以前のバージョンの SQL Server コネクタ
  
以前のバージョンの SQL Server コネクタへのディープ リンク

- 電流: [1.0.5.0 (バージョン 15.0.2000.367) – ファイルの日付: 2020 年 9 月 11 日](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/1033_15.0.2000.367/SQLServerConnectorforMicrosoftAzureKeyVault.msi)
- [1.0.5.0 (バージョン 15.0.300.96) – ファイル日付: 2018 年 1 月 30 日](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/ENU/SQLServerConnectorforMicrosoftAzureKeyVault.msi)
- [1.0.4.0: (バージョン 13.0.811.168)](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/SQLServerConnectorforMicrosoftAzureKeyVault.msi)

### <a name="rolling-the-ssnoversion-service-principal"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service プリンシパルのローリング

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、Azure Active Directory で作成されたサービス プリンシパルを資格情報に使用して、Key Vault にアクセスします。 サービス プリンシパルにはクライアント ID と認証キーが含まれます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の資格情報は **VaultName**、 **クライアント ID**、 **認証キー**で設定されます。 **認証キー**は一定期間 (1 年または 2 年) 有効です。 期限が切れる前に Azure AD でサービス プリンシパルの新しいキーを生成する必要があります。 その後、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で資格情報を変更する必要があります。 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] では現在のセッションで資格情報のキャッシュを保持するため、資格情報に変更があった場合は [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] を再起動する必要があります。  
  
### <a name="key-backup-and-recovery"></a>キーのバックアップと回復

Key Vault は定期的にバックアップする必要があります。 資格情報コンテナー内の非対称キーが失われた場合は、バックアップから復元できます。 このキーは、以前と同じ名前で復元する必要があります。復元は Restore PowerShell コマンドで行います (以下の手順を参照)。  
資格情報コンテナーが失なわれた場合は、資格情報コンテナーを再作成し、非対称キーは以前と同じ名前で資格情報コンテナーに復元する必要があります。 資格情報コンテナーの名前は、以前とは別の名前にできます (同じでもかまいません)。 新しい資格情報コンテナーに対するアクセス許可を設定し、SQL Server 暗号化のシナリオに必要なアクセス権を SQL Server サービス プリンシパルに付与します。その後、新しい資格情報コンテナー名が反映されるように SQL Server 資格情報を調整します。

手順の概要を以下に示します。  
  
- コンテナー キーをバックアップします (Backup-AzureKeyVaultKey PowerShell コマンドレットを使用)。  
- 資格情報コンテナーの障害の場合は、同じ地理的リージョンに新しい資格情報コンテナーを作成します。 資格情報コンテナーを作成するユーザーは、SQL Server のサービス プリンシパルの設定と同じ既定のディレクトリに存在している必要があります。  
- Restore-AzureKeyVaultKey PowerShell コマンドレットを使用して、新しい資格情報コンテナーにキーを復元します。これにより、以前と同じ名前を使用してキーが復元されます。 既に同じ名前のキーが存在する場合、復元は失敗します。  
- 新しい資格情報コンテナーを使用するための権限を SQL Server サービス プリンシパルに付与します。
- 必要に応じて、新しい資格情報コンテナー名を反映するように、データベース エンジンが使用する SQL Server 資格情報を変更します。  
  
キーのバックアップは、クラウドの地理的領域または国が一致していれば、異なる Azure リージョン間で復元することができます:米国、カナダ、日本、オーストラリア、インド、APAC、ヨーロッパ、ブラジル、中国、米国政府、ドイツ。  
  
##  <a name="b-frequently-asked-questions"></a><a name="AppendixB"></a> B. よく寄せられる質問

### <a name="on-azure-key-vault"></a>Azure Key Vault について
  
**Azure Key Vault との間でキーの処理はどのように行われますか。**  
 Key Vault 内の非対称キーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化キーを保護するために使用されます。 資格情報コンテナーから出て行くのは非対称キーの公開部分だけで、秘密の部分がコンテナーからエクスポートされることはありません。 非対称キーを使用するすべての暗号化操作は、Azure Key Vault サービス内で実行され、このサービスのセキュリティによって保護されます。  
  
 **キーの URI とは何ですか。**  
 Azure Key Vault 内のすべてのキーに、Uniform Resource Identifier (URI) が割り当てられます。アプリケーションからこの URI を使用してキーを参照できます。 常に最新のバージョンを取得するには `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` の形式、特定のバージョンを取得するには `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` の形式を使用します。  
  
### <a name="on-configuring-ssnoversion"></a>構成について [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**SQL Server コネクタがアクセスする必要のあるエンドポイントは何ですか。**
コネクタは 2 つのエンドポイントと通信します。これらは許可されている必要があります。 これらの他のサービスへの送信通信に必要な唯一のポートは、Https 用の 443 です。

- login.microsoftonline.com/*:443
- *.vault.azure.net/* :443

**HTTP(S) プロキシ サーバー経由で Azure Key Vault に接続するにはどうすればよいでしょうか。**
このコネクタでは、Internet Explorer のプロキシ構成設定が使用されます。 これらの設定は[グループ ポリシー](/archive/blogs/askie/how-to-configure-proxy-settings-for-ie10-and-ie11-as-iem-is-not-available)またはレジストリから制御できますが、システム全体の設定ではなく、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを実行しているサービス アカウントを対象にする必要があることに注意することが重要です。 データベース管理者が Internet Explorer の設定を表示または編集する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エンジンではなく、そのデータベース管理者のアカウントにのみ影響します。 サービス アカウントを利用して対話方式でサーバーにログオンすることは推奨されておらず、セキュリティで保護されている多くの環境でブロックされます。 構成済みのプロキシ設定を変更する場合、コネクタでキー コンテナーへの接続が最初に試行されたときにキャッシュされるため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを再起動しないと変更が適用されないことがあります。

**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の各構成手順で最低限必要な権限レベルを教えてください。**  
 すべての構成手順は sysadmin 固定サーバー ロールのメンバーとして実行することもできますが、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では使用する権限を最小限に抑えることをお勧めします。 次の一覧に、各操作の最小アクセス許可レベルを定義します。  
  
- 暗号化サービス プロバイダーを作成するには、 `CONTROL SERVER` 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
- 構成オプションを変更して `RECONFIGURE` ステートメントを実行するには、 `ALTER SETTINGS` サーバー レベル権限が与えられている必要があります。 `ALTER SETTINGS` 権限は、sysadmin 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
- 資格情報を作成するには、 `ALTER ANY CREDENTIAL` 権限が必要です。  
  
- ログインに資格情報を追加するには、 `ALTER ANY LOGIN` 権限が必要です。  
  
- 非対称キーを作成するには、 `CREATE ASYMMETRIC KEY` 権限が必要です。  

**[!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] コネクタ用に作成したサービス プリンシパルと同じサブスクリプションおよび Active Directory で Key Vault が作成されるように、既定の Active Directory を変更するにはどうすればよいですか。**

![aad change default directory helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Azure クラシック ポータルに移動: [https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. 左側のメニューで、 **[設定]** を選択します。
3. 現在使用している Azure サブスクリプションを選択し、画面の下部にあるコマンドの **[ディレクトリの編集]** をクリックします。
4. ポップアップ ウィンドウで、 **[ディレクトリ]** ドロップダウンを使用して、使用する Active Directory を選択します。 これで既定のディレクトリになります。
5. 新しく選択した Active Directory のグローバル管理者であることを確認します。 グローバル管理者でない場合、ディレクトリを切り替えると、管理権限が失われる可能性があります。
6. ポップアップ ウィンドウが閉じてから、自分のどのサブスクリプションも表示されない場合は、画面右上のメニューにある **[サブスクリプション]** フィルターで **[ディレクトリでフィルター]** フィルターを更新し、新しく更新された Active Directory を使用してサブスクリプションを表示する必要がある場合があります。

    > [!NOTE] 
    > Azure サブスクリプションの既定のディレクトリを実際に変更する権限がない場合があります。 この場合は、既定のディレクトリ内に AAD サービス プリンシパルを作成し、後で使用する Azure Key Vault と同じディレクトリ内に存在するようにします。

Active Directory の詳細については、「 [Azure サブスクリプションを Azure Active Directory に関連付ける方法](/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)」を参照してください。
  
##  <a name="c-error-code-explanations-for-ssnoversion-connector"></a><a name="AppendixC"></a> C. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのエラー コードの説明

**プロバイダーのエラー コード:**  
  
エラー コード  |Symbol  |説明
---------|---------|---------  
0 | scp_err_Success | 操作は成功しました。
1 | scp_err_Failure | 操作は失敗しました。
2 | scp_err_InsufficientBuffer | バッファーに割り当てるメモリ量を増やすようエンジンに指示が出されます。
3 | scp_err_NotSupported | この操作はサポートされていません。 たとえば、指定されたキーの種類やアルゴリズムは、EKM プロバイダーでサポートされていません。
4 | scp_err_NotFound | 指定されたキーまたはアルゴリズムを EKM プロバイダーが検出できませんでした。
5 | scp_err_AuthFailure | EKM プロバイダーでの認証に失敗しました。
6 | scp_err_InvalidArgument | 指定された引数は無効です。
7 | scp_err_ProviderError | 特定できないエラーが EKM プロバイダーで発生したことを SQL エンジンが検出しました。
401 | acquireToken | 要求に対し、サーバーから 401 応答が返されました。 クライアント ID とシークレットが正しいことと、資格情報の文字列が AAD クライアント ID とシークレットのハイフンなしの連結になっていることを確認してください。
404 | getKeyByName | キー名が見つからなかったために、サーバーが 404 で応答しました。 キー名が Key Vault に存在していることを確認してください。
2049 | scp_err_KeyNameDoesNotFitThumbprint | キー名が長すぎて、SQL エンジンの拇印に収まりません。 キー名が 26 文字を超えないようにしてください。
2050 | scp_err_PasswordTooShort | AAD クライアント ID とシークレットを連結したシークレット文字列が 32 文字未満です。
2051 | scp_err_OutOfMemory | SQL エンジンのメモリ不足から、EKM プロバイダーに必要なメモリを割り当てることができませんでした。
2052 | scp_err_ConvertKeyNameToThumbprint | キー名を拇印に変換できませんでした。
2053 | scp_err_ConvertThumbprintToKeyName|  拇印をキー名に変換できませんでした。
3000 | ErrorSuccess | AKV 操作は成功しました。
3001 | ErrorUnknown | 特定できないエラーが発生して AKV 操作に失敗しました。
3002 | ErrorHttpCreateHttpClientOutOfMemory | メモリ不足により、AKV 操作に使用する HttpClient を作成できません。
3003 | ErrorHttpOpenSession | ネットワーク エラーのため、HTTP セッションを開くことができません。
3004 | ErrorHttpConnectSession | ネットワーク エラーのため、HTTP セッションを接続できません。
3005 | ErrorHttpAttemptConnect | ネットワーク エラーのため、接続を試行できません。
3006 | ErrorHttpOpenRequest | ネットワーク エラーのため、要求を開くことができません。
3007 | ErrorHttpAddRequestHeader | 要求ヘッダーを追加できません。
3008 | ErrorHttpSendRequest | ネットワーク エラーのため、要求を送信できません。
3009 | ErrorHttpGetResponseCode | ネットワーク エラーのため、応答コードを取得できません。
3010 | ErrorHttpResponseCodeUnauthorized | 要求に対し、サーバーから 401 応答が返されました。
3011 | ErrorHttpResponseCodeThrottled | サーバーによって要求が調整されています。
3012 | ErrorHttpResponseCodeClientError | コネクタから送信された要求が無効です。 これは通常、キー名が無効であるか、キー名に無効な文字が含まれることを意味します。
3013 | ErrorHttpResponseCodeServerError | サーバーから 500 ～ 600 の応答コードが返されました。
3014 | ErrorHttpQueryHeader | 応答ヘッダーを照会できません。
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | メモリ不足のため、応答ヘッダーをコピーできません。
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | バッファーの再割り当て時にメモリ不足が発生したため、応答ヘッダーを照会できません。
3017 | ErrorHttpQueryHeaderNotFound | クエリ ヘッダーが応答に見つかりません。
3018 | ErrorHttpQueryHeaderUpdateBufferLength | 応答ヘッダーを照会しているときにバッファーの長さを更新することはできません。
3019 | ErrorHttpReadData | ネットワーク エラーのため、応答データを読み取ることができません。
3076 | ErrorHttpResourceNotFound | キー名が見つからなかったために、サーバーが 404 で応答しました。 キー名がコンテナーに存在していることを確認してください。
3077 | ErrorHttpOperationForbidden | ユーザーに操作を実行するための適切な権限がないため、サーバーが 403 で応答しました。 指定された操作に対する権限があることを確認してください。 コネクタが正常に機能するには、少なくとも "get、list、wrapKey、unwrapKey" 権限が必要です。
3100 | ErrorHttpCreateHttpClientOutOfMemory               | メモリ不足により、AKV 操作に使用する HttpClient を作成できません。
3101 | ErrorHttpOpenSession                               | ネットワーク エラーのため、HTTP セッションを開くことができません。
3102 | ErrorHttpConnectSession                            | ネットワーク エラーのため、HTTP セッションを接続できません。
3103 | ErrorHttpAttemptConnect                            | ネットワーク エラーのため、接続を試行できません。
3104 | ErrorHttpOpenRequest                               | ネットワーク エラーのため、要求を開くことができません。
3105 | ErrorHttpAddRequestHeader                          | 要求ヘッダーを追加できません。
3106 | ErrorHttpSendRequest                               | ネットワーク エラーのため、要求を送信できません。
3107 | ErrorHttpGetResponseCode                           | ネットワーク エラーのため、応答コードを取得できません。
3108 | ErrorHttpResponseCodeUnauthorized                  | 要求に対し、サーバーから 401 応答が返されました。 クライアント ID とシークレットが正しいことと、資格情報の文字列が AAD クライアント ID とシークレットのハイフンなしの連結になっていることを確認してください。
3109 | ErrorHttpResponseCodeThrottled                     | サーバーによって要求が調整されています。
3110 | ErrorHttpResponseCodeClientError                    | 要求が無効です。 これは通常、キー名が無効であるか、キー名に無効な文字が含まれることを意味します。
3111 | ErrorHttpResponseCodeServerError                   | サーバーから 500 ～ 600 の応答コードが返されました。
3112 | ErrorHttpResourceNotFound                          | キー名が見つからなかったために、サーバーが 404 で応答しました。 キー名が Key Vault に存在していることを確認してください。
3113 | ErrorHttpOperationForbidden                         | ユーザーに操作を実行するための適切な権限がないため、サーバーが 403 で応答しました。 指定された操作の権限があることを確認してください。 "get、wrapKey、unwrapKey" 以上の権限が必要です。
3114 | ErrorHttpQueryHeader                               | 応答ヘッダーを照会できません。
3115 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader          | メモリ不足のため、応答ヘッダーをコピーできません。
3116 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer       | バッファーの再割り当て時にメモリ不足が発生したため、応答ヘッダーを照会できません。
3117 | ErrorHttpQueryHeaderNotFound                       | クエリ ヘッダーが応答に見つかりません。
3118 | ErrorHttpQueryHeaderUpdateBufferLength             | 応答ヘッダーを照会しているときにバッファーの長さを更新することはできません。
3119 | ErrorHttpReadData                                  | ネットワーク エラーのため、応答データを読み取ることができません。
3120 | ErrorHttpGetResponseOutOfMemoryCreateTempBuffer    | 一時バッファーの作成時にメモリ不足が発生したため、応答本文を取得できません。
3121 | ErrorHttpGetResponseOutOfMemoryGetResultString     | 結果文字列の取得時にメモリ不足が発生したため、応答本文を取得できません。
3122 | ErrorHttpGetResponseOutOfMemoryAppendResponse      | 応答の追加時にメモリ不足が発生したため、応答本文を取得できません。
3200 | ErrorGetAADValuesOutOfMemoryConcatPath | パスの連結時にメモリ不足が発生したため、Azure Active Directory チャレンジ ヘッダー値を取得できません。
3201 | ErrorGetAADDomainUrlStartPosition | Azure Active Directory ドメイン URL の開始位置が見つかりません。応答チャレンジ ヘッダーの形式が不正です。
3202 | ErrorGetAADDomainUrlStopPosition | Azure Active Directory ドメイン URL の終了位置が見つかりません。応答チャレンジ ヘッダーの形式が不正です。
3203 | ErrorGetAADDomainUrlMalformatted | Azure Active Directory 応答チャレンジ ヘッダーの形式が不正です。AAD ドメイン URL が含まれていません。
3204 | ErrorGetAADDomainUrlOutOfMemoryAlloc | Azure Active Directory ドメイン URL のバッファー割り当て時にメモリ不足が発生しました。
3205 | ErrorGetAADTenantIdOutOfMemoryAlloc | Azure Active Directory tenantId のバッファー割り当て時にメモリ不足が発生しました。
3206 | ErrorGetAKVResourceUrlStartPosition | Azure Key Vault リソース URL の開始位置が見つかりません。応答チャレンジ ヘッダーの形式が不正です。
3207 | ErrorGetAKVResourceUrlStopPosition | Azure Key Vault リソース URL の終了位置が見つかりません。応答チャレンジ ヘッダーの形式が不正です。
3208 | ErrorGetAKVResourceUrlOutOfMemoryAlloc | Azure Key Vault リソース URL のバッファー割り当て時にメモリ不足が発生しました。
3300 | ErrorGetTokenOutOfMemoryConcatPath | 要求パスの連結時にメモリ不足が発生したため、トークンを取得できません。
3301 | ErrorGetTokenOutOfMemoryConcatBody | 応答本文の連結時にメモリ不足が発生したため、トークンを取得できません。
3302 | ErrorGetTokenOutOfMemoryConvertResponseString | 応答文字列の変換時にメモリ不足が発生したため、トークンを取得できません。
3303 | ErrorGetTokenBadCredentials | 資格情報が間違っているため、トークンを取得できません。 資格情報文字列または証明書が有効であることを確認してください。
3304 | ErrorGetTokenFailedToGetToken | 資格情報は正しいですが、操作で有効なトークンを取得できませんでした。
3305 | ErrorGetTokenRejected | トークンは有効ですが、サーバーによって拒否されています。
3306 | ErrorGetTokenNotFound | 応答にトークンが見つかりません。
3307 | ErrorGetTokenJsonParser | サーバーの JSON 応答を解析できません。
3308 | ErrorGetTokenExtractToken | JSON 応答からトークンを抽出できません。
3400 | ErrorGetKeyByNameOutOfMemoryConvertResponseString | 応答文字列の変換時にメモリ不足が発生したため、名前でキーを取得できません。
3401 | ErrorGetKeyByNameOutOfMemoryConcatPath | パスの連結時にメモリ不足が発生したため、名前でキーを取得できません。
3402 | ErrorGetKeyByNameOutOfMemoryConcatHeader | ヘッダーの連結時にメモリ不足が発生したため、名前でキーを取得できません。
3403 | ErrorGetKeyByNameNoResponse | サーバーから応答がないため、名前でキーを取得できません。
3404 | ErrorGetKeyByNameJsonParser | JSON 応答の解析に失敗したため、名前でキーを取得できません。
3405 | ErrorGetKeyByNameExtractKeyNode | 応答からキー ノードを抽出できなかったため、名前でキーを取得できません。
3406 | ErrorGetKeyByNameExtractKeyId | 応答からキー ID を抽出できなかったため、名前でキーを取得できません。
3407 | ErrorGetKeyByNameExtractKeyType | 応答からキーの種類を抽出できなかったため、名前でキーを取得できません。
3408 | ErrorGetKeyByNameExtractKeyN | 応答からキー N を抽出できなかったため、名前でキーを取得できません。
3409 | ErrorGetKeyByNameBase64DecodeN | N の Base64 デコードに失敗したため、名前でキーを取得できません。
3410 | ErrorGetKeyByNameExtractKeyE | 応答からキー E を抽出できなかったため、名前でキーを取得できません。
3411 | ErrorGetKeyByNameBase64DecodeE | E の Base64 デコードに失敗したため、名前でキーを取得できません。
3412 | ErrorGetKeyByNameExtractKeyUri | 応答からキー URI を抽出できません。
3500 | ErrorBackupKeyOutOfMemoryConvertResponseString | 応答文字列の変換時にメモリ不足が発生したため、キーをバックアップできません。
3501 | ErrorBackupKeyOutOfMemoryConcatPath | パスの連結時にメモリ不足が発生したため、キーをバックアップできません。
3502 | ErrorBackupKeyOutOfMemoryConcatHeader | 要求ヘッダーの連結時にメモリ不足が発生したため、キーをバックアップできません。
3503 | ErrorBackupKeyNoResponse | サーバーから応答がないため、キーをバックアップできません。
3504 | ErrorBackupKeyJsonParser | JSON 応答の解析に失敗したため、キーをバックアップできません。
3505 | ErrorBackupKeyExtractValue | JSON 応答から値を抽出できなかったため、キーをバックアップできません。
3506 | ErrorBackupKeyBase64DecodeValue | 値フィールドの Base64 デコードに失敗したため、キーをバックアップできません。
3600 | ErrorWrapKeyOutOfMemoryConvertResponseString | 応答文字列の変換時にメモリ不足が発生したため、キーの折り返しができません。
3601 | ErrorWrapKeyOutOfMemoryConcatPath | パスの連結時にメモリ不足が発生したため、キーの折り返しができません。
3602 | ErrorWrapKeyOutOfMemoryConcatHeader | ヘッダーの連結時にメモリ不足が発生したため、キーの折り返しができません。
3603 | ErrorWrapKeyOutOfMemoryConcatBody | 本文の連結時にメモリ不足が発生したため、キーの折り返しができません。
3604 | ErrorWrapKeyOutOfMemoryConvertEncodedBody | エンコードされた本文の変換時にメモリ不足が発生したため、キーの折り返しができません。
3605 | ErrorWrapKeyBase64EncodeKey | キーを Base64 エンコードできなかったため、キーの折り返しができません。
3606 | ErrorWrapKeyBase64DecodeValue | 応答値の Base64 デコードに失敗したため、キーの折り返しができません。
3607 | ErrorWrapKeyJsonParser | JSON 応答の解析に失敗したため、キーの折り返しができません。
3608 | ErrorWrapKeyExtractValue | 応答から値を抽出できなかったため、キーの折り返しができません。
3609 | ErrorWrapKeyNoResponse | サーバーから応答がないため、キーの折り返しができません。
3700 | ErrorUnwrapKeyOutOfMemoryConvertResponseString | 応答文字列の変換時にメモリ不足が発生したため、キーの折り返しを解除できません。
3701 | ErrorUnwrapKeyOutOfMemoryConcatPath | パスの連結時にメモリ不足が発生したため、キーの折り返しを解除できません。
3702 | ErrorUnwrapKeyOutOfMemoryConcatHeader | ヘッダーの連結時にメモリ不足が発生したため、キーの折り返しを解除できません。
3703 | ErrorUnwrapKeyOutOfMemoryConcatBody | 本文の連結時にメモリ不足が発生したため、キーの折り返しを解除できません。
3704 | ErrorUnwrapKeyOutOfMemoryConvertEncodedBody | エンコードされた本文の変換時にメモリ不足が発生したため、キーの折り返しを解除できません。
3705 | ErrorUnwrapKeyBase64EncodeKey | キーを Base64 エンコードできなかったため、キーの折り返しを解除できません。
3706 | ErrorUnwrapKeyBase64DecodeValue | 応答値の Base64 デコードに失敗したため、キーの折り返しを解除できません。
3707 | ErrorUnwrapKeyJsonParser | 応答から値を抽出できなかったため、キーの折り返しを解除できません。
3708 | ErrorUnwrapKeyExtractValue | 応答から値を抽出できなかったため、キーの折り返しを解除できません。
3709 | ErrorUnwrapKeyNoResponse | サーバーから応答がないため、キーの折り返しを解除できません。
3800 | ErrorSecretAuthParamsGetRequestBody | AAD clientId とシークレットを使用して要求本文を作成するときにエラーが発生しました。
3801 | ErrorJWTTokenCreateHeader | AAD での認証用に JWT トークン ヘッダーを作成するときにエラーが発生しました。
3802 | ErrorJWTTokenCreatePayloadGUID | AAD での認証用に JWT トークン ペイロードの GUID を作成するときにエラーが発生しました。
3803 | ErrorJWTTokenCreatePayload | AAD での認証用に JWT トークン ペイロードを作成するときにエラーが発生しました。
3804 | ErrorJWTTokenCreateSignature | AAD での認証用に JWT トークン署名を作成するときにエラーが発生しました。
3805 | ErrorJWTTokenSignatureHashAlg | AAD での認証用に SHA 256 ハッシュ アルゴリズムを取得するときにエラーが発生しました。
3806 | ErrorJWTTokenSignatureHash | JWT トークンによる AAD での認証用に SHA 256 ハッシュを作成するときにエラーが発生しました。
3807 | ErrorJWTTokenSignatureSignHash | AAD での認証用に JWT トークン ハッシュに署名するときにエラーが発生しました。
3808 | ErrorJWTTokenCreateToken | AAD での認証用に JWT トークンを作成するときにエラーが発生しました。
3809 | ErrorPfxCertAuthParamsImportPfx | AAD での認証用に Pfx 証明書をインポートするときにエラーが発生しました。
3810 | ErrorPfxCertAuthParamsGetThumbprint | AAD での認証用に Pfx 証明書から拇印を取得するときにエラーが発生しました。
3811 | ErrorPfxCertAuthParamsGetPrivateKey | AAD での認証用に Pfx 証明書から秘密キーを取得するときにエラーが発生しました。
3812 | ErrorPfxCertAuthParamsSignAlg | Pfx 証明書による AAD での認証用に RSA 署名アルゴリズムを取得するときにエラーが発生しました。
3813 | ErrorPfxCertAuthParamsImportForSign | AAD での認証用に RSA 署名用の Pfx 秘密キーをインポートするときにエラーが発生しました。
3814 | ErrorPfxCertAuthParamsCreateRequestBody | AAD での認証用に Pfx 証明書から要求本文を作成するときにエラーが発生しました。
3815 | ErrorPEMCertAuthParamsGetThumbprint | AAD での認証用に拇印を Base64 デコードするときにエラーが発生しました。
3816 | ErrorPEMCertAuthParamsGetPrivateKey | AAD での認証用に PEM から RSA 秘密キーを取得するときにエラーが発生しました。
3817 | ErrorPEMCertAuthParamsSignAlg | PEM 秘密キーによる AAD での認証用に RSA 署名アルゴリズムを取得するときにエラーが発生しました。
3818 | ErrorPEMCertAuthParamsImportForSign | AAD での認証用に RSA 署名用の PEM 秘密キーをインポートするときにエラーが発生しました。
3819 | ErrorPEMCertAuthParamsCreateRequestBody | AAD での認証用に PEM 秘密キーから要求本文を作成するときにエラーが発生しました。
3820 | ErrorLegacyPrivateKeyAuthParamsSignAlg | Legacy 秘密キーによる AAD での認証用に RSA 署名アルゴリズムを取得するときにエラーが発生しました。
3821 | ErrorLegacyPrivateKeyAuthParamsImportForSign | AAD での認証用に RSA 署名用の Legacy 秘密キーをインポートするときにエラーが発生しました。
3822 | ErrorLegacyPrivateKeyAuthParamsCreateRequestBody        | AAD での認証用に Legacy 秘密キーから要求本文を作成するときにエラーが発生しました。
3900 | ErrorAKVDoesNotExist | インターネット名未解決エラー。 これは通常、Azure Key Vault が削除されていることを示します。
4000 | ErrorCreateKeyVaultRetryManagerOutOfMemory | メモリ不足のため、AKV 操作に使用する RetryManager を作成できません。

この表に記載されていないエラー コードについて、その他の考えられる原因を以下に示します。
  
- インターネットにアクセスできない可能性があるか、Azure Key Vault にアクセスできません。 インターネット接続を確認してください。  
  
- Azure Key Vault サービスがダウンしている可能性があります。 後でもう一度試してください。  
  
- 非対称キーが Azure Key Vault または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]から削除されている可能性があります。 キーを復元してください。  
  
- "ライブラリを読み込めません" というエラーが表示された場合は、実行中の SQL Server のバージョンに基づいて、適切なバージョンの Visual Studio C++ 再頒布可能パッケージがインストールされていることを確認してください。 次の表に、Microsoft ダウンロード センターからインストールするバージョンを示します。

Windows イベント ログでは、SQL Server コネクタに関連付けられているエラーもログに記録されます。これは、他の文脈で、エラーが実際に発生している理由を特定するのに役立つことがあります。 Windows アプリケーション イベント ログのソースは、"SQL Server コネクタ for Microsoft Azure Key Vault" になります。
  
SQL Server のバージョン  |再頒布可能パッケージのインストール リンク
---------|---------
2008、2008 R2、2012、2014 | [Visual Studio 2013 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=40784)
2016 | [Visual Studio 2015 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=48145)
  
## <a name="additional-references"></a>その他のリファレンス

 拡張キー管理について詳しくは、以下のページを参照してください。  
  
- [拡張キー管理 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 SQL の暗号化が EKM に対応することによって、次のことが可能となります。  
  
- [EKM の使用による TDE の有効化](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
- [バックアップの暗号化](../../../relational-databases/backup-restore/backup-encryption.md)  
  
- [暗号化されたバックアップの作成](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 関連する [!INCLUDE[tsql](../../../includes/tsql-md.md)] コマンド:  
  
- [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
- [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
- [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
- [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
- [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
- [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
- [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Azure Key Vault のドキュメント:  
  
- [Azure Key Vault とは](/azure/key-vault/general/basic-concepts)  
  
- [Azure Key Vault の使用を開始する](/azure/key-vault/general/overview)  
  
- PowerShell の [Azure Key Vault コマンドレット](/powershell/module/azurerm.keyvault/) のリファレンス  
  
## <a name="see-also"></a>参照

 [Azure Key Vault を使用した拡張キー管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)  
 [EKM provider enabled サーバー構成オプション](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
 [Azure Key Vault を使用した拡張キー管理のセットアップ手順](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)

追加のサンプル スクリプトについては、「[SQL Server Transparent Data Encryption and Extensible Key Management with Azure Key Vault (Azure Key Vault を使用した SQL Server Transparent Data Encryption と拡張キー管理)](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549)」のブログをご覧ください。