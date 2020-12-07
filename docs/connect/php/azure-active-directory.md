---
title: Azure Active Directory
description: Microsoft Drivers for PHP for SQL Server と共に Azure Active Directory 認証を使用する方法について説明します。
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f7abb90d32f93975c9a984670ca450dc791a46ae
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92004559"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 認証を使用して接続する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](/azure/active-directory/active-directory-whatis) (Azure AD) は、[SQL Server 認証](how-to-connect-using-sql-server-authentication.md)の代替手段として機能する、集中ユーザー ID 管理テクノロジです。 Azure AD を使用すると、ユーザー名とパスワード、Windows 統合認証、または Azure AD アクセス トークンを使用して、Azure AD のフェデレーション ID で、Microsoft Azure SQL Database と Azure Synapse Analytics に接続できます。 SQL Server 用の PHP ドライバーでは、これらの機能が部分的にサポートされます。

Azure AD を使用するには、次の表で示すように、**Authentication** または **AccessToken** キーワードを使用します (どちらか一方)。 技術的な詳細については、「[ODBC ドライバーでの Azure Active Directory の使用](../odbc/using-azure-active-directory.md)」をご覧ください。

|Keyword|値|説明|
|-|-|-|
|**AccessToken**|非設定 (既定値)|他のキーワードによって決定される認証モード。 詳細については、「 [Connection Options](connection-options.md)」を参照してください。 |
||バイト文字列|OAuth JSON の応答から抽出された Azure AD アクセス トークン。 接続文字列に、ユーザー ID、パスワード、または Authentication キーワードを含めることはできません (Linux または macOS では、ODBC Driver バージョン 17 以降が必要です)。 |
|**認証**|非設定 (既定値)|他のキーワードによって決定される認証モード。 詳細については、「 [Connection Options](connection-options.md)」を参照してください。 |
||`SqlPassword`|ユーザー名とパスワードを使用して、SQL Server インスタンス (Azure インスタンスである可能性があります) に対して直接認証を行います。 **UID** と **PWD** キーワードを使用して、ユーザー名とパスワードを接続文字列に渡す必要があります。 |
||`ActiveDirectoryPassword`|ユーザー名とパスワードを使用して、Azure Active Directory の ID で認証を行います。 **UID** と **PWD** キーワードを使用して、ユーザー名とパスワードを接続文字列に渡す必要があります。 |
||`ActiveDirectoryMsi`|システム割り当てのマネージド ID またはユーザー割り当てのマネージド ID を使用して、認証を行います (ODBC ドライバー バージョン 17.3.1.1 以降が必要です)。 概要とチュートリアルについては、「[Azure リソースのマネージド ID とは](/azure/active-directory/managed-identities-azure-resources/overview)」を参照してください。|

**Authentication** キーワードは、接続のセキュリティ設定に影響します。 それが接続文字列で設定されている場合、既定で **Encrypt** キーワードが true に設定されます。これは、クライアントが暗号化を要求することを意味します。 さらに、**TrustServerCertificate** が true に設定されていない限り (既定では **false**)、暗号化の設定に関係なくサーバー証明書が検証されます。 この機能は、接続文字列で暗号化が明示的に要求されている場合にのみサーバー証明書が検証される、セキュリティが劣る古いログイン方法とは異なります。

#### <a name="limitations"></a>制限事項

Windows では、基になる ODBC ドライバーで **Authentication** キーワードに対してもう 1 つの値 **ActiveDirectoryIntegrated** がサポートされていますが、PHP ドライバーではこの値はどのプラットフォームでもサポートされていません。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>例 - SqlPassword と ActiveDirectoryPassword を使用して接続する

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdo_sqlsrv-driver"></a>例 - PDO_SQLSRV ドライバーを使用して接続する

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>例 - Azure AD アクセス トークンを使用して接続する

### <a name="sqlsrv-driver"></a>SQLSRV ドライバー

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdo_sqlsrv-driver"></a>PDO_SQLSRV ドライバー

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>例 - Azure リソースのマネージド ID を使用して接続する

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>SQLSRV ドライバーでシステム割り当てのマネージド ID を使用する

システム割り当てのマネージド ID を使用して接続する場合は、UID または PWD オプションを使用しないでください。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdo_sqlsrv-driver"></a>PDO_SQLSRV ドライバーでユーザー割り当てのマネージド ID を使用する

ユーザー割り当てマネージド ID は、スタンドアロン Azure リソースとして作成されます。 使用中のサブスクリプションで信頼されている Azure AD テナントに、Azure によって ID が作成されます。 作成された ID は、1 つまたは複数の Azure サービス インスタンスに割り当てることができます。 この ID の `Object ID` をコピーし、接続文字列のユーザー名として設定します。 

そのため、ユーザー割り当てのマネージド ID を使用して接続するときは、ユーザー名としてオブジェクト ID を指定しますが、パスワードは省略します。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>参照
[ODBC ドライバーでの Azure Active Directory の使用](../odbc/using-azure-active-directory.md)

[Azure リソースのマネージド ID とは](/azure/active-directory/managed-identities-azure-resources/overview)