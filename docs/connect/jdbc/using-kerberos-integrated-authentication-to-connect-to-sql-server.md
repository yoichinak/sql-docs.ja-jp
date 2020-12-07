---
description: Kerberos 統合認証による SQL Server への接続
title: Kerberos 統合認証による SQL Server への接続 | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d015565b114641f2c44c28da1f2dc03e4fdda773
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727517"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Kerberos 統合認証による SQL Server への接続

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 以降、アプリケーションは、**authenticationScheme** 接続プロパティを使用して、タイプ 4 の Kerberos 統合認証を使用してデータベースに接続することを示すことができます。 接続プロパティの詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。 Kerberos の詳細については、「[Microsoft Kerberos](/windows/win32/secauthn/microsoft-kerberos)」を参照してください。

Java **Krb5LoginModule** で統合認証を使用する場合、[Krb5LoginModule クラス](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)を使用してモジュールを構成できます。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、IBM Java VM 用に次のプロパティが設定されます。

- **useDefaultCcache = true**
- **moduleBanner = false**

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、他のすべての Java VM 用に次のプロパティが設定されます。

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>解説

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] より前、アプリケーションでは、「[接続 URL の構築](../../connect/jdbc/building-the-connection-url.md)」に示されているように、**integratedSecurity** 接続プロパティを使用し、**mssql-jdbc_auth-\<version>-\<arch>.dll** を参照することによって、(使用可能性に基づいて Kerberos または NTLM を使用する) 統合認証を指定できました。

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 以降、アプリケーションは、**authenticationScheme** 接続プロパティを使用して、ピュア Java Kerberos 実装を使用した Kerberos 統合認証を使用してデータベースに接続することを示すことができます。

- **Krb5LoginModule** による統合認証を使用するには、依然として **integratedSecurity=true** 接続プロパティを指定する必要があります。 その後、**authenticationScheme=JavaKerberos** 接続プロパティも指定します。

- **mssql-jdbc_auth-\<version>-\<arch>.dll** による統合認証を引き続き使用するには、単に **integratedSecurity=true** 接続プロパティ (また、必要に応じて **authenticationScheme=NativeAuthentication**) を指定します。

- **authenticationScheme=JavaKerberos** を指定するが **integratedSecurity=true** を指定しない場合は、ドライバーによって **authenticationScheme** 接続プロパティが無視され、ユーザー名とパスワードの資格情報が接続文字列に含まれていると見なされます。

データソースを使用して接続を作成する場合、**setAuthenticationScheme** を使用して認証スキームをプログラムで設定できます。また、(必要に応じて) **setServerSpn** を使用して Kerberos 接続用の SPN を設定できます。

Kerberos 認証をサポートするために、新しいロガー com.microsoft.sqlserver.jdbc.internals.KerbAuthentication が追加されました。 詳細については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」を参照してください。

Kerberos を構成する場合は、次のガイドラインに従ってください。

1. Windows のレジストリで **AllowTgtSessionKey** を 1 に設定します。 詳しくは、「[Kerberos protocol registry entries and KDC configuration keys in Windows Server 2003](https://support.microsoft.com/kb/837361)」(Windows Server 2003 における Kerberos プロトコルのレジストリ エントリおよび KDC 構成キー) をご覧ください。
2. Kerberos 構成 (UNIX 環境の krb5.conf) で環境の適切な領域および KDC が指定されていることを確認します。
3. kinit を使用するかまたはドメインにログインして、TGT キャッシュを初期化します。
4. **authenticationScheme=JavaKerberos** を使用するアプリケーションを Windows Vista または Windows 7 オペレーティング システムで実行する場合は、標準ユーザー アカウントを使用する必要があります。 ただし、管理者のアカウントでアプリケーションを実行する場合は、アプリケーションを管理者権限で実行する必要があります。

> [!NOTE]  
> serverSpn 接続属性は、Microsoft JDBC Driver 4.2 以降でのみサポートされています。

## <a name="service-principal-names"></a>サービス プリンシパル名

サービス プリンシパル名 (SPN) は、クライアントがサービスのインスタンスを一意に識別するための名前です。

**serverSpn** 接続プロパティを使用して SPN を指定できますが、ドライバーで自動的に作成することもできます (既定)。 このプロパティの形式は、"MSSQLSvc/fqdn:port\@REALM" です。fqdn は完全修飾ドメイン名、port はポート番号、REALM は SQL Server の Kerberos 領域を大文字で示したものです。 Kerberos 構成の既定の領域が、サーバーと同じ領域であり、既定で含まれていない場合には、このプロパティの領域部分は省略可能です。 ここで、Kerberos 構成で既定の領域がサーバーの領域とは異なる領域であり、その領域間の認証のシナリオをサポートする場合には、serverSpn プロパティを使用して SPN を設定する必要があります。

たとえば、SPN は次のようになります。"MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ.CORP.CONTOSO.COM"

サービス プリンシパル名 (SPN) の詳細については、以下を参照してください。

- [Kerberos 接続用のサービス プリンシパル名の登録](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)

- [SQL Server での Kerberos の使用](/archive/blogs/sql_protocols/using-kerberos-with-sql-server)

> [!NOTE]  
> 6\.2 リリースより前の JDBC ドライバーでは、Cross Realm Kerberos を適切に使用するために、**serverSpn** を明示的に設定する必要があります。
>
> 6\.2 リリースでは、Cross Realm Kerberos を使用する場合でも、ドライバーによって既定で **serverSpn** を構築できます。 ただし、**serverSpn** を明示的に使用することもできます。

## <a name="creating-a-login-module-configuration-file"></a>ログイン モジュール構成ファイルの作成

オプションで Kerberos 構成ファイルを指定できます。 構成ファイルを指定しない場合、次の設定が有効になります。

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

ログイン モジュール構成ファイルを作成する場合は、次の形式に従ってファイルを作成する必要があります。

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

ログイン構成ファイルは、特定の 1 つまたは複数のアプリケーションに使用する基底の認証テクノロジを指定する 1 つ以上のエントリから構成されます。 たとえば、次のように入力します。

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

このように、それぞれのログイン モジュール構成ファイル エントリは、名前と、それに続く、(それぞれがセミコロンで終了し、グループ全体が中かっこで囲まれた) 1 つまたは複数のログイン モジュール固有のエントリから構成されます。 それぞれの構成ファイル エントリはセミコロンで終了します。

ドライバーは、ログイン モジュール構成ファイルに指定された設定を使用して Kerberos 資格情報を取得できることに加え、既存の資格情報を使用できます。 これは、アプリケーションでユーザーの資格情報を複数使用して接続を作成する必要がある場合に便利です。

ドライバーは、指定されたログイン モジュールを使用してログインを試行する前に、既存の資格情報を使用できる場合はそれを使用します。 したがって、特定のコンテキストで `Subject.doAs` メソッドを使用してコードを実行した場合、`Subject.doAs` 呼び出しに渡された資格情報を使用して接続が作成されます。

詳しくは、「[JAAS Login Configuration File](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html)」(JAAS ログイン構成ファイル) および「[Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)」(Krb5LoginModule クラス) をご覧ください。

Microsoft JDBC Driver 6.2 以降では、必要に応じて、接続プロパティ `jaasConfigurationName` を使用してログイン モジュール構成ファイルの名前を渡すことができます。これにより、各接続に独自のログイン構成を指定できます。

## <a name="creating-a-kerberos-configuration-file"></a>Kerberos 構成ファイルの作成

Kerberos の構成ファイルについて詳しくは、「[Kerberos Requirements](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)」(Kerberos の要件) をご覧ください。

サンプル ドメイン構成ファイルの例を次に示します。ここで、YYYY および ZZZZ は、ドメイン名です。

```ini
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  

[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  

[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  

        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  

```

## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>ドメイン構成ファイルおよびログイン モジュール構成ファイルの有効化

ドメイン構成ファイルを有効にするには、-Djava.security.krb5.conf を使用します。 ログイン モジュール ファイルを有効にするには、 **-Djava.security.auth.login.config** を使用します。

たとえば、次のコマンドを使用してアプリケーションを起動できます。

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Kerberos を介して SQL Server にアクセスできることを確認する

SQL Server Management Studio で次のクエリを実行します。

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

このクエリを実行するために必要な権限があることを確認してください。

## <a name="constrained-delegation"></a>制約付き委任

Microsoft JDBC Driver 6.2 以降では、ドライバーによって Kerberos の制約付き委任がサポートされています。 委任された資格情報は、org.ietf.jgss.GSSCredential オブジェクトとして渡すことができます。これらの資格情報は、接続を確立するためにドライバーによって使用されます。

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>プリンシパル名とパスワードを使用した Kerberos 接続

Microsoft JDBC Driver 6.2 以降では、ドライバーによって、接続文字列で渡されたプリンシパル名とパスワードを使用して Kerberos 接続を確立できます。

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

krb5.conf ファイルで設定されている default_realm にユーザーが属している場合、username プロパティには REALM は必要ありません。 `userName` と `password` が `integratedSecurity=true;` プロパティおよび `authenticationScheme=JavaKerberos;` プロパティと共に設定されている場合は、指定されたパスワードと共に Kerberos プリンシパルとしての userName の値を使用して、接続が確立されます。

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>同じドメインの Unix コンピューターからの Kerberos 認証の使用

このガイドは、動作中の Kerberos セットアップが既に存在することを前提としています。 これが存在することを確認するには、動作中の Kerberos 認証を使用して、Windows コンピューターで次のコードを実行します。 存在する場合は、このコードによって "Authentication Scheme:KERBEROS" がコンソールに出力されます。 追加の実行時フラグ、依存関係、またはドライバー設定は、指定されているもの以外には必要ありません。 Linux で同じコード ブロックを実行して、接続が成功したかどうかを確認できます。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. ドメイン クライアント コンピューターをサーバーと同じドメインに参加させます。
2. (省略可能) 既定の Kerberos チケットの場所を設定します。 そのための最も簡単な方法としては、`KRB5CCNAME` 環境変数を設定します。
3. 既定の Kerberos チケットの場所に新しい Kerberos チケットを生成するか、または既存のものを配置することによって、Kerberos チケットを取得します。 チケットを生成するには、単にターミナルを使用し、`kinit USER@DOMAIN.AD` を使用してチケットを初期化します ("USER" と "DOMAIN.AD" は、それぞれプリンシパルとドメインです)。 例: `kinit SQL_SERVER_USER03@MICROSOFT.COM`。 チケットは、既定のチケットの場所、または `KRB5CCNAME` パス (設定されている場合) に生成されます。
4. ターミナルでパスワードの入力を求められたら、パスワードを入力します。
5. `klist` を使用してチケット内の資格情報を確認し、資格情報が認証に使用するものであることを確認します。
6. 上記のサンプル コードを実行し、Kerberos 認証が成功したことを確認します。

## <a name="see-also"></a>関連項目

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)