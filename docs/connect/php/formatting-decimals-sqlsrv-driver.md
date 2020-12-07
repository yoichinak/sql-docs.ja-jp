---
title: 10 進数文字列と金額の書式設定 (SQLSRV ドライバー)
description: Microsoft SQLSRV Driver for PHP for SQL Server を使用する場合に FormatDecimals オプションと DecimalPlaces オプションを使用して 10 進数または金額を書式設定する方法について説明します。
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
ms.openlocfilehash: b111dd925a98c4f0380dfceb0a09ddffadb96592
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726824"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>10 進数文字列と金額の書式設定 (SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

正確さを維持するため、[decimal 型または numeric 型](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)は、正確な精度と小数点以下桁数の文字列として常にフェッチされます。 値が 1 未満の場合、先頭の 0 はありません。 money フィールドと smallmoney フィールドも、小数点以下桁数が 4 に固定された 10 進数フィールドであるため、これと同じです。

## <a name="add-leading-zeroes-if-missing"></a>先頭に 0 がない場合に追加する
バージョン 5.6.0 以降、オプション `FormatDecimals` が sqlsrv 接続およびステートメント レベルに追加され、ユーザーは 10 進数文字列を書式設定できます。 このオプションはブール値 (true または false) であり、フェッチされた結果の decimal または numeric の値の書式設定にのみ影響します。 つまり、`FormatDecimals` オプションは挿入や更新などの他の操作には影響しません。

既定では、`FormatDecimals` は **false** です。 true に設定すると、1 未満の 10 進値に対して先頭の 0 が追加されます。

## <a name="configure-number-of-decimal-places"></a>小数点以下の桁数を構成する
`FormatDecimals` をオンにすると、別のオプション `DecimalPlaces` を使用して、money および smallmoney のデータを表示するときの小数点以下の桁数を構成できます。 [0, 4] の範囲の整数値を指定でき、表示されるときに丸めが発生する場合があります。 ただし、基になる金額データは変わりません。

いずれのオプションも接続またはステートメント レベルに設定できます。ステートメント設定は、それに対応する接続設定を常にオーバーライドします。 `DecimalPlaces` オプションの影響を受けるのは money データ**だけ**であり、`DecimalPlaces` を有効にするには `FormatDecimals` を true に設定する必要があることに注意してください。 そうしないと、`DecimalPlaces` の設定に関係なく、書式設定は無効になります。

> [!NOTE]
> money または smallmoney のフィールドには小数点以下桁数が 4 であるため、`DecimalPlaces` 値を負の値または 4 より大きい値に設定すると無視されます。 書式設定された金額データを計算への入力として使用することはお勧めしません。

## <a name="example---a-simple-fetch"></a>例 - 単純なフェッチ
次の例からは、単純なフェッチで新しいオプションを使用する方法がわかります。

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>例 - 出力パラメーターの書式設定
10 進数または数値フィールドが[出力パラメーター](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)として返される場合、戻り値は通常の varchar 文字列と見なされます。 ただし、SQLSRV_SQLTYPE_DECIMAL か SQLSRV_SQLTYPE_NUMERIC が指定されている場合、`FormatDecimals` を true に設定すると、数字の文字列値で先頭のゼロが不足することがなくなります。 詳細については、「[方法: SQLSRV ドライバーを使用して出力パラメーターを取得する](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)」をご覧ください。

次の例からは、10 進数 (8,4) 値を返すストアド プロシージャの出力パラメーターを書式設定する方法がわかります。

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>参照
[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[データの取得](../../connect/php/retrieving-data.md)