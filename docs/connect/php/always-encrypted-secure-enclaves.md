---
title: PHP Drivers でのセキュリティで保護されたエンクレーブが設定された Always Encrypted
description: Microsoft Drivers for PHP for SQL Server でセキュア エンクレーブが設定された Always Encrypted を使用する方法について説明します。
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: ''
ms.author: v-daenge
author: David-Engel
ms.openlocfilehash: c49d81783f82c41cd95e25b137807b006e5b2ad1
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464708"
---
# <a name="using-always-encrypted-with-secure-enclaves-with-the-php-drivers-for-sql-server"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を SQL Server 用 PHP ドライバーと共に使用する

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>適用対象

- Microsoft SQL Server 用 Drivers 5.8.0 for PHP

## <a name="introduction"></a>はじめに

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) は、SQL Server 用 Always Encrypted 機能の 2 回目のイテレーションです。 セキュリティで保護されたエンクレーブが設定された Always Encrypted を利用すると、ユーザーは、セキュリティ エンクレーブ (計算が実行できるようにデータベース内の暗号化されたデータが複合される、サーバー上のメモリの領域) を作成することで、暗号化されたデータに対して優れた計算を実行できます。 サポートされる操作には、`LIKE` 句を使用した比較とパターン マッチングが含まれます。

## <a name="enabling-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする

セキュリティで保護されたエンクレーブが設定された Always Encrypted のサポートは、SQL Server 用 PHP ドライバー 5.8.0 以降で利用可能です。 セキュリティで保護されたエンクレーブが設定された Always Encrypted では、SQL Server 2019 以降と ODBC ドライバーのバージョン 17.4 以降が必要になります。 SQL Server 用 PHP ドライバーを利用する Always Encrypted の一般的な要件の詳細については、[こちら](using-always-encrypted-php-drivers.md)で確認できます。

セキュリティで保護されたエンクレーブが設定された Always Encrypted では、エンクレーブを証明する (つまり、外部の構成証明サービスに対してエンクレーブの検証を行う) ことによって、暗号化されたデータのセキュリティが保証されます。 セキュリティ保護されたエンクレーブを使用するには、`ColumnEncryption` キーワードでは、コンマで区切られた状態で、関連する構成証明データと共に構成証明の種類とプロトコルが識別される必要があります。 ODBC ドライバーのバージョン 17.4 では、エンクレーブの種類とプロトコルに対して、仮想化ベースのセキュリティ (VBS) とホスト ガーディアン サービス (HGS) プロトコルのみがサポートされます。 関連付けられている構成証明データは、構成証明サーバーの URL です。 このため、接続文字列には以下の設定が追加されます。

```
ColumnEncryption=VBS-HGS,http://attestationserver.mydomain/Attestation
```

プロトコルが正しくない場合は、ドライバーに認識されず、接続が失敗してエラーが返されます。 構成証明 URL のみが正しくない場合は、接続は成功し、エンクレーブが有効化された計算が試行されるとエラーがスローされますが、それ以外の場合、動作は元の Always Encrypted の動作と同じです。 `ColumnEncryption` を `enabled` に設定すると、通常の Always Encrypted 機能が提供されますが、エンクレーブが有効化された操作を試行すると、エラーが返されます。

ホスト ガーディアン サービスの設定や必要な暗号化キーの作成など、セキュリティで保護されたエンクレーブが設定された Always Encrypted をサポートするように環境を構成する方法の詳細については、[こちら](../../relational-databases/security/encryption/configure-always-encrypted-enclaves.md)で確認できます。

## <a name="examples"></a>例

1 つは SQLSRV 用、もう 1 つは PDO_SQLSRV 用を示した次の例では、プレーンテキスト内に複数のデータ型が含まれるテーブルを作成し、暗号化して、比較とパターン マッチングを実行します。 次の詳細に注意します。

- `ALTER TABLE` を使用してテーブルを暗号化する場合、`ALTER TABLE` の呼び出しごとに 1 つの列しか暗号化できないため、複数の列を暗号化するには複数回の呼び出しが必要になります。
- char 型と nchar 型を比較する場合にパラメーターとして比較のしきい値を渡すときは、対応する `SQLSRV_SQLTYPE_*` 内に列幅を指定する必要があります。そうしないと、エラー `HY104`、`Invalid precision value` が返されます。
- パターン マッチングでは、`COLLATE` 句を使用して、照合順序が `Latin1_General_BIN2` として指定される必要があります。
- char 型と nchar 型では文字列の末尾が空白で埋められるので、char 型と nchar 型を照合するためにパターン マッチングの文字列をパラメーターとして渡すときは、`sqlsrv_query` または `sqlsrv_prepare` に渡される `SQLSRV_SQLTYPE_*` には、列のサイズではなく、照合される文字列の長さを指定する必要があります。 たとえば、文字列 `%abc%` を char(10) 列に対して照合する場合は、`SQLSRV_SQLTYPE_CHAR(5)` を指定します。 代わりに `SQLSRV_SQLTYPE_CHAR(10)` を指定すると、クエリでは `%abc%     ` (5 つのスペースが追加されている状態) と照合して、5 個未満のスペースが追加されている列のデータはすべて、一致しなくなります (つまり、`abcdef` には 4つのスペースが埋め込まれているため、`%abc%` とは一致しません)。 Unicode 文字列の場合は、`mb_strlen` 関数または `iconv_strlen` 関数を使用して、文字数を取得します。
- PDO インターフェイスでは、パラメーターの長さを指定することはできません。 代わりに、`PDOStatement::bindParam` に長さ 0 または `null` を指定します。 長さに明示的に別の数値が設定されている場合、パラメーターは出力パラメーターとして処理されます。
- Always Encrypted での文字列以外の型に対しては、パターン マッチングは機能しません。
- わかりやすくするために、エラー チェックは除外されています。

次のデータは、両方の例に共通です。

```php
<?php
// Data for testing - integer, datetime2, char, nchar, varchar, and nvarchar
// String data is random, showing that we can match or compare anything
$testValues = array(array(1, "2019-12-31 01:00:00", "abcd", "㬚㔈♠既", "abcd", "㬚㔈♠既"),
                    array(-100, "1753-01-31 14:25:25.25", "#e@?q&zy+", "ઔܛ᎓Ե⅜", "#e@?q&zy+", "ઔܛ᎓Ե⅜"),
                    array(100, "2112-03-15 23:40:10.1594", "zyxwv", "㶋㘚ᐋꗡ", "zyxwv", "㶋㘚ᐋꗡ"),
                    array(0, "8888-08-08 08:08:08.08", "7t", "㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ", "7t", "㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ"),
                    );

// Queries to create the table and insert data
$createTable = "DROP TABLE IF EXISTS $myTable; 
                CREATE TABLE $myTable (c_integer int NULL, 
                                       c_datetime2 datetime2(7) NULL, 
                                       c_char char(32) NULL, 
                                       c_nchar nchar(32) NULL, 
                                       c_varchar varchar(32) NULL, 
                                       c_nvarchar nvarchar(32) NULL);";
$insertData = "INSERT INTO $myTable (c_integer, c_datetime2, c_char, c_nchar, c_varchar, c_nvarchar) VALUES (?, ?, ?, ?, ?, ?)";

// This is the query that encrypts the table in place
$encryptQuery = " ALTER TABLE $myTable
                      ALTER COLUMN [c_integer] integer
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_datetime2] datetime2(7)
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_char] char(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_nchar] nchar(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_varchar] varchar(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_nvarchar] nvarchar(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;";
?>
```

### <a name="sqlsrv"></a>SQLSRV

```php
<?php
// Specify Azure Key Vault credentials using the KeyStoreAuthentication, KeyStorePrincipalId, and KeyStoreSecret keywords
// Otherwise, the local Windows Certificate Store will be used
$options = array('database'=>$myDatabase,
                 'uid'=>$myUsername,
                 'pwd'=>$myPassword,
                 'CharacterSet'=>'UTF-8',
                 'ReturnDatesAsStrings'=>true,
                 'ColumnEncryption'=>"VBS-HGS,http://myattestationserver.mydomain/Attestation",
                 );
                 
$conn = sqlsrv_connect($myServer, $options);

// Create the table and insert the test data
$stmt = sqlsrv_query($conn, $createTable);

foreach ($testValues as $values) {
    $stmt = sqlsrv_prepare($conn, $insertData, $values);
    sqlsrv_execute($stmt);
}

// Encrypt the table in place
$stmt = sqlsrv_query($conn, $encryptQuery);

// Test comparison and pattern matching on the encrypted table
echo "Test comparisons:\n";

$intThreshold = 0;
$testGreater = "SELECT c_integer FROM $myTable WHERE c_integer > ?";
$param = array($intThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_INT);
$stmt = sqlsrv_prepare($conn, $testGreater, array($param));
getResults($stmt);
// Expect:
// 1
// 100

$datetimeThreshold = "3000-01-01 00:00:00.0";
$testLess = "SELECT c_datetime2 FROM $myTable WHERE c_datetime2 < ?";
$param = array($datetimeThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_DATETIME2);
$stmt = sqlsrv_prepare($conn, $testLess, array($param));
getResults($stmt);
// Expect:
// 2019-12-31 01:00:00.0000000
// 1753-01-31 14:25:25.2500000
// 2112-03-15 23:40:10.1594000

$charThreshold = "abcd";
$ncharThreshold = "㬚㔈♠既";

$testGreaterEqual = "SELECT c_char FROM $myTable WHERE c_char >= ?";
$param = array($charThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_CHAR(32));
$stmt = sqlsrv_prepare($conn, $testGreaterEqual, array($param));
getResults($stmt);
// Expect:
// abcd                            
// zyxwv                           

$testLessEqual = "SELECT c_nchar FROM $myTable WHERE c_nchar <= ?";
$param = array($ncharThreshold, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING('UTF-8'), SQLSRV_SQLTYPE_NCHAR(32));
$stmt = sqlsrv_prepare($conn, $testLessEqual, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// ઔܛ᎓Ե⅜                           
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$testNotGreater = "SELECT c_varchar FROM $myTable WHERE c_varchar !> ?";
$param = array($charThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_VARCHAR);
$stmt = sqlsrv_prepare($conn, $testNotGreater, array($param));
getResults($stmt);
// Expect:
// abcd
// #e@?q&zy+
// 7t

$testNotLess = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar !< ?";
$param = array($ncharThreshold, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING('UTF-8'), SQLSRV_SQLTYPE_NVARCHAR);
$stmt = sqlsrv_prepare($conn, $testNotLess, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㶋㘚ᐋꗡ

echo "\nTest pattern matching:\n";

$charMatch = "%zy%";
$ncharMatch = "%㔈♠既%";

$param = array($charMatch, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_CHAR(strlen($charMatch)));
$testCharMatch = "SELECT c_char FROM $myTable WHERE c_char LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testCharMatch, array($param));
getResults($stmt);
// Expect:
// #e@?q&zy+                       
// zyxwv                           

$param = array($ncharMatch, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING("UTF-8"), SQLSRV_SQLTYPE_NCHAR(iconv_strlen($ncharMatch)));
$testNCharMatch = "SELECT c_nchar FROM $myTable WHERE c_nchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testNCharMatch, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$param = array($charMatch, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_VARCHAR(strlen($charMatch)));
$testVarcharMatch = "SELECT c_varchar FROM $myTable WHERE c_varchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testVarcharMatch, array($param));
getResults($stmt);
// Expect:
// #e@?q&zy+
// zyxwv

$param = array($ncharMatch, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING("UTF-8"), SQLSRV_SQLTYPE_NVARCHAR(iconv_strlen($ncharMatch)));
$testNVarcharMatch = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testNVarcharMatch, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ

function getResults($stmt)
{
    sqlsrv_execute($stmt);
    while ($res = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_NUMERIC)) {
        print_r($res[0]);
        echo "\n";
    }
}
?>
```

### <a name="pdo_sqlsrv"></a>PDO_SQLSRV

```php
<?php
// Specify Azure Key Vault credentials using the KeyStoreAuthentication, KeyStorePrincipalId, and KeyStoreSecret keywords
// Otherwise, the local Windows Certificate Store will be used
$options = "sqlsrv:server=$myServer;database=$myDatabase;driver={ODBC Driver 17 for SQL Server};";
$options .= "ColumnEncryption=VBS-HGS,http://myattestationserver.mydomain/Attestation",

$conn = new PDO($options, $myUsername, $myPassword);

// Create the table and insert the test data
$stmt = $conn->query($createTable);

foreach ($testValues as $values) {
    $stmt = $conn->prepare($insertData);
    $stmt->execute($values);
}

// Encrypt the table in place
$stmt = $conn->query($encryptQuery);

// Test comparison and pattern matching on the encrypted table
echo "Test comparisons:\n";

$intThreshold = 0;
$testGreater = "SELECT c_integer FROM $myTable WHERE c_integer > ?";
$stmt = $conn->prepare($testGreater);
$stmt->bindParam(1, $intThreshold, PDO::PARAM_INT);
getResults($stmt);
// Expect:
// 1
// 100

$datetimeThreshold = "3000-01-01 00:00:00.0";
$testLess = "SELECT c_datetime2 FROM $myTable WHERE c_datetime2 < ?";
$stmt = $conn->prepare($testLess);
$stmt->bindParam(1, $datetimeThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// 2019-12-31 01:00:00.0000000
// 1753-01-31 14:25:25.2500000
// 2112-03-15 23:40:10.1594000

$charThreshold = "abcd";
$ncharThreshold = "㬚㔈♠既";

$testGreaterEqual = "SELECT c_char FROM $myTable WHERE c_char >= ?";
$stmt = $conn->prepare($testGreaterEqual);
$stmt->bindParam(1, $charThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// abcd                            
// zyxwv                           

$testLessEqual = "SELECT c_nchar FROM $myTable WHERE c_nchar <= ?";
$stmt = $conn->prepare($testLessEqual);
$stmt->bindParam(1, $ncharThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// ઔܛ᎓Ե⅜                           
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$testNotGreater = "SELECT c_varchar FROM $myTable WHERE c_varchar !> ?";
$stmt = $conn->prepare($testNotGreater);
$stmt->bindParam(1, $charThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// abcd
// #e@?q&zy+
// 7t

$testNotLess = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar !< ?";
$stmt = $conn->prepare($testNotLess);
$stmt->bindParam(1, $ncharThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㶋㘚ᐋꗡ

echo "\nTest pattern matching:\n";

$charMatch = "%zy%";
$ncharMatch = "%㔈♠既%";

$testCharMatch = "SELECT c_char FROM $myTable WHERE c_char LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testCharMatch);
$stmt->bindParam(1, $charMatch, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// #e@?q&zy+                       
// zyxwv                           

$testNCharMatch = "SELECT c_nchar FROM $myTable WHERE c_nchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testNCharMatch);
$stmt->bindParam(1, $ncharMatch, PDO::PARAM_STR,null,PDO::SQLSRV_ENCODING_UTF8);
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$testVarcharMatch = "SELECT c_varchar FROM $myTable WHERE c_varchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testVarcharMatch);
$stmt->bindParam(1, $charMatch, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// #e@?q&zy+
// zyxwv

$testNVarcharMatch = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testNVarcharMatch);
$stmt->bindParam(1, $ncharMatch, PDO::PARAM_STR,null,PDO::SQLSRV_ENCODING_UTF8);
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ

function getResults($stmt)
{
    $stmt->execute();
    while($res = $stmt->fetch(PDO::FETCH_NUM)) {
        print_r($res[0]);
        echo "\n";
    }
}
?>
```

出力:

```
Test comparisons:
1
100
2019-12-31 01:00:00.0000000
1753-01-31 14:25:25.2500000
2112-03-15 23:40:10.1594000
abcd                            
zyxwv                           
㬚㔈♠既                            
ઔܛ᎓Ե⅜                           
㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    
abcd
#e@?q&zy+
7t
㬚㔈♠既
㶋㘚ᐋꗡ

Test pattern matching:
#e@?q&zy+                       
zyxwv                           
㬚㔈♠既                            
㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    
#e@?q&zy+
zyxwv
㬚㔈♠既
㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ
```

## <a name="see-also"></a>参照

[プログラミング ガイド](programming-guide-for-php-sql-driver.md)  
[SQLSRV ドライバー API リファレンス](sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV ドライバー API リファレンス](pdo-sqlsrv-driver-reference.md)  
[SQL Server 用 PHP ドライバーと共に Always Encrypted を使用する](using-always-encrypted-php-drivers.md)
