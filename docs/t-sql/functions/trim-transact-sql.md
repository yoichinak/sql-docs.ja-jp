---
description: TRIM (Transact-SQL)
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
author: julieMSFT
ms.author: jrasnick
monikerRange: = azure-sqldw-latest||=azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c2110b541ad06770b1218e3e48e77056085eaeb
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379527"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

文字列の先頭と末尾にあるスペース文字 `char(32)` または他の指定した文字を削除します。  

## <a name="syntax"></a>構文

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database
TRIM ( [ characters FROM ] string )
```

```syntaxsql
-- Syntax for Azure Synapse Analytics
TRIM ( string )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数

characters: 削除する必要がある文字を含む LOB 以外の任意の文字型 (`nvarchar`、`varchar`、`nchar`、または`char`) のリテラル、変数、または関数呼び出しです。 `nvarchar(max)` および `varchar(max)` 型は使用できません。

string: 文字を削除する必要がある任意の文字型 (`nvarchar`、`varchar`、`nchar`、または`char`) の式です。

## <a name="return-types"></a>戻り値の型

空白文字 `char(32)` または他の指定した文字が両側から削除される、文字列引数の型を持つ文字式を返します。 入力文字列が `NULL` の場合は `NULL` を返します。

## <a name="remarks"></a>解説

既定では、`TRIM` 関数によって文字列の先頭と末尾の両方から空白文字が削除されます。 この動作は `LTRIM(RTRIM(@string))` と同等です。

## <a name="examples"></a>例

### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  文字列の先頭と末尾からスペース文字を削除します。

次の例では、単語 `test` の前後からスペースを削除します。

```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```
test
```

### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  指定した文字を文字列の両側から削除します。

次の例では、`#` の前と単語 `test` の後ろからピリオドとスペースを削除します。

```sql
SELECT TRIM( '.,! ' FROM  '     #     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
#     test
```

## <a name="see-also"></a>参照

- [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
- [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
- [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
- [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
- [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
- [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
- [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
