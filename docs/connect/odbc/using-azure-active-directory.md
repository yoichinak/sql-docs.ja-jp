---
title: ODBC ドライバーでの Azure Active Directory の使用
description: Microsoft ODBC Driver for SQL Server を使用すると、ODBC アプリケーションで、Azure Active Directory を使用して Azure SQL Database のインスタンスに接続できるようになります。
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6925b2b79629fbcbe84f6577e2617e9b45ea82c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727385"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>ODBC ドライバーでの Azure Active Directory の使用
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>目的

Microsoft ODBC Driver for SQL Server バージョン 13.1 以降を使用すると、ODBC アプリケーションで、Azure Active Directory のフェデレーション ID を使用して、ユーザー名/パスワード、Azure Active Directory アクセス トークン、Azure Active Directory マネージド ID (17.3+)、または Windows 統合認証 (Linux/macOS での 17.6+) によって Azure SQL Database のインスタンスに接続できるようになります。 ODBC ドライバー バージョン 13.1 の場合、Azure Active Directory アクセス トークン認証は _Windows のみ_です。 ODBC ドライバー バージョン 17 以降では、すべてのプラットフォーム (Windows、Linux、macOS) でこの認証がサポートされます。 ログイン ID を使用した新しい Azure Active Directory 対話型認証は、Windows で ODBC ドライバー バージョン 17.1 に導入されています。 新しい Azure Active Directory マネージド ID 認証方法は、ODBC ドライバー バージョン 17.3.1.1 で、システム割り当てとユーザー割り当ての両方の ID に対して追加されました。 これらはすべて、新しい DSN と接続文字列のキーワード、および接続属性を使用することによって実現します。

> [!NOTE]
> バージョン 17.6 より前の、Linux および macOS の ODBC ドライバーでは、Azure Active Directory に対する直接の Azure Active Directory 認証のみがサポートされます。 Linux または macOS クライアントから Azure Active Directory のユーザー名とパスワード認証を使用しており、Active Directory 構成によって、クライアントに Active Directory フェデレーション サービス エンドポイントに対する認証が要求されている場合は、認証が失敗する可能性があります。 ドライバー バージョン 17.6 の時点でこの制限は削除されました。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新しいまたは変更された DSN と接続文字列のキーワード

DSN または接続文字列を使用して接続する場合、`Authentication` キーワードを使用して認証モードを制御できます。 接続文字列で設定された値は、DSN の値 (指定されている場合) をオーバーライドします。 `Authentication` 設定の "_事前属性値_" は、接続文字列および DSN の値から計算された値です。

|名前|値|Default|説明|
|-|-|-|-|
|`Authentication`|(未設定)、(空の文字列)、`SqlPassword`、`ActiveDirectoryPassword`、`ActiveDirectoryIntegrated`、`ActiveDirectoryInteractive`、`ActiveDirectoryMsi` |(未設定)|認証モードを制御します。<table><tr><th>値<th>説明<tr><td>(未設定)<td>認証モードは他のキーワード (既存のレガシ接続オプション) によって決定されます。<tr><td>(空の文字列)<td>(接続文字列のみ。)DSN で設定されている `Authentication` 値をオーバーライドおよび設定解除します。<tr><td>`SqlPassword`<td>ユーザー名とパスワードを使用して、SQL Server インスタンスに対して直接認証を行います。<tr><td>`ActiveDirectoryPassword`<td>ユーザー名とパスワードを使用して、Azure Active Directory の ID で認証を行います。<tr><td>`ActiveDirectoryIntegrated`<td>_Windows および Linux/Mac 17.6+ ドライバーのみ_。 統合認証を使用して、Azure Active Directory の ID で認証を行います。<tr><td>`ActiveDirectoryInteractive`<td>"_Windows ドライバーのみ_"。 対話型認証を使用して、Azure Active Directory の ID で認証を行います。<tr><td>`ActiveDirectoryMsi`<td>マネージド ID 認証を使用して、Azure Active Directory の ID で認証を行います。 ユーザー割り当て ID の場合、UID はユーザー ID のオブジェクト ID に設定されます。</table>|
|`Encrypt`|(未設定)、`Yes`、`No`|(説明を参照)|接続の暗号化を制御します。 DSN または接続文字列で `Authentication` 設定の事前属性値が _none_ でない場合、既定値は `Yes` です。 それ以外の場合、既定値は `No` です。 属性 `SQL_COPT_SS_AUTHENTICATION` によって `Authentication` の事前属性値がオーバーライドされる場合は、DSN か接続文字列または接続属性で暗号化の値を明示的に設定します。 暗号化の事前属性値は、その値が DSN または接続文字列のいずれかで `Yes` に設定されている場合は `Yes` です。|

## <a name="new-andor-modified-connection-attributes"></a>新しいまたは変更された接続属性

次の接続前接続属性は、Azure Active Directory 認証をサポートするために導入または変更されています。 接続属性に対応する接続文字列または DSN キーワードがあり、接続属性が設定されている場合は、接続属性が優先されます。

|属性|Type|値|Default|説明|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(未設定)|上記の `Authentication` キーワードの説明を参照してください。 `SQL_AU_NONE` は、DSN または接続文字列で設定された `Authentication` 値を明示的にオーバーライドするために用意されています。それに対し、`SQL_AU_RESET` は、属性が設定されている場合にそれを設定解除し、DSN または接続文字列の値が優先されるようにします。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|`ACCESSTOKEN` へのポインターまたは NULL|NULL|null 以外の場合は、使用する AzureAD アクセス トークンを指定します。 アクセス トークンを指定し、同時に `UID`、`PWD`、`Trusted_Connection`、または `Authentication` 接続文字列キーワードまたはそれと同等の属性を指定すると、エラーになります。 <br> **注:** ODBC ドライバー バージョン 13.1 では、_Windows_ でのみこれがサポートされます。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(説明を参照)|接続の暗号化を制御します。 `SQL_EN_OFF` を指定すると暗号化が無効になり、`SQL_EN_ON` を指定すると有効になります。 `Authentication` 設定の事前属性値が _none_ でないか、または `SQL_COPT_SS_ACCESS_TOKEN` が設定されていて、DSN または接続文字列のいずれかで `Encrypt` が指定されていなかった場合、既定値は `SQL_EN_ON` です。 それ以外の場合、既定値は `SQL_EN_OFF` です。 接続属性 `SQL_COPT_SS_AUTHENTICATION` が _none_ 以外に設定されていて、DSN または接続文字列で `Encrypt` が指定されていなかった場合は、`SQL_COPT_SS_ENCRYPT` を必要な値に明示的に設定してください。 この属性の有効な値によって、[接続に暗号化を使用するかどうか](../../relational-databases/native-client/features/using-encryption-without-validation.md)が制御されます。|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Azure Active Directory ではサポートされません。Azure AD プリンシパルに対するパスワードの変更は、ODBC 接続を通じて行うことができないためです。 <br><br>SQL Server 2005 では、SQL Server 認証におけるパスワードの期限切れが導入されました。 クライアントから接続の古いパスワードと新しいパスワードの両方を提供できるようにするために、`SQL_COPT_SS_OLDPWD` 属性が追加されました。 この属性が設定されている場合、接続文字列には変更された "古いパスワード" が含まれているので、プロバイダーは最初の接続またはそれ以降の接続で接続プールを使用しません。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|"_非推奨_" です。代わりに `SQL_COPT_SS_AUTHENTICATION` を `SQL_AU_AD_INTEGRATED` に設定して使用してください。 <br><br>サーバー ログインでのアクセス検証に Windows 認証 (Linux と macOS では Kerberos) を使用するように強制します。 Windows 認証を使用すると、ドライバーでは `SQLConnect`、`SQLDriverConnect`、または `SQLBrowseConnect` の処理の一環として提供されるユーザー ID とパスワードが無視されます。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory での UI の追加 (Windows ドライバーのみ)

ドライバーの DSN セットアップと接続の UI が拡張され、Azure AD による認証を使用するために必要なオプションが追加されました。

### <a name="creating-and-editing-dsns-in-the-ui"></a>UI で DSN を作成および編集する

ドライバーのセットアップ UI を使用して既存の DSN を作成または編集する際に、新しい Azure AD 認証オプションを使用できます。

Azure SQL Database への Azure Active Directory 統合認証の場合: `Authentication=ActiveDirectoryIntegrated`

![Azure Active Directory 統合認証を選択した DSN の作成および編集画面。](windows/create-dsn-ad-integrated.png)

Azure SQL Database に対する Azure Active Directory ユーザー名/パスワード認証の場合: `Authentication=ActiveDirectoryPassword`

![Azure Active Directory パスワード認証を選択した DSN の作成および編集画面。](windows/create-dsn-ad-password.png)

Azure SQL Database への Azure Active Directory 対話型認証の場合: `Authentication=ActiveDirectoryInteractive`

![Azure Active Directory 対話型認証を選択した DSN の作成および編集画面。](windows/create-dsn-ad-interactive.png)

SQL Server に対するユーザー名/パスワード認証の場合 (Azure またはそれ以外): `Authentication=SqlPassword`

![SQL Server 認証が選択された DSN の作成および編集画面。](windows/create-dsn-ad-sql-server.png)

Windows レガシ SSPI 統合認証の場合: `Trusted_Connection=Yes`

![統合 Windows 認証を選択した DSN の作成および編集画面。](windows/create-dsn-win-sspi.png)

Azure Active Directory マネージド ID 認証の場合: `Authentication=ActiveDirectoryMsi`

![マネージド サービス ID 認証を選択した DSN の作成および編集画面。](windows/create-dsn-ad-msi.png)

6 つのオプションは、それぞれ `Trusted_Connection=Yes` (既存のレガシ Windows SSPI のみの統合認証) と `Authentication=` `ActiveDirectoryIntegrated`、`SqlPassword`、`ActiveDirectoryPassword`、`ActiveDirectoryInteractive`、および `ActiveDirectoryMsi` に対応しています。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect プロンプト (Windows ドライバーのみ)

接続を完了するために必要な情報を要求するときに SQLDriverConnect によって表示されるプロンプト ダイアログには、Azure AD 認証に関する 4 つの新しいオプションが含まれています。

![SQLDriverConnect によって表示される SQL Server のログイン ダイアログ。](windows/server-login.png)

これらのオプションは、上記の DSN セットアップ UI で使用できるものと同じ 6 つのオプションに対応しています。

### <a name="example-connection-strings"></a>接続文字列の例
1. SQL Server 認証 - レガシ構文。 サーバー証明書は検証されず、暗号化はサーバーで適用される場合にのみ使用されます。 ユーザー名/パスワードは接続文字列内で渡されます。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 認証 - 新しい構文。 クライアントが暗号化を要求します (`Encrypt` の既定値は `true` です)。サーバー証明書は、暗号化の設定に関係なく検証されます (`TrustServerCertificate` が `true` に設定されている場合を除きます)。 ユーザー名/パスワードは接続文字列内で渡されます。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. (SQL Server または SQL IaaS に対する) SSPI を使用した統合 Windows 認証 (Linux と macOS では Kerberos) - 現在の構文。 暗号化を使用しない限り、サーバー証明書は検証されません。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. ("_Windows ドライバーのみ_"。)SSPI を使用した統合 Windows 認証 (ターゲット データベースが SQL Server または SQL IaaS 内にある場合) - 新しい構文。 クライアントが暗号化を要求します (`Encrypt` の既定値は `true` です)。サーバー証明書は、暗号化の設定に関係なく検証されます (`TrustServerCertificate` が `true` に設定されている場合を除きます)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Azure Active Directory ユーザー名/パスワード認証 (ターゲット データベースが Azure SQL Database 内にある場合)。 暗号化の設定に関係なく、サーバー証明書は検証されます (`TrustServerCertificate` が `true` に設定されている場合を除きます)。 ユーザー名/パスワードは接続文字列内で渡されます。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows および Linux/macOS 17.6+ ドライバーのみ_)。ADAL または Kerberos を使用した統合 Windows 認証。ターゲット データベースが Azure SQL Database 内にあると想定して、Azure AD によって発行されたアクセス トークンの Windows アカウント資格情報を使用します。 暗号化の設定に関係なく、サーバー証明書は検証されます (`TrustServerCertificate` が `true` に設定されている場合を除きます)。 Linux/macOS では、適切な Kerberos チケットが必要です。詳細については、以下のフェデレーション アカウントに関するセクションと「[統合認証を使用する](linux-mac/using-integrated-authentication.md)」をご覧ください。
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. ("_Windows ドライバーのみ_"。)Azure AD 対話型認証では、Azure Multi-factor Authentication テクノロジを使用して接続をセットアップします。 このモードでは、ログイン ID を指定することで Azure 認証ダイアログがトリガーされ、ユーザーがパスワードを入力して接続を完了できます。 ユーザー名は接続文字列内で渡されます。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![Active Directory 対話型認証を使用する場合の Windows Azure 認証 UI。](windows/WindowsAzureAuth.png)

8. Azure Active Directory マネージド ID 認証では、システム割り当てまたはユーザー割り当ての ID を認証に使用して接続をセットアップします。 ユーザー割り当て ID の場合、UID はユーザー ID のオブジェクト ID に設定されます。<br>
システムによって割り当てられた ID の場合:<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
オブジェクト ID が myObjectId であるユーザー割り当て ID の場合:<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE]
>- バージョン 17.4.2 ***より前の*** Windows ODBC ドライバーで Active Directory オプションを使用する場合は、[SQL Server 用 Active Directory 認証ライブラリ](https://go.microsoft.com/fwlink/?LinkID=513072)がインストールされていることを確認します。 Linux および macOS ドライバーを使用する場合は、`libcurl` がインストールされていることを確認します。 ドライバー バージョン 17.2 以降では、これが明示的な依存関係にはなりません。他の認証方法や ODBC 操作では不要であるためです。
>- Azure Active Directory 構成に条件付きアクセス ポリシーが含まれ、クライアントが Windows 10 または Server 2016 以降である場合は、統合またはユーザー名/パスワードによる認証は失敗する可能性があります。 条件付きアクセス ポリシーでは、Windows アカウント マネージャー (WAM) を使用する必要があります。これは、Windows のドライバー バージョン 17.6 以降でサポートされています。 WAM を使用するには、グローバル、ユーザー DSN、またはシステム DSN スコープ構成それぞれの `HKLM\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`、`HKCU\Software\ODBC\ODBC.INI\<your-user-DSN-name>`、または `HKLM\Software\ODBC\ODBC.INI\<your-system-DSN-name>` に `ADALuseWAM` という名前の新しい文字列または DWORD 値を作成し、その値を 1 に設定します。 なお、WAM での認証では、`runas`を使用して別のユーザーとしてアプリケーションを実行することはサポートされていません。 条件付きアクセス ポリシーを必要とするシナリオは、Linux および macOS ではサポートされていません。
>- SQL Server アカウントのユーザー名とパスワードを使用して接続する場合、新しい `SqlPassword` オプションを使用できるようになりました。このオプションは、より安全性の高い接続の既定値が有効になるので、Azure SQL では特にお勧めします。
>- Azure Active Directory アカウントのユーザー名とパスワードを使用して接続するには、接続文字列に `Authentication=ActiveDirectoryPassword` を指定し、ユーザー名とパスワードではそれぞれ `UID` と `PWD` キーワードを指定します。
>- Windows 統合または Active Directory 統合 (Windows および Linux/macOS 17.6+ ドライバーのみ) 認証を使用して接続するには、接続文字列に `Authentication=ActiveDirectoryIntegrated` を指定します。 ドライバーによって適切な認証モードが自動的に選択されます。 `UID` と `PWD` は指定できません。
>- Active Directory 対話型 (Windows ドライバーのみ) 認証を使用して接続するには、`UID` を指定する必要があります。

## <a name="authenticating-with-an-access-token"></a>アクセス トークンを使用した認証

`SQL_COPT_SS_ACCESS_TOKEN` 接続前属性を使用すると、ユーザー名とパスワードではなく Azure AD から取得したアクセス トークンを認証に使用できます。また、ドライバーによるアクセス トークンのネゴシエーションと取得もバイパスされます。 アクセス トークンを使用するには、`SQL_COPT_SS_ACCESS_TOKEN` 接続属性を `ACCESSTOKEN` 構造体へのポインターに設定します。

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN` は、4 バイト_長_と、その後のアクセス トークンを形成する不透明データのバイト_長_によって構成される、可変長構造体です。 SQL Server によるアクセス トークンの処理方法が原因で、[OAuth 2.0](/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 応答を介して取得されたものを拡張して、ASCII 文字のみを含む UCS 2 文字列のように、各バイトの後に 0 埋め込みバイトを挿入することが必要です。ただし、トークンは不透明値であり、バイト単位で指定する長さに null 終端文字を含めることはできません。 この認証方法は、長さと形式の制約が非常に多いため、`SQL_COPT_SS_ACCESS_TOKEN` 接続属性を使用してプログラムでのみ使用できます。対応する DSN または接続文字列のキーワードはありません。 接続文字列には、`UID`、`PWD`、`Authentication`、または `Trusted_Connection` キーワードを含めることはできません。

> [!NOTE]
> ODBC ドライバー バージョン 13.1 では、_Windows_ でのみこの認証がサポートされます。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 認証サンプル コード

次のサンプルは、Azure Active Directory を使用して接続キーワードによって SQL Server に接続するために必要なコードを示しています。 アプリケーション コード自体を変更する必要はないことに注意してください。認証に Azure AD を使用するために必要な変更は、接続文字列または DSN (使用されている場合) だけです。
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);    
    ...
~~~
次のサンプルは、Azure Active Directory を使用してアクセス トークン認証によって SQL Server に接続するために必要なコードを示しています。 この場合、アクセス トークンを処理し、関連する接続属性を設定するためにアプリケーション コードの変更が必要です。
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);        
    ...
    free(pAccToken);
~~~
以下は、Azure Active Directory 対話型認証で使用するサンプルの接続文字列です。 パスワードは Azure 認証画面を使用して入力されるため、PWD フィールドが含まれていないことに注意してください。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
以下は、Azure Active Directory マネージド ID 認証で使用するサンプルの接続文字列です。 ユーザー割り当て ID に対して、UID がユーザー ID のオブジェクト ID に設定されていることに注意してください。
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="considerations-for-using-adfs-federated-accounts-on-linuxmacos"></a>Linux/macOS で ADFS フェデレーション アカウントを使用する場合の考慮事項

バージョン 17.6 以降、Linux および macOS 用のドライバーでは、ユーザー名/パスワード (`ActiveDirectoryPassword`) または Kerberos (`ActiveDirectoryIntegrated`) を使用した Azure Active Directory ADFS フェデレーション アカウントによる認証をサポートしています。 統合モードを使用する場合、プラットフォームによって異なるいくつかの制限があります。

UPN サフィックスが Kerberos 領域とは異なるユーザー、つまり、代替 UPN サフィックスが使用されているユーザーで認証する場合は、Kerberos チケットを取得するときに Enterprise Principal オプション (`kinit` で `-E` オプションを使用し、`user@federated-domain` の形式でプリンシパル名を指定) を使用する必要があります。 これにより、ドライバーはフェデレーション ドメインと Kerberos 領域の両方を正しく判断できます。

`klist` コマンドの出力を調べることにより、適切な Kerberos チケットが使用可能であることを確認できます。 フェデレーション ドメインが Kerberos 領域と UPN サフィックスと同じ場合、プリンシパル名は `user@realm`の形式になります。 異なる場合は、プリンシパル名は `user@federated-domain@realm`の形式にする必要があります。

### <a name="linux"></a>Linux

SuSE 11 では、既定の Kerberos ライブラリ バージョン 1.6.x は、代替 UPN サフィックスを使用するために必要な Enterprise Principal オプションをサポートしていません。 Azure AD 統合認証で代替 UPN サフィックスを使用するには、Kerberos ライブラリを 1.7 以降にアップグレードします。

Alpine Linux では、既定の `libcurl` は Azure AD 統合認証に必要な SPNEGO/Kerberos 認証をサポートしていません。

### <a name="macos"></a>macOS

システム Kerberos ライブラリ `kinit` は、`--enterprise` オプションを使用した Enterprise Principal をサポートしていますが、名前の正規化を暗黙的に実行します。これにより、代替 UPN サフィックスを使用できなくなります。 Azure AD 統合認証で代替 UPN サフィックスを使用するには、`brew install krb5` を介して新しい Kerberos ライブラリをインストールし、前述のように `-E` オプションと共に `kinit` を使用します。

## <a name="see-also"></a>参照

[Azure AD 認証を使用して Azure SQL Database のトークン ベース認証をサポート](/archive/blogs/sqlsecurity/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

[統合認証を使用する](linux-mac/using-integrated-authentication.md)