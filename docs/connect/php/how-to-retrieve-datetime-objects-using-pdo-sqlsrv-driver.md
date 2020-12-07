---
title: '方法: PDO_SQLSRV ドライバーを使用して日付型と時刻型を PHP DateTime オブジェクトとして取得する'
description: このトピックでは、Microsoft PDO_SQLSRV Driver for PHP for SQL Server の使用時、日付型と時刻型を PHP DateTime オブジェクトとして取得する方法について説明します
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 507dc2a228419fb695d10a437681229ec6586f11
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680757"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdo_sqlsrv-driver"></a>方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

バージョン 5.6.0 で追加されたこの機能は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の PDO_SQLSRV ドライバーの利用時にのみ有効です。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>DateTime オブジェクトとして日付と時刻の型を取得するには

PDO_SQLSRV の利用時、日付と時刻の型 (**smalldatetime**、**datetime**、**date**、**time**、**datetime2**、**datetimeoffset**) は既定で文字列として返されます。 PDO::ATTR_STRINGIFY_FETCHES 属性と PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 属性のどちらにも効力がありません。 [PHP DateTime](http://php.net/manual/en/class.datetime.php) オブジェクトとして日付と時刻の型を取得するには、接続またはステートメント属性 `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` を **true** に設定します (既定では **false**)。

> [!NOTE]
> DateTime オブジェクトは出力パラメーターとして指定できないため、この接続またはステートメント属性は、日付/時刻型の通常のフェッチにのみ適用されます。

## <a name="example---use-the-connection-attribute"></a>例 - 接続属性の使用
次の例では、わかりやすくするため、エラー チェックを省略しています。 この例からは、接続属性の設定方法がわかります。

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>例 - ステートメント属性の使用
この例からは、ステートメント属性の設定方法がわかります。

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>例 - ステートメント オプションの使用
代わりに、ステートメント属性をオプションとして設定できます。

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>例 - 文字列として datetime 型を取得する
次の例からは、逆に変換する方法がわかります (既定では false であるため、これは実際には不要です)。

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>参照
[データの取得](../../connect/php/retrieving-data.md)

[SQLSRV ドライバーを使用して日付/時刻型を文字列として取得する](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)
