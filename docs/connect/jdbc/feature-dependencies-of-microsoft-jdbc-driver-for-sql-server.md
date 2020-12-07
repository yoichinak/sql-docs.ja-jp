---
title: Microsoft JDBC Driver の機能の依存関係
description: Microsoft JDBC Driver for SQL Server の依存関係と、それらを満たす方法について説明します。
ms.custom: ''
ms.date: 8/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9e7c01c160848e5a0067db9d37b7e2dbe220386f
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042435"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server の機能の依存関係

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、Microsoft JDBC Driver for SQL Server が依存しているライブラリを示します。 プロジェクトには、次の依存関係があります。

## <a name="compile-time"></a>コンパイル時間

 - `com.microsoft.azure:azure-keyvault`:Always Encrypted Azure Key Vault 機能用 Azure Key Vault Provider (省略可能)
 - `com.microsoft.azure:adal4j`:Azure Active Directory 認証機能および Azure Key Vault 機能用 Azure Active Directory Library for Java (省略可能)
 - `com.microsoft.rest:client-runtime`:Azure Active Directory 認証機能および Azure Key Vault 機能用 Azure Active Directory Library for Java (省略可能)
 - `org.antlr:antlr4-runtime`:useFmtOnly 機能用 ANTLR 4 Runtime (省略可能)
 - `org.osgi:org.osgi.core`:OSGi Framework をサポートするための OSGi Core ライブラリ。
 - `org.osgi:org.osgi.compendium`:OSGi Framework をサポートするための OSGi Compendium ライブラリ。
 - `com.google.code.gson`:セキュア エンクレーブ機能を使用する Always Encrypted 用の JSON パーサー (省略可能)
 - `org.bouncycastle.bcprov-jdk15on`:JAVA 8 のみを使用する場合の、セキュア エンクレーブ機能を使用する Always Encrypted 用の Bouncy Castle プロバイダー。 (省略可能)

## <a name="test-time"></a>テスト時

前述の機能のいずれかを必要とするプロジェクトでは、該当する依存関係を POM ファイルに明示的に宣言する必要があります。

**例:** Azure Active Directory 認証機能を使用する場合は、プロジェクトの POM ファイルで `adal4j` 依存関係を再宣言する必要があります。 次のスニペットを参照してください。

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.7.4</version>
</dependency>
```

**例:** Azure Key Vault 機能を使用する場合は、プロジェクトの POM ファイルで `azure-keyvault` 依存関係と `adal4j` 依存関係を再宣言する必要があります。 次のスニペットを参照してください。

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.7.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.4</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC ドライバーの依存関係の要件

### <a name="working-with-the-azure-key-vault-provider"></a>Azure Key Vault プロバイダーの操作:

- JDBC ドライバー バージョン 8.4.1 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.2.4)、Adal4j (バージョン 1.6.5)、Client-Runtime-for-AutoRest (1.7.4)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 8.2.2 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.2.2)、Adal4j (バージョン 1.6.4)、Client-Runtime-for-AutoRest (1.7.0)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 7.4.1 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.2.1)、Adal4j (バージョン 1.6.4)、Client-Runtime-for-AutoRest (1.6.10)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 7.2.2 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.2.0)、Azure-Keyvault-Webkey (バージョン 1.2.0)、Adal4j (バージョン 1.6.3)、Client-Runtime-for-AutoRest (1.6.5)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 7.0.0 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.0.0)、Adal4j (バージョン 1.6.0)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-7.0.md))
- JDBC ドライバー バージョン 6.4.0 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.0.0)、Adal4j (バージョン 1.4.0)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-6.2.2.md))
- JDBC ドライバー バージョン 6.2.2 - 依存関係のバージョン:Azure-Keyvault (バージョン 1.0.0)、Adal4j (バージョン 1.4.0)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-6.2.2.md))
- JDBC ドライバー バージョン 6.0.0 - 依存関係のバージョン:Azure-Keyvault (バージョン 0.9.7)、Adal4j (バージョン 1.3.0)、およびそれらの依存関係 ([サンプル アプリケーション](azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> ドライバーの 6.2.2 および 6.4.0 バージョンでは、azure-keyvault-java の依存関係がバージョン 1.0.0 に更新されています。 ただし、新しいバージョンは前のバージョン (0.9.7) と互換性がないため、ドライバー内の既存の実装は破壊されます。 ドライバーの新しい実装では API を変更する必要があり、これにより、Azure Key Vault Provider を使用しているクライアント プログラムが破壊されます。
>
> この問題は、最新バージョンのドライバー (7.0.0 以降) では解決されています。 認証コールバック メカニズムを使用していた削除済みのコンストラクターは、下位互換性を保つために Azure Key Vault Provider に戻されています。

### <a name="working-with-azure-active-directory-authentication"></a>Azure Active Directory 認証の操作:

- JDBC ドライバー バージョン 8.4.1 - 依存関係のバージョン:Adal4j (バージョン 1.6.5)、Client-Runtime-for-AutoRest (1.7.4)、およびそれらの依存関係。
- JDBC ドライバー バージョン 8.2.2 - 依存関係のバージョン:Adal4j (バージョン 1.6.4)、Client-Runtime-for-AutoRest (1.7.0)、およびそれらの依存関係。 このバージョンのドライバーでは、"sqljdbc_auth.dll" は "mssql-jdbc_auth-\<version>-\<arch>.dll" に名前が変更されました。
- JDBC ドライバー バージョン 7.4.1 - 依存関係のバージョン:Adal4j (バージョン 1.6.4)、Client-Runtime-for-AutoRest (1.6.10)、およびそれらの依存関係
- JDBC ドライバー バージョン 7.2.2 - 依存関係のバージョン:Adal4j (バージョン 1.6.3)、Client-Runtime-for-AutoRest (1.6.5)、およびそれらの依存関係
- JDBC ドライバー バージョン 7.0.0 - 依存関係のバージョン:Adal4j (バージョン 1.6.0) とその依存関係
- JDBC ドライバー バージョン 6.4.0 - 依存関係のバージョン:Adal4j (バージョン 1.4.0) とその依存関係
- JDBC ドライバー バージョン 6.2.2 - 依存関係のバージョン:Adal4j (バージョン 1.4.0) とその依存関係
- JDBC ドライバー バージョン 6.0.0 - 依存関係のバージョン:Adal4j (バージョン 1.3.0)、およびその依存関係。 このバージョンのドライバーでは、Windows オペレーティング システム上で _ActiveDirectoryIntegrated_ 認証モードのみで sqljdbc_auth.dll と SQL Server 用 Active Directory 認証ライブラリ (ADALSQL.DLL) を使用して接続できます。

ドライバーのバージョン 6.4.0 以降、アプリケーションでは、Windows オペレーティング システム上で ADALSQL.DLL を必ず使用する必要はありません。 *Windows 以外のオペレーティング システム*では、ActiveDirectoryIntegrated 認証を機能させるには、ドライバーで Kerberos チケットが必要です。 Kerberos を使用して Active Directory に接続する方法の詳細については、「[Windows、Linux、macOS で Kerberos チケットを設定する](connecting-using-azure-active-directory-authentication.md#set-kerberos-ticket-on-windows-linux-and-macos)」をご覧ください。

*Windows オペレーティング システム*では、ドライバーは、既定で sqljdbc_auth.dll が検索され、Kerberos チケットの設定も Azure ライブラリの依存関係も必要ありません。 sqljdbc_auth.dll を使用できない場合、ドライバーでは、他のオペレーティング システムと同じように、Active Directory への認証用の Kerberos チケットが検索されます。

ドライバー バージョン 8.2.2 以降、"sqljdbc_auth.dll" は "mssql-jdbc_auth-\<version>-\<arch>.dll" に名前が変更されます。 例: 'mssql-jdbc_auth-8.2.2.x64.dll'

この機能を使用している[サンプル アプリケーション](connecting-using-azure-active-directory-authentication.md)を取得できます。

## <a name="see-also"></a>関連項目

[JDBC Driver GitHub リポジトリ](https://github.com/microsoft/mssql-jdbc)  
[JDBC Driver API リファレンス](reference/jdbc-driver-api-reference.md)
