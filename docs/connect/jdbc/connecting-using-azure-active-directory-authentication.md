---
title: Azure Active Directory 認証を利用した接続
description: Microsoft JDBC Driver for SQL Server で Azure Active Directory 認証機能を使用する Java アプリケーションを開発する方法について説明します。
ms.custom: ''
ms.date: 09/23/2020
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf829dfabdd291367990ef21280208ac0741154c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081311"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Azure Active Directory 認証を利用した接続

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事には、Microsoft JDBC Driver for SQL Server で Azure Active Directory 認証機能を使用する Java アプリケーションの開発方法に関する情報が記載されています。

Azure Active Directory の ID を使用して Azure SQL Database v12 に接続するメカニズムである、Azure Active Directory (Azure AD) 認証を使用できます。 Azure Active Directory 認証は、データベース ユーザーの ID を一元管理するという目的で使用でき、SQL Server 認証に代わる方法となります。 JDBC Driver では、Azure Active Directory の資格情報を JDBC 接続文字列に指定して、Azure SQL Database に接続することができます。 Azure Active Directory 認証を構成する方法については、[Azure Active Directory 認証を使用した SQL Database への接続](/azure/azure-sql/database/authentication-aad-overview)に関するページを参照してください。 

Microsoft JDBC Driver for SQL Server で Azure Active Directory 認証をサポートする接続プロパティは次のとおりです。
*   **authentication**:このプロパティを使用して、接続に使用する SQL 認証方法を指定します。 次のいずれかの値になります。 
    * **ActiveDirectoryMSI**
        * ドライバー バージョン **v7.2** 以降でサポートされています。`authentication=ActiveDirectoryMSI` を使用して、"ID" サポートが有効になっている Azure リソース内から Azure SQL Database および Data Warehouse に接続することができます。 必要に応じて、この認証モードと共に、**msiClientId** を Connection または DataSource プロパティで指定することもできます。これには、接続を確立するための **accessToken** を取得するために使用される、マネージド ID のクライアント ID が含まれている必要があります。
    * **ActiveDirectoryIntegrated**
        * ドライバー バージョン **v6.0** 以降でサポートされています。`authentication=ActiveDirectoryIntegrated` を使用し、統合認証を使って Azure SQL Database および Data Warehouse に接続することができます。 この認証モードを使用するには、オンプレミスの Active Directory フェデレーション サービス (ADFS) をクラウドの Azure Active Directory とフェデレーションする必要があります。 これが設定されたら、Windows OS のアプリケーション クラス パスにネイティブ ライブラリ 'mssql-jdbc_auth-\<version>-\<arch>.dll' を追加するか、クロスプラットフォーム認証されるよう Kerberos チケットを設定します。 ドメインに参加しているマシンにログインしているときに、資格情報の入力を求められることなく、Azure SQL Database と Azure Synapse Analytics にアクセスできるようになります。
    * **ActiveDirectoryPassword**
        * ドライバー バージョン **v6.0** 以降でサポートされています。`authentication=ActiveDirectoryPassword` を使用し、Azure AD ユーザー名とパスワードを使って Azure SQL Database および Data Warehouse に接続することができます。
    * **SqlPassword**
        * `authentication=SqlPassword` を使用し、userName または user および password プロパティを使って SQL Server に接続します。
    * **NotSpecified**
        * これらの認証方法が不要な場合は、`authentication=NotSpecified` を使用するか、既定値のままにしておきます。

*   **accessToken**:この接続プロパティを使用し、アクセス トークンを使って SQL Database に接続します。 accessToken は、DriverManager クラスの getConnection () メソッドの Properties パラメーターを使用してのみ設定できます。 接続 URL では使用できません。  

詳細については、「[接続プロパティの設定](setting-the-connection-properties.md)」ページの認証プロパティを参照してください。  


## <a name="client-setup-requirements"></a>クライアント設定の要件
**ActiveDirectoryMSI** 認証の場合、以下のコンポーネントをクライアント コンピューターにインストールする必要があります。
* Java 8 以上
* SQL Server 用 Microsoft JDBC Driver 7.2 (またはそれ以降)
* クライアント環境は Azure リソースである必要があり、"ID" 機能のサポートが有効になっている必要があります。
* Azure リソースのシステム割り当て済みマネージド ID またはユーザー割り当て済みマネージド ID、あるいはマネージド ID が属しているグループのいずれかを表す包含データベース ユーザーは、ターゲット データベースに存在する必要があり、CONNECT 権限を持っている必要があります。

その他の認証モードの場合は、以下のコンポーネントをクライアント コンピューターにインストールする必要があります。
* Java 7 以上
* SQL Server 用 Microsoft JDBC Driver 6.0 (またはそれ以降)
* アクセス トークン ベースの認証モードを使用する場合に、この記事の例を実行するには、[azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) とその依存関係が必要です。 詳細については、「**アクセス トークンを使用した接続**」セクションを参照してください。
* **ActiveDirectoryPassword** 認証モードを使用する場合は、[azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) とその依存関係が必要です。 詳細については、「**ActiveDirectoryPassword 認証モードを使用した接続**」セクションを参照してください。
* **ActiveDirectoryIntegrated** モードを使用する場合は、azure-activedirectory-library-for-java とその依存関係が必要です。 詳細については、「**ActiveDirectoryIntegrated 認証モードを使用した接続**」セクションを参照してください。

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>ActiveDirectoryMSI 認証モードを使用した接続
次の例では、`authentication=ActiveDirectoryMSI` モードの使用方法を示します。 この例は、Azure リソース (Azure Virtual Machine、App Service、または Azure Active Directory とフェデレーションされている Function App など) 内から実行します。

例を実行する前に、以下の行のサーバーとデータベースの名前を、ご利用のサーバーとデータベースの名前に置き換えます。

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMSIClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned Managed Identity to be used
```

ActiveDirectoryMSI 認証モードを使用する例:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned Managed Identity to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Azure Virtual Machine でこの例を実行すると、"_システム割り当てマネージド ID_" または "_ユーザー割り当てマネージド ID_" (**msiClientId** が指定されている場合) からアクセス トークンがフェッチされ、フェッチされたアクセス トークンを使用して接続が確立されます。 接続が確立された場合は、次のメッセージが表示されるはずです。

```bash
You have successfully logged on as: <your Managed Identity username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>ActiveDirectoryIntegrated 認証モードを使用した接続
バージョン 6.4 では、Microsoft JDBC Driver によって、複数のプラットフォーム (Windows、Linux、および macOS) で Kerberos チケットを使用した ActiveDirectoryIntegrated 認証のサポートが追加されています。
詳細については、「[Windows、Linux、macOS で Kerberos チケットを設定する](#set-kerberos-ticket-on-windows-linux-and-macos)」をご覧ください。 また、Windows では、JDBC ドライバーを使用した ActiveDirectoryIntegrated 認証に mssql-jdbc_auth-\<version>-\<arch>.dll を使用することもできます。

> [!NOTE]
>  古いバージョンのドライバーを使う場合は、こちらの[リンク](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)で、この認証モードを使用するために必要な該当する依存関係を確認してください。 

次の例では、`authentication=ActiveDirectoryIntegrated` モードの使用方法を示します。 Azure Active Directory とフェデレーションされているドメインに参加しているコンピューターで、この例を実行します。 Azure AD ユーザーを表す包含データベース ユーザー、または属しているグループの 1 つがデータベースに存在している必要があり、CONNECT 権限を持っている必要があります。 

例をビルドして実行する前に、(例を実行する) クライアント コンピューターに、[azure-activedirectory-library-for-java ライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java) とその依存関係をダウンロードし、それらを Java ビルド パスに含めます

例を実行する前に、以下の行のサーバーとデータベースの名前を、ご利用のサーバーとデータベースの名前に置き換えます。

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

ActiveDirectoryIntegrated 認証モードを使用する例:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

クライアント コンピューターでこの例を実行すると、Kerberos チケットが自動的に使用され、パスワードは必要ありません。 接続が確立された場合は、次のメッセージが表示されるはずです。

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-macos"></a>Windows、Linux、macOS で Kerberos チケットを設定する

現在のユーザーを Windows ドメイン アカウントにリンクする Kerberos チケットを設定する必要があります。 主な手順の概要を以下に示します。

#### <a name="windows"></a>Windows
JDK には `kinit` が付属しています。これを使用して、Azure Active Directory とフェデレーションされているドメインに参加しているコンピューター上のキー配布センター (KDC) から TGT を取得することができます。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>手順 1:チケット保証チケットの取得
- **実行対象**:Windows
- **アクション**:
  - コマンド `kinit username@DOMAIN.COMPANY.COM` を使用して KDC から TGT を取得する場合、ドメイン パスワードの入力を求めるメッセージが表示されます。
  - `klist` を使用して、利用可能なチケットを確認します。 kinit が正常に実行された場合は、krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM からのチケットが表示されるはずです。

> [!NOTE]
>  アプリケーションで KDC を検索する場合は、`-Djava.security.krb5.conf` での `.ini` ファイルの指定が必要になる場合があります。

#### <a name="linux-and-macos"></a>Linux と macOS

##### <a name="requirements"></a>必要条件
Kerberos ドメイン コントローラーのクエリを実行するための、Windows ドメインに参加しているコンピューターへのアクセス権。

##### <a name="step-1-find-kerberos-kdc"></a>手順 1:Kerberos KDC を検索する
- **実行対象**:Windows コマンド ライン
- **アクション**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (この "DOMAIN.COMPANY.COM" はご利用のドメイン名にマップされます)
- **サンプル出力**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **抽出される情報**: DC 名。この場合は `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>手順 2:krb5.conf での KDC の構成
- **実行対象**:Linux/macOS
- **アクション**:任意のエディターで /etc/krb5.conf を編集します。 次のキーを構成します。
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  次に、krb5.conf ファイルを保存して終了します。

> [!NOTE]
>  ドメインはすべて大文字にする必要があります。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>手順 3:チケット保証チケットの取得のテスト
- **実行対象**:Linux/macOS
- **アクション**:
  - コマンド `kinit username@DOMAIN.COMPANY.COM` を使用して KDC から TGT を取得する場合、ドメイン パスワードの入力を求めるメッセージが表示されます。
  - `klist` を使用して、利用可能なチケットを確認します。 kinit が正常に実行された場合は、krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM からのチケットが表示されるはずです。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>ActiveDirectoryPassword 認証モードを使用した接続
次の例では、`authentication=ActiveDirectoryPassword` モードの使用方法を示します。

例をビルドして実行する前に、次のようにします。
1.  (例を実行する) クライアント コンピューターに、[azure-activedirectory-library-for-java ライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java)とその依存関係をダウンロードし、それらを Java ビルド パスに含めます
2.  次のコード行を見つけて、サーバーとデータベースの名前を、実際のサーバーとデータベースの名前に置き換えます。
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  次のコード行を見つけて、ユーザー名を、接続する場合に使用する Azure AD ユーザーの名前に置き換えます。
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

ActiveDirectoryPassword 認証モードを使用する例:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
接続が確立された場合、出力として次のメッセージが表示されるはずです。
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含ユーザー データベースが存在している必要あり、指定された Azure AD ユーザー、または指定された Azure AD ユーザーが属しているグループの 1 つを表す包含データベース ユーザーが、データベースに存在している必要があり、CONNECT 権限を持っている必要があります (Azure Active Directory サーバー管理者やグループを除く)

## <a name="connecting-using-access-token"></a>アクセス トークンを使用した接続
アプリケーションとサービスでは、Azure Active Directory からアクセス トークンを取得し、それを使用して Azure SQL Database および Data Warehouse に接続することができます。

> [!NOTE] 
> **accessToken** は、DriverManager クラスの getConnection () メソッドの Properties パラメーターを使用してのみ設定できます。 接続文字列では使用できません。

以下の例には、アクセス トークンベースの認証を使用して、Azure SQL Database および Data Warehouse に接続するシンプルな Java アプリケーションが含まれています。 例をビルドして実行する前に、次の手順を行います。
1.  サービスの Azure Active Directory でアプリケーション アカウントを作成します。
    1. Azure portal にサインインします。
    2. 左側のナビゲーションで、[Azure Active Directory] をクリックします。
    3. [アプリの登録] タブをクリックします。
    4. ドロワーで、[新しいアプリケーションの登録] をクリックします。
    5. アプリケーションのフレンドリ名として「mytokentest」と入力し、[Web アプリ/API] を選択します。
    6. サインオン URL は必要ありません。 何も指定します。 "https://mytokentest" 。
    7. 下部にある [作成] をクリックします。
    9. 引き続き、Azure portal で、アプリケーションの [設定] タブをクリックし、[プロパティ] タブを開きます。
    10. "アプリケーション ID" (クライアント ID ともいう) の値を見つけてコピーしておきます。これは、後でアプリケーションを構成するときに必要です (例: 1846943b-ad04-4808-aa13-4702d908b5c1)。 以下のスナップショットを参照してください。
    11. [キー] セクションで、キーを作成します。その場合、名前フィールドに入力し、キーの期間を選択し、構成を保存します (値フィールドは空のままにします)。 保存後に、値フィールドが自動的に入力されるはずです。生成された値をコピーします。 これがクライアント シークレットです。
    12. 左側のパネルで、[Azure Active Directory] をクリックします。 [アプリの登録] で、[エンド ポイント] タブを見つけます。[OATH 2.0 TOKEN ENDPOINT]\(OATH 2.0 トークン エンドポイント\) の下の URL をコピーします。これが STS URL です。
    
    ![Azure portal のアプリ登録エンド ポイント - STS URL](media/jdbc_aad_token.png)  
2. Azure SQL Server のユーザー データベースに Azure Active Directory 管理者としてサインインし、T-SQL コマンドを使用して、アプリケーション プリンシパルの包含データベース ユーザーをプロビジョニングします。 Azure Active Directory 管理者と包含データベース ユーザーの作成方法に関する詳細については、[Azure Active Directory 認証を使用した SQL Database または Azure Synapse Analytics への接続](/azure/azure-sql/database/authentication-aad-overview)に関する記事を参照してください。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  (例を実行する) クライアント コンピューターに、[azure-activedirectory-library-for-java ライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java) とその依存関係をダウンロードし、それらを Java ビルド パスに含めます。 azure-activedirectory-library-for-java は、この特定の例を実行する場合にのみ必要であることに注意してください。 この例では、このライブラリの API を使用して、Azure AD からアクセス トークンを取得します。 アクセス トークンが既にある場合は、この手順をスキップできます。 また、アクセス トークンを取得する例でセクションを削除する必要もあることに注意してください。

次の例では、STS URL、クライアント ID、クライアント シークレット、サーバー、データベース名を実際の値に置き換えます。

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

接続に成功した場合は、出力として以下のメッセージが表示されるはずです。

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
```