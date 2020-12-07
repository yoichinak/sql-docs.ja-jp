---
description: TRANSLATE (Transact-SQL)
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49a16c2b5f18eeda3a6abd1396650131543ead4f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88417138"
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)

[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

2 番目の引数で指定された一部の文字が 3 番目の引数で指定された対象の文字セットに変換された後に、最初の引数として指定された文字列を返します。

## <a name="syntax"></a>構文

```syntaxsql
TRANSLATE ( inputString, characters, translations)
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数

 *inputString*。検索する文字列 [式](../../t-sql/language-elements/expressions-transact-sql.md)です。 *inputString* には、任意の文字データ型 (nvarchar、varchar、nchar、char) を指定できます。

 *characters*。置換対象の文字を含む文字列 [式](../../t-sql/language-elements/expressions-transact-sql.md)です。 *characters* には、任意の文字データ型を指定できます。

*translations*。置換文字を含む文字列 [式](../../t-sql/language-elements/expressions-transact-sql.md)です。 *translations* には、*characters* と同じデータ型および長さを指定する必要があります。

## <a name="return-types"></a>戻り値の型

2 番目の引数の文字が 3 番目の引数の一致する文字に置き換えられる、`inputString` と同じデータ型の文字式を返します。

## <a name="remarks"></a>解説

*characters* 式と *translations* 式の長さが異なる場合、`TRANSLATE` はエラーを返します。 `TRANSLATE` は、いずれかの引数が NULL の場合は NULL を返します。  

`TRANSLATE` 関数の動作は、複数の [REPLACE](../../t-sql/functions/replace-transact-sql.md) 関数を使用した場合と似ています。 ただし、`TRANSLATE` では `inputString` 内の個々の文字が複数回置き換えられることはありません。 `characters` パラメーター内の 1 つの値で、`inputString` 内の複数の文字を置き換えることができます。 

これは、複数の `REPLACE` 関数の動作とは異なります。関数を呼び出すごとに、前回の入れ子になった `REPLACE` 関数呼び出しによって置き換えられている場合であっても、関連するすべての文字が置き換えられるためです。 

`TRANSLATE` は常に SC 照合順序を認識しています。

## <a name="examples"></a>例

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. 角かっこと中かっこを通常のかっこで置き換える

次のクエリは、入力文字列の角かっこと中かっこを通常のかっこで置き換えます。

```sql
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```text
2*(3+4)/(7-2)
```

#### <a name="equivalent-calls-to-replace"></a>REPLACE と同等の呼び出し

次の SELECT ステートメントには、REPLACE 関数の入れ子になった 4 回の呼び出しがグループになっています。 このグループは、1 つ前の SELECT での TRANSLATE 関数に対する 1 回の呼び出しと同等です。

```sql
SELECT
REPLACE
(
      REPLACE
      (
            REPLACE
            (
                  REPLACE
                  (
                        '2*[3+4]/{7-2}',
                        '[',
                        '('
                  ),
                  ']',
                  ')'
            ),
            '{',
            '('
      ),
      '}',
      ')'
);
```

### <a name="b-convert-geojson-points-into-wkt"></a>B. GeoJSON ポイントを WKT に変換する

GeoJSON は、さまざまな地理的データ構造をエンコードするための形式です。 `TRANSLATE` 関数を使用すると、開発者は GeoJSON ポイントから WKT 形式への変換とその逆の変換に簡単に実行できます。 次のクエリは、入力の角かっこと中かっこを通常のかっこで置き換えます。

```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|ポイント  |座標 |  
|---------|--------- |
|(137.4  72.3) |[137.4,72.3] |

### <a name="c-use-the-translate-function"></a>C. TRANSLATE 関数を使用する

```sql
SELECT TRANSLATE('abcdef','abc','bcd') AS Translated,
       REPLACE(REPLACE(REPLACE('abcdef','a','b'),'b','c'),'c','d') AS Replaced;
```

結果は次のようになります。

| 変換後 | 置換後 |  
| ---------|--------- |
| bcddef | ddddef |


## <a name="see-also"></a>参照

- [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
- [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
- [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
- [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
- [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
- [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
- [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
- [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
- [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
- [文字列関数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)
