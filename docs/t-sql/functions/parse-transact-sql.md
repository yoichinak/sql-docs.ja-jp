---
title: "PARSE (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSE
- PARSE_TSQL
dev_langs: TSQL
helpviewer_keywords: PARSE function
ms.assetid: 6a2dbf10-f692-471b-9458-24d246963049
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3e172a7d68edc212ce4803103dc1f975e4bf89db
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="parse-transact-sql"></a>PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で要求されたデータ型に変換された式の結果を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>引数  
 *string_value*  
 指定したデータ型に解析する、書式設定された値を表す **nvarchar**(4000) 値。  
  
 *string_value* は、要求されたデータ型の有効な表現である必要があります。そうでない場合、PARSE でエラーが発生します。  
  
 *data_type*  
 結果に要求されたデータ型を表すリテラル値。  
  
 *culture*  
 *string_value* が書式設定されるカルチャを識別する文字列です (省略可能)。  
  
 *culture* 引数が指定されていない場合は、現在のセッションの言語が使用されます。 この言語は、SET LANGUAGE ステートメントを使用して、暗黙的または明示的に設定されます。 *culture* は、.NET Framework でサポートされている任意のカルチャを受け入れます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で明示的にサポートされている言語に制限されません。 *culture* 引数が有効でない場合は、PARSE でエラーが発生します。  
  
## <a name="return-types"></a>戻り値の型  
 要求されたデータ型に変換された式の結果を返します。  
  
## <a name="remarks"></a>解説  
 PARSE への引数として渡される null の値は、2 つの方法で扱われます。  
  
1.  null 定数が渡されると、エラーが発生します。 null の値をカルチャに対応する方法で異なるデータ型に解析することはできません。  
  
2.  実行時に null の値を含んだパラメーターが渡された場合、バッチ全体がキャンセルされないように null が返されます。  
  
 PARSE は、文字列型から日付/時刻型および数値型への変換にのみ使用します。 一般的な型変換では、引き続き CAST または CONVERT を使用します。 文字列値の解析には、一定のパフォーマンス オーバーヘッドが発生することに留意してください。  
  
 解析は、.NET Framework 共通言語ランタイム (CLR) の存在に依存しています。  
  
 この関数は、CLR の存在に依存するため、リモート処理は行われません。 CLR が必要な関数をリモート処理すると、リモート サーバー上でエラーが発生します。  
  
 **data_type パラメーターの詳細**  
  
 *data_type* パラメーターの値は、スタイルと共に、次の表に示す型に制限されます。 スタイル情報は、許可するパターンの種類を決定するために提供されます。 スタイルの詳細については、**System.Globalization.NumberStyles** および **DateTimeStyles** 列挙体に関する .NET Framework のドキュメントを参照してください。  
  
|カテゴリ|型|.NET Framework 型|使用されるスタイル|  
|--------------|----------|-------------------------|-----------------|  
|数値|bigint|Int64|NumberStyles.Number|  
|数値|int|Int32|NumberStyles.Number|  
|数値|smallint|Int16|NumberStyles.Number|  
|数値|tinyint|Byte|NumberStyles.Number|  
|数値|decimal|Decimal|NumberStyles.Number|  
|数値|numeric|Decimal|NumberStyles.Number|  
|数値|float|Double|NumberStyles.Float|  
|数値|real|Single|NumberStyles.Float|  
|数値|smallmoney|Decimal|NumberStyles.Currency|  
|数値|money|Decimal|NumberStyles.Currency|  
|日時|date|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日時|time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日時|datetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日時|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日時|datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日時|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
  
 **カルチャ パラメーターの詳細**  
  
 次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 言語から .NET Framework カルチャへのマッピングを示します。  
  
|完全名|別名|LCID|特定のカルチャ|  
|---------------|-----------|----------|----------------------|  
|us_english|英語|1033|ja-JP|  
|Deutsch|ドイツ語|1031|de-DE|  
|Français|フランス語|1036|fr-FR|  
|日本語|日本語|1041|ja-JP|  
|Dansk|デンマーク語|1030|da-DK|  
|Español|スペイン語|3082|es-ES|  
|Italiano|イタリア語|1040|it-IT|  
|Nederlands|オランダ語|1043|nl-NL|  
|Norsk|ノルウェー語|2068|nn-NO|  
|Português|ポルトガル語|2070|pt-PT|  
|Suomi|フィンランド語|1035|fi|  
|Svenska|スウェーデン語|1053|sv-SE|  
|Čeština|チェコ語|1029|Cs-CZ|  
|magyar|ハンガリー語|1038|Hu-HU|  
|polski|ポーランド語|1045|Pl-PL|  
|română|ルーマニア語|1048|Ro-RO|  
|hrvatski|クロアチア語|1050|hr-HR|  
|slovenčina|スロバキア語|1051|Sk-SK|  
|slovenski|スロベニア語|1060|Sl-SI|  
|ΕΛΛΗΝΙΚΆ|ギリシャ語|1032|El-GR|  
|БЪЛГАРСКИ|ブルガリア語|1026|bg-BG|  
|РУССКИЙ|ロシア語|1049|Ru-RU|  
|Türkçe|トルコ語|1055|Tr-TR|  
|British|英語 (U.K.)|2057|en-GB|  
|eesti|エストニア語|1061|Et-EE|  
|latviešu|ラトビア語|1062|lv-LV|  
|lietuvių|リトアニア語|1063|lt-LT|  
|Português (Brasil)	|ポルトガル語 (ブラジル)|1046|pt-BR|  
|繁體中文|繁体字中国語|1028|zh-TW|  
|한국어|韓国語|1042|Ko-KR|  
|简体中文|簡体字中国語|2052|zh-CN|  
|アラビア語|アラビア語|1025|ar-SA|  
|ไทย|タイ語|1054|Th-TH|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-parse-into-datetime2"></a>A. Datetime2 に解析します。  
  
```  
SELECT PARSE('Monday, 13 December 2010' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-13 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-parse-with-currency-symbol"></a>B. 通貨記号で解析します。  
  
```  
SELECT PARSE('€345,98' AS money USING 'de-DE') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
345.98  
  
(1 row(s) affected)  
```  
  
### <a name="c-parse-with-implicit-setting-of-language"></a>C. 暗黙的な言語設定で解析します。  
  
```  
-- The English language is mapped to en-US specific culture  
SET LANGUAGE 'English';  
SELECT PARSE('12/16/2010' AS datetime2) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-16 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
  
