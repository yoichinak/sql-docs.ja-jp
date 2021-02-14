---
title: Java データ型
titleSuffix: SQL Server Language Extensions
description: 入力および出力のデータ構造と、sp_execute_external_script に対する入力パラメーターのデータ型を Java から SQL Server にマップします。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 66cec63a05624a219ddbc1eb77fc5f9325626234
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100069887"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java および SQL Server のサポートされるデータ型
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

この記事では、SQL Server データ型を [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) のデータ構造とパラメーターの Java データ型にマップします。

現在、次の SQL および Java データ型が入力/出力データ セットおよび入力/出力パラメーターでサポートされています。

| SQL データ型        | Java データ型 | 解説 |
| ------------- |-------------|-|
| bit      | boolean | |
| Tinyint      | short      | |
| Smallint | short      | |
| int | INT      | |
| Real | float      | |
| Bigint | long      | |
| float | double      | |
| nchar(n) | String      | |
| nvarchar(n) | String      | |
| binary(n) | byte[]      | |
| varbinary(n) | byte[]      | |
| nvarchar(max) | String      | |
| varbinary(max) | byte[]      | |
| UNIQUEIDENTIFIER | String | |
| char(n) | String | UTF8 文字列のみがサポートされています |
| varchar(n) | String | UTF8 文字列のみがサポートされています |
| varchar(max) | String | UTF8 文字列のみがサポートされています |
| date | java.sql.date  | |
| numeric | java.math.BigDecimal  | |
| decimal | java.math.BigDecimal  | |
| money | java.math.BigDecimal  | |
| smallmoney | java.math.BigDecimal  | |
| smalldatetime | java.sql.timestamp  | |
| DATETIME | java.sql.timestamp  | |
| datetime2 | java.sql.timestamp  | |


## <a name="next-steps"></a>次のステップ

+ [SQL Server で Java を呼び出す方法](../how-to/call-java-from-sql.md)