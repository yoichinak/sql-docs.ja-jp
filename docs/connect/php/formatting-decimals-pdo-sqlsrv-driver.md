---
title: 10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)
description: PDO_SQLSRV ドライバーを使用する場合に PDO::SQLSRV_ATTR_FORMAT_DECIMALS と SQLSRV_ATTR_DECIMAL_PLACES 属性を使用して 10 進数または金額の書式設定を行う方法について説明します
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db9392b523be8777a96e4d262cfca5acccc8f406
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726843"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

正確さを維持するため、[decimal 型または numeric 型](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)は、正確な精度と小数点以下桁数の文字列として常にフェッチされます。 値が 1 未満の場合、先頭の 0 はありません。 money フィールドと smallmoney フィールドも、小数点以下桁数が 4 に固定された 10 進数フィールドであるため、これと同じです。

## <a name="add-leading-zeroes-if-missing"></a>先頭に 0 がない場合に追加する
バージョン 5.6.0 以降では、ユーザーは、接続属性またはステートメント属性 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` を使用して、10 進数の文字列の書式を設定できます。 この属性はブール値 (true または false) であり、フェッチされた結果の decimal または numeric の値の書式設定にのみ影響します。 つまり、この属性は挿入や更新などの他の操作には影響しません。

既定では、`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` は **false** です。 true に設定すると、1 未満の 10 進値に対して先頭の 0 が追加されます。

## <a name="configure-number-of-decimal-places"></a>小数点以下の桁数を構成する
`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` をオンにすると、別の接続属性またはステートメント属性 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` を使用して、money および smallmoney のデータを表示するときの小数点以下の桁数を構成できます。 [0, 4] の範囲の整数値を指定でき、表示されるときに丸めが発生する場合があります。 ただし、基になる金額データは変わりません。

接続設定は、対応するステートメント属性によって常にオーバーライドされます。 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` オプションの影響を受けるのは money データ**だけ**であり、`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` を true に設定する必要があることに注意してください。 そうしないと、`PDO::SQLSRV_ATTR_DECIMAL_PLACES` の設定に関係なく、書式設定は無効になります。

> [!NOTE]
> money または smallmoney のフィールドには小数点以下桁数が 4 であるため、`PDO::SQLSRV_ATTR_DECIMAL_PLACES` を負の値または 4 より大きい値に設定すると無視されます。 書式設定された金額データを計算への入力として使用することはお勧めしません。

### <a name="to-set-the-connection-attributes"></a>接続文字列を設定するには

-   接続の時点で属性を設定します。

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   接続の後で属性を設定します。

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>例 - 金額データの書式を設定する
次の例では、[PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) を使用して金額データをフェッチする方法を示します。

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>例 - 接続属性をオーバーライドする
次の例では、接続属性をオーバーライドする方法を示します。

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>参照
[10 進数文字列と金額の書式設定 (SQLSRV ドライバー)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[データの取得](../../connect/php/retrieving-data.md)