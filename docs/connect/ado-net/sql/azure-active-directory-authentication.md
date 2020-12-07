---
title: SqlClient での Azure Active Directory 認証の使用
description: サポートされている Azure Active Directory 認証モードを使用して、SqlClient で Azure SQL データ ソースに接続する方法について説明します
ms.date: 11/20/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: karinazhou
ms.author: v-jizho2
ms.reviewer: ''
ms.openlocfilehash: 0f8aaffc1f87b33a5c685b55d724fe96c44258af
ms.sourcegitcommit: ece151df14dc2610d96cd0d40b370a4653796d74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96297949"
---
# <a name="using-azure-active-directory-authentication-with-sqlclient"></a>SqlClient での Azure Active Directory 認証の使用

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

この記事では、.NET アプリケーションから SqlClient で Azure Active Directory (Azure AD) 認証を使用して Azure SQL データ ソースに接続する方法について説明します。

Azure AD 認証では、Azure AD の ID を使用して、Azure SQL Database、Azure SQL Managed Instance、Azure Synapse Analytics などの Azure SQL データ ソースにアクセスします。 **Microsoft.Data.SqlClient** 名前空間を使用すると、クライアント アプリケーションで Azure SQL Database に接続しているときに、さまざまな認証モードで Azure AD 資格情報を指定できます。 

接続文字列の `Authentication` 接続プロパティを設定すると、クライアントでは、指定された値に従って優先する Azure AD 認証モードを選択できます。

- 最初の **Microsoft.Data.SqlClient** バージョンでは、.NET Framework、.NET Core、および .NET Standard の `Active Directory Password` がサポートされています。 また、.NET Framework の `Active Directory Integrated` 認証と `Active Directory Interactive` 認証もサポートされています。 

- **Microsoft.Data.SqlClient** 2.0.0 から、`Active Directory Integrated` 認証と `Active Directory Interactive` 認証のサポートが .NET Framework、.NET Core、および .NET Standard にわたって拡張されました。 

  SqlClient 2.0.0 には、新しい `Active Directory Service Principal` 認証モードも追加されています。 サービス プリンシパル ID のクライアント ID とシークレットを使用して認証を行います。 

- **Microsoft.Data.SqlClient** 2.1.0 には、他にも認証モードが追加されています (`Active Directory Device Code Flow` や `Active Directory Managed Identity` (別名 `Active Directory MSI`) など)。 これらの新しいモードにより、アプリケーションでサーバーに接続するためのアクセス トークンを取得できます。 

以下のセクションで説明されていない Azure AD 認証の詳細については、[Azure Active Directory 認証を使用した SQL Database への接続](/azure/azure-sql/database/authentication-aad-overview)に関する記事を参照してください。


## <a name="setting-azure-active-directory-authentication"></a>Azure Active Directory 認証の設定

アプリケーションが Azure AD 認証を使用して Azure SQL データ ソースに接続するときは、有効な認証モードを指定する必要があります。 次の表に、サポートされている認証モードの一覧を示します。 アプリケーションでは、接続文字列の `Authentication` 接続プロパティを使用してモードを指定します。

| 値 | 説明  | フレームワーク    | Microsoft.Data.SqlClient のバージョン |
|:--|:--|:--|:--:|
| Active Directory パスワード | ユーザー名とパスワードを使用して Azure AD の ID で認証します | .NET Framework 4.6 以降、.NET Core 2.1 以降、.NET Standard 2.0 以降  | 1.0 以降|
| Active Directory 統合 |統合認証を使用して Azure AD の ID で認証します | .NET Framework 4.6 以降、.NET Core 2.1 以降、.NET Standard 2.0 以降 | 2.0.0 以降<sup>1</sup> |
| Active Directory 対話型 | 対話型認証を使用して Azure AD の ID で認証します | .NET Framework 4.6 以降、.NET Core 2.1 以降、.NET Standard 2.0 以降 | 2.0.0 以降<sup>1</sup> |
| Active Directory サービス プリンシパル | サービス プリンシパル ID のクライアント ID とシークレットを使用して Azure AD の ID で認証します | .NET Framework 4.6 以降、.NET Core 2.1 以降、.NET Standard 2.0 以降 | 2.0.0 以降 |
| Active Directory デバイス コード フロー | デバイス コード フロー モードを使用して Azure AD の ID で認証します | .NET Framework 4.6 以降、.NET Core 2.1 以降、.NET Standard 2.0 以降 | 2.1.0 以降 |
| Active Directory Managed Identity、 <br>Active Directory MSI | システム割り当て、またはユーザー割り当てマネージド ID を使用して Azure AD の ID で認証します | .NET Framework 4.6 以降、.NET Core 2.1 以降、.NET Standard 2.0 以降 | 2.1.0 以降 |

<sup>1</sup> **Microsoft.Data.SqlClient** 2.0.0 より前のバージョンでは、`Active Directory Integrated` および `Active Directory Interactive` 認証は .NET Framework 4.6 以降でのみサポートされます。 


## <a name="using-active-directory-password-authentication"></a>Active Directory パスワード認証の使用

`Active Directory Password` 認証モードでは、ネイティブまたはフェデレーション Azure AD ユーザーの Azure AD を使用した Azure データ ソースへの認証がサポートされます。 このモードを使用する場合は、接続文字列にユーザー資格情報を指定する必要があります。 次の例は、`Active Directory Password` 認証を使用する方法を示しています。

```c#
// Use your own server, database, user ID, and password.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Password; Database=testdb; User Id=user@domain.com; Password=**_";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-integrated-authentication"></a>Active Directory 統合認証の使用

`Active Directory Integrated` 認証モードを使用するには、オンプレミスの Active Directory インスタンスをクラウド内の Azure AD とフェデレーションする必要があります。 たとえば、Active Directory フェデレーション サービス (AD FS) を使用してフェデレーションを行うことができます。

ドメイン参加済みのマシンにサインインしている場合は、このモードで資格情報の入力を求められることなく、Azure SQL データ ソースにアクセスできます。 .NET Framework アプリケーションの接続文字列にユーザー名とパスワードを指定することはできません。 .NET Core および .NET Standard アプリケーションの接続文字列では、ユーザー名は省略可能です。 このモードでは、SqlConnection の `Credential` プロパティを設定することはできません。 

次のコード スニペットは、`Active Directory Integrated` 認証が使用されている場合の例です。

```c#
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is optional for .NET Core and .NET Standard.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-interactive-authentication"></a>Active Directory 対話型認証の使用

`Active Directory Interactive` 認証では、Azure SQL データ ソースに接続するための多要素認証テクノロジがサポートされています。 この認証モードを接続文字列で指定すると、Azure 認証画面が表示され、ユーザーは有効な資格情報を入力するように求められます。 接続文字列にパスワードを指定することはできません。 

このモードでは、SqlConnection の `Credential` プロパティを設定することはできません。 _ *Microsoft.Data.SqlClient** 2.0.0 以降では、対話モードの場合に接続文字列でのユーザー名の使用が許可されます。 

次の例は、`Active Directory Interactive` 認証を使用する方法を示しています。

```c#
// Use your own server, database, and user ID.
// User ID is optional.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is not provided.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-service-principal-authentication"></a>Active Directory サービス プリンシパル認証の使用

`Active Directory Service Principal` 認証モードでは、クライアント アプリケーションは、サービス プリンシパル ID のクライアント ID とシークレットを指定することによって、Azure SQL データ ソースに接続できます。 サービス プリンシパル認証には次が伴います。
1. シークレットを使用してアプリの登録を設定する。
1. Azure SQL Database インスタンスのアプリにアクセス許可を付与する。
1. 正しい資格情報で接続する。 

次の例は、`Active Directory Service Principal` 認証を使用する方法を示しています。

```c#
// Use your own server, database, app ID, and secret.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Service Principal; Database=testdb; User Id=AppId; Password=secret";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-device-code-flow-authentication"></a>Active Directory デバイス コード フロー認証の使用

.NET 用 [Microsoft Authentication Library](/azure/active-directory/develop/msal-overview) (MSAL.NET) を使用すると、`Active Directory Device Code Flow` 認証により、クライアント アプリケーションで、対話型の Web ブラウザーがインストールされていないデバイスやオペレーティング システムから Azure SQL データ ソースに接続できます。 対話型認証は、別のデバイスで実行されます。 デバイス コード フロー認証の詳細については、[OAuth 2.0 デバイス コード フロー](/azure/active-directory/develop/v2-oauth2-device-code)に関する記事を参照してください。 

このモードを使用している場合、`SqlConnection` の `Credential` プロパティを設定することはできません。 また、接続文字列でユーザー名とパスワードを指定することはできません。 

次のコード スニペットは、`Active Directory Device Code Flow` 認証を使用する場合の例です。

```c#
// Use your own server and database.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Device Code Flow; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-managed-identity-authentication"></a>Active Directory Managed Identity 認証の使用

Azure リソースの "*マネージド ID*" は、以前にマネージド サービス ID (MSI) と呼ばれていたサービスの新しい名前です。 クライアント アプリケーションが Azure リソースを使用して Azure AD 認証がサポートされた Azure サービスにアクセスする場合、Azure AD で Azure リソースの ID を指定することによって、マネージド ID を使用して認証できます。 その後、その ID を使用してアクセス トークンを取得できます。 これにより、資格情報とシークレットを管理する必要がなくなります。 

マネージド ID には、次の 2 種類があります。 

- "_システム割り当てマネージド ID_" は、Azure AD のサービス インスタンス上に作成されます。 これは、そのサービス インスタンスのライフサイクルに関連付けられています。 
- "_ユーザー割り当てマネージド ID_" は、スタンドアロンの Azure リソースとして作成されます。 Azure サービスの 1 つ以上のインスタンスに割り当てることができます。 

マネージド ID の詳細については、[Azure リソースのマネージド ID の概要](/azure/active-directory/managed-identities-azure-resources/overview)に関する記事を参照してください。

**Microsoft.Data.SqlClient** 2.1.0 以降、ドライバーでは、マネージド ID を使用してアクセス トークンを取得することによる Azure SQL Database、Azure Synapse Analytics、および Azure SQL Managed Instance への認証がサポートされています。 この認証を使用するには、接続文字列で `Active Directory Managed Identity`、`Active Directory MSI` のいずれかを指定します。パスワードは必要ありません。 

このモードで `SqlConnection` の `Credential` プロパティを設定することはできません。 ユーザー割り当てマネージド ID の場合は、ユーザー名を指定する必要があります。 

次の例は、システム割り当てマネージド ID で `Active Directory Managed Identity` 認証を使用する方法を示しています。

```c#
// For system-assigned managed identity
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```

次の例は、ユーザー割り当てマネージド ID を使用した `Active Directory Managed Identity` 認証を示しています。

```c#
// For user-assigned managed identity
// Use your own server, database, and user ID.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="customizing-active-directory-authentication"></a>Active Directory 認証のカスタマイズ

**Microsoft.Data.SqlClient** 2.1.0 以降では、ドライバーに組み込まれている Active Directory 認証を使用するだけでなく、Active Directory 認証をカスタマイズするためのオプションがアプリケーションに提供されます。 カスタマイズは、[`SqlAuthenticationProvider`](/dotnet/api/system.data.sqlclient.sqlauthenticationprovider) 抽象クラスから派生した `ActiveDirectoryAuthenticationProvider` クラスに基づきます。 

Active Directory 認証中、クライアント アプリケーションは次のいずれかの方法で独自の `ActiveDirectoryAuthencationProvider` クラスを定義できます。

- カスタマイズされたコールバック メソッドを使用する。
- アクセス トークンをフェッチするために SqlClient ドライバーを使用してアプリケーション クライアント ID を MSAL ライブラリに渡す。

次の例は、`Active Directory Device Code Flow` 認証を使用している場合にカスタム コールバックを使用する方法を示しています。 

[!code-csharp [AADAuthenticationCustomDeviceFlowCallback#1](~/../sqlclient/doc/samples/AADAuthenticationCustomDeviceFlowCallback.cs#1)]

カスタマイズされた `ActiveDirectoryAuthenticationProvider` クラスでは、サポートされている Active Directory 認証モードが使用されている場合に、ユーザー定義のアプリケーション クライアント ID を SqlClient に渡すことができます。 サポートされている Active Directory 認証モードには、`Active Directory Password`、`Active Directory Integrated`、`Active Directory Interactive`、`Active Directory Service Principal`、`Active Directory Device Code Flow` などがあります。

アプリケーション クライアント ID は、`SqlAuthenticationProviderConfigurationSection` または `SqlClientAuthenticationProviderConfigurationSection` を使用して構成することもできます。 構成プロパティ `applicationClientId` は、.NET Framework 4.6 以降と .NET Core 2.1 以降に適用されます。

次のコード スニペットは、`Active Directory Interactive` 認証が使用されている場合に、カスタマイズされた `ActiveDirectoryAuthenticationProvider` クラスをユーザー定義のアプリケーション クライアント ID と共に使用する例です。

[!code-csharp [ApplicationClientIdAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/ApplicationClientIdAzureAuthenticationProvider.cs#1)]

次の例は、configuration セクションを使用してアプリケーション クライアント ID を設定する方法を示しています。

```xml
<configuration>
  <configSections>
    <section name="SqlClientAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlClientAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlClientAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>

<!--or-->

<configuration>
  <configSections>
    <section name="SqlAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>
```

## <a name="support-for-a-custom-sql-authentication-provider"></a>カスタム SQL 認証プロバイダーのサポート

柔軟性の向上により、クライアント アプリケーションでは、`ActiveDirectoryAuthenticationProvider` クラスを使用する代わりに、Active Directory 認証用に独自のプロバイダーを使用することもできます。 カスタム認証プロバイダーは、オーバーライドされたメソッドを含む `SqlAuthenticationProvider` のサブクラスである必要があります。 

次の例は、`Active Directory Device Code Flow` 認証用に新しい認証プロバイダーを使用する方法を示しています。

[!code-csharp [CustomDeviceCodeFlowAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/CustomDeviceCodeFlowAzureAuthenticationProvider.cs#1)]

`Active Directory Interactive` 認証エクスペリエンスの改善に加え、**Microsoft.Data.SqlClient** 2.1.0 以降では、クライアント アプリケーションで対話型認証とデバイス コード フロー認証をカスタマイズするための次の API が提供されます。

```c#
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework targeted applications only
    // Sets a reference to the current System.Windows.Forms.IWin32Window that triggers the browser to be shown. 
    // Used to center the browser pop-up onto this window.
    public void SetIWin32WindowFunc(Func<IWin32Window> iWin32WindowFunc);

    // For .NET Standard targeted applications only
    // Sets a reference to the ViewController (if using Xamarin.iOS), Activity (if using Xamarin.Android) IWin32Window, or IntPtr (if using .NET Framework). 
    // Used for invoking the browser for Active Directory Interactive authentication.
    public void SetParentActivityOrWindowFunc(Func<object> parentActivityOrWindowFunc);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Sets a callback method that's invoked with a custom web UI instance that will let the user sign in with Azure AD, present consent if needed, and get back the authorization code. 
    // Applicable when working with Active Directory Interactive authentication.
    public void SetAcquireAuthorizationCodeAsyncCallback(Func<Uri, Uri, CancellationToken, Task<Uri>> acquireAuthorizationCodeAsyncCallback);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Clears cached user tokens from the token provider.
    public static void ClearUserTokenCache();
}
```


## <a name="see-also"></a>関連項目
- [Azure Active Directory のアプリケーション オブジェクトとサービス プリンシパル オブジェクト](/azure/active-directory/develop/app-objects-and-service-principals)
- [認証フロー](/azure/active-directory/develop/msal-authentication-flows)
