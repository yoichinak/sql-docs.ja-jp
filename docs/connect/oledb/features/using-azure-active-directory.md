---
title: Azure Active Directory の使用
description: Microsoft OLE DB Driver for SQL Server で利用できて、Azure SQL データベースへの接続を可能にする Azure Active Directory 認証方法について説明します。
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: bace88bd8ccf42cbef96a34ddb2af2593cedd7be
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727299"
---
# <a name="using-azure-active-directory"></a>Azure Active Directory の使用
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>目的

バージョン 18.2.1 から、Microsoft OLE DB Driver for SQL Server では、フェデレーション ID を使用して OLE DB アプリケーションが Azure SQL Database のインスタンスに接続できるようになりました。 新しい認証方法は次のとおりです。
- Azure Active Directory のログイン ID とパスワード
- Azure Active Directory のアクセス トークン
- Azure Active Directory 統合認証
- SQL ログイン ID とパスワード

バージョン 18.3 では、次の認証方法のサポートが追加されています。
- Azure Active Directory 対話型認証
- Azure Active Directory マネージド ID 認証

> [!NOTE]
> `DataTypeCompatibility` (またはそれに対応するプロパティ) が `80` に設定された状態での次の認証モードの使用は、サポート**されていません**。
> - ログイン ID とパスワードを使用する Azure Active Directory 認証
> - アクセス トークンを使用する Azure Active Directory 認証
> - Azure Active Directory 統合認証
> - Azure Active Directory 対話型認証
> - Azure Active Directory マネージド ID 認証

## <a name="connection-string-keywords-and-properties"></a>接続文字列キーワードとプロパティ
次の接続文字列キーワードが、Azure Active Directory 認証をサポートするために導入されています。

|接続文字列キーワード|Connection プロパティ|説明|
|---               |---                |---        |
|Access Token|SSPROP_AUTH_ACCESS_TOKEN|Azure Active Directory に対する認証を行うためのアクセス トークンを指定します。 |
|認証|SSPROP_AUTH_MODE|使用する認証方法を指定します。|

新しいキーワード/プロパティの詳細については、次のページを参照してください。
- [OLE DB Driver for SQL Server での接続文字列キーワードの使用](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初期化プロパティと承認プロパティ](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>暗号化と証明書の検証
このセクションでは、暗号化および証明書の検証の動作の変更について説明します。 これらの変更は、新しい認証またはアクセス トークンの接続文字列キーワード (またはそれに対応するプロパティ) を使用する場合に**のみ**有効です。

### <a name="encryption"></a>暗号化
新しい接続プロパティ/キーワードが使用された場合、セキュリティを強化するために、ドライバーは既定の暗号化の値を `yes` に設定して、それをオーバーライドします。 オーバーライドが行われるのは、データ ソース オブジェクトの初期化時です。 初期化の前に何らかの方法で暗号化が設定されると、値は保持され、オーバーライドされません。

> [!NOTE]   
> ADO アプリケーション、および `IDataInitialize::GetDataSource` を介して `IDBInitialize` インターフェイスを取得するアプリケーションでは、このインターフェイスを実装するコア コンポーネントによって、暗号化が既定値の `no` に明示的に設定されます。 その結果、新しい認証プロパティ/キーワードではこの設定が保持され、暗号化の値はオーバーライド**されません**。 そのため、これらのアプリケーションで `Use Encryption for Data=true` を明示的に設定し、既定値をオーバーライドすることを**お勧めします**。

### <a name="certificate-validation"></a>証明書の検証
セキュリティを強化するために、新しい接続プロパティ/キーワードでは、**クライアントの暗号化設定に関係なく**、`TrustServerCertificate` 設定 (およびそれに対応する接続文字列キーワード/プロパティ) が保持されます。 その結果、既定でサーバー証明書が検証されます。

> [!NOTE]   
> 証明書の検証は、`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` レジストリ エントリの `Value` フィールドを使用して制御することもできます。 有効な値は `0` または `1`です。 OLE DB ドライバーでは、レジストリと接続プロパティ/キーワード設定の間で最も安全なオプションが選択されます。 つまり、レジストリ/接続設定の少なくとも 1 つでサーバー証明書の検証が有効になっていれば、ドライバーによってサーバー証明書が検証されます。

## <a name="gui-additions"></a>GUI の追加
ドライバーのグラフィカル ユーザー インターフェイスが拡張され、Azure Active Directory 認証が可能になりました。 詳細については、次を参照してください。
- [SQL Server のログイン ダイアログ](../help-topics/sql-server-login-dialog.md)
- [ユニバーサル データ リンク (UDL) の構成](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>接続文字列の例
このセクションでは、`IDataInitialize::GetDataSource` および `DBPROP_INIT_PROVIDERSTRING` プロパティで使用される新規および既存の接続文字列キーワードの例を示します。

### <a name="sql-authentication"></a>SQL 認証
- `IDataInitialize::GetDataSource`の使用
    - 新規:
        > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=SqlPassword**;User ID=[ユーザー名];Password=[パスワード];Use Encryption for Data=true
    - 非推奨:
        > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];User ID=[ユーザー名];Password=[パスワード];Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    - 新規:
        > Server=[サーバー];Database=[データベース];**Authentication=SqlPassword**;UID=[ユーザー名];PWD=[パスワード];Encrypt=yes
    - 非推奨:
        > Server=[サーバー];Database=[データベース];UID=[ユーザー名];PWD=[パスワード];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>セキュリティ サポート プロバイダー インターフェイス (SSPI) を使用する統合 Windows 認証

- `IDataInitialize::GetDataSource`の使用
    - 新規:
        > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
    - 非推奨:
        > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Integrated Security=SSPI**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    - 新規:
        > Server=[サーバー];Database=[データベース];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 非推奨:
        > Server=[サーバー];Database=[データベース];**Trusted_Connection=yes**;Encrypt=yes

### <a name="azure-active-directory-username-and-password-authentication"></a>Azure Active Directory のユーザー名とパスワードの認証

- `IDataInitialize::GetDataSource`の使用
    > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=ActiveDirectoryPassword**;User ID=[ユーザー名];Password=[パスワード];Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    > Server=[サーバー];Database=[データベース];**Authentication=ActiveDirectoryPassword**;UID=[ユーザー名];PWD=[パスワード];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Azure Active Directory 統合認証

- `IDataInitialize::GetDataSource`の使用
    > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    > Server=[サーバー];Database=[データベース];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>アクセス トークンを使用する Azure Active Directory 認証

- `IDataInitialize::GetDataSource`の使用
    > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Access Token=[アクセス トークン]**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    > `DBPROP_INIT_PROVIDERSTRING` を使用したアクセス トークンの提供はサポートされていません

### <a name="azure-active-directory-interactive-authentication"></a>Azure Active Directory 対話型認証

- `IDataInitialize::GetDataSource`の使用
    > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=ActiveDirectoryInteractive**;User ID=[ユーザー名];Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    > Server=[サーバー];Database=[データベース];**Authentication=ActiveDirectoryInteractive**;UID=[ユーザー名];Encrypt=yes

### <a name="azure-active-directory-managed-identity-authentication"></a>Azure Active Directory マネージド ID 認証

- `IDataInitialize::GetDataSource`の使用
    - ユーザー割り当てマネージド ID:
        > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=ActiveDirectoryMSI**;User ID=[オブジェクト ID];Use Encryption for Data=true
    - システム割り当てマネージド ID:
        > Provider=MSOLEDBSQL;Data Source=[サーバー];Initial Catalog=[データベース];**Authentication=ActiveDirectoryMSI**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`の使用
    - ユーザー割り当てマネージド ID:
        > Server=[サーバー];Database=[データベース];**Authentication=ActiveDirectoryMSI**;UID=[オブジェクト ID];Encrypt=yes
    - システム割り当てマネージド ID:
        > Server=[サーバー];Database=[データベース];**Authentication=ActiveDirectoryMSI**;Encrypt=yes

## <a name="code-samples"></a>コード サンプル

次のサンプルは、接続キーワードによって Azure Active Directory に接続するために必要なコードを示しています。 

### <a name="access-token"></a>Access Token
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Active Directory 統合
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>次のステップ
- [OAuth 2.0 コード付与フローを使用して Azure Active Directory Web アプリケーションへのアクセスを承認する](/azure/active-directory/azuread-dev/v1-protocols-oauth-code)。

- SQL Server への [Azure Active Directory 認証](/azure/azure-sql/database/authentication-aad-overview)について学習します。

- OLE DB ドライバーがサポートする[接続文字列キーワード](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)を使用してドライバー接続を構成します。