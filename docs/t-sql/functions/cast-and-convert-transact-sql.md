---
title: "CAST および CONVERT (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs: TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: "136"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd3db7627c4190a51db01082138677bc2b6d40d9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="cast-and-convert-transact-sql"></a>CAST および CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

あるデータ型の式を別のデータ型の式に変換します。  
たとえば、次の例では、有効桁数のレベルが異なるその他の 2 つの型に入力データ型を変更します。
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|Original   |int    |decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> このトピックの下部に多くの[例](#BKMK_examples)があります。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>引数  
*expression*  
任意の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)です。
  
*data_type*  
対象のデータ型です。 これには **xml**、**bigint**、**sql_variant** などがあります。 別名データ型は使用できません。
  
*length*  
対象のデータ型の長さを指定する整数です (省略可能)。 既定値は、30 です。
  
*style*  
CONVERT 関数で *expression* を変換する方法を指定する整数式です。 スタイルが NULL の場合は、NULL が返されます。 範囲は、*data_type* で決まります。 
  
## <a name="return-types"></a>戻り値の型
*data_type* に変換された *expression* を返します。

## <a name="date-and-time-styles"></a>日付および時刻のスタイル  
*expression* が日付や時刻のデータ型である場合、 *style* には次の表に示すいずれかの値を指定できます。 その他の値は 0 として処理されます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、日付型と時刻型を **datetimeoffset** に変換するときにサポートされているスタイルは、0 または 1 のみです。 他のすべての変換スタイルでは 9809 が返されます。
  
>  [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、アラビア式での日付形式がクウェート アルゴリズムによりサポートされます。
  
|2 桁の年 (yy) (<sup>1</sup>)|4 桁の年 (yyyy)|標準|入力/出力 (<sup>3</sup>)|  
|---|---|--|---|  
|-|**0**または**100** (<sup>1、</sup><sup>2</sup>)|datetime および smalldatetime の既定値|mon dd yyyy hh:miAM (または PM)|  
|**1**|**101**|米国|1 = mm/dd/yy<br /> 101 = mm/dd/yyyy|  
|**2**|**102**|ANSI|2 = yy.mm.dd<br /> 102 = yyyy.mm.dd|  
|**3**|**103**|イギリス/フランス|3 = dd/mm/yy<br /> 103 = dd/mm/yyyy|  
|**4**|**104**|ドイツ|4 = dd.mm.yy<br /> 104 = dd.mm.yyyy|  
|**5**|**105**|イタリア|5 = dd-mm-yy<br /> 105 = dd-mm-yyyy|  
|**6**|**106** <sup>(1)</sup>|-|6 = dd mon yy<br /> 106 = dd mon yyyy|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mon dd, yy<br /> 107 = Mon dd, yyyy|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9**または**109** (<sup>1、</sup><sup>2</sup>)|既定値 + ミリ秒|mon dd yyyy hh:mi:ss:mmmAM (または PM)|  
|**10**|**110**|米国|10 = mm-dd-yy<br /> 110 = mm-dd-yyyy|  
|**11**|**111**|日本|11 = yy/mm/dd<br /> 111 = yyyy/mm/dd|  
|**12**|**112**|ISO|12 = yymmdd<br /> 112 = yyyymmdd|  
|-|**13**または**113** (<sup>1、</sup><sup>2</sup>)|ヨーロッパの既定値 + ミリ秒|dd mon yyyy hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20**または**120** (<sup>2</sup>)|ODBC 標準|yyyy-mm-dd hh:mi:ss(24h)|  
|-|**21**または**121** (<sup>2</sup>)|time、date、datetime2、および datetimeoffset の ODBC 標準 (ミリ秒を含む) の既定値|yyyy-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|yyyy-mm-ddThh:mi:ss.mmm (スペースなし)<br /> 注: ミリ秒 (mmm) の値が 0 の場合、ミリ秒の値は表示されません。 たとえば、値 '2012-11-07T18:26:20.000' は、'2012-11-07T18:26:20' と表示されます。|  
|-|**127**(<sup>6, 7</sup>)|ISO 8601 (タイム ゾーン Z)|yyyy-mm-ddThh:mi:ss.mmmZ (スペースなし)<br /> 注: ミリ秒 (mmm) の値が 0 の場合、ミリ秒の値は表示されません。 たとえば、値 '2012-11-07T18:26:20.000' は、'2012-11-07T18:26:20' と表示されます。|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|イスラム暦 (<sup>5</sup>)|dd mon yyyy hh:mi:ss:mmmAM<br /> このスタイルでは、mon は月の正式名に関する複数トークンの Hijri (イスラム暦) ユニコード表現を意味します。 この値は、SSMS の既定の米国用インストールでは正しく表示されません。|  
|-|**131** (<sup>2</sup>)|イスラム暦 (<sup>5</sup>)|dd/mm/yyyy hh:mi:ss:mmmAM|  
  
<sup>1</sup>これらのスタイル値が非決定的な結果を返します。 この場合は、すべての (yy) (2 桁の年) スタイルと、(yyyy) (4 桁の年) スタイルのサブセットが対象となります。
  
<sup>2</sup>既定値 (*style* **0** または**100**、 **9**または**109**、 **13**または**113**、 **20**または**120**、および**21**または**121**)常に 4 桁の年 (yyyy) を返します。
  
<sup>3</sup>**datetime** 型に変換する場合は入力になり、文字データに変換する場合は出力になります。
  
<sup>4</sup> XML で使用するよう設計されています。 **datetime** または **smalldatetime** 型から文字データに変換する場合の出力形式は、前の表に示したとおりです。
  
<sup>5</sup>Hijri とはいくつかのバリエーションがあるカレンダー システムです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではクウェート アルゴリズムが使用されます。
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定では、2 桁の年は、終了年 2049 年を基準に解釈されます。 つまり、2 桁の年である 49 年は 2049 年、50 年は 1950 年と解釈されます。 クライアント アプリケーションの中には、オートメーション オブジェクトをベースとするクライアント アプリケーションのように、2030 年を終了年とするものも多くあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では構成オプション two digit year cutoff が用意されており、このオプションを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の終了年の設定を変更でき、一貫した日付の処理を行うことができます。 年は 4 桁で指定することを推奨します。  
  
<sup>6</sup>文字データを **datetime** または **smalldatetime** 型にキャストする場合のみサポートされます。 日付部分または時刻部分のみを表す文字データは、**datetime** または **smalldatetime** データ型にキャストされます。時刻部分の指定がない場合、時刻は 00:00:00:000 に設定され、日付部分の指定がない場合、日付は 1900-01-01 に設定されます。
  
<sup>7</sup> タイム ゾーン インジケーター Z は省略可能です。これを使用すると、タイム ゾーン情報が含まれる XML の **datetime** 値から、タイム ゾーン情報が含まれない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 値へのマップが容易になります。 Z は、タイム ゾーン UTC-0 を示すインジケーターです。 他のタイム ゾーンは、+ または - の方向に HH:MM オフセットで示されます。 たとえば、`2006-12-12T23:45:12-08:00` のようになります。
  
**smalldatetime** 型を文字データに変換する場合、秒またはミリ秒を含むスタイルではそれらの位置に 0 が表示されます。 **datetime** や **smalldatetime** データ型の値を変換するときは、**char** や **varchar** データ型の長さを適切に設定することにより、日付の不要な部分を切り捨てることができます。
  
時刻を含むスタイルを使用する文字データから **datetimeoffset** に変換すると、タイム ゾーン オフセットが結果に追加されます。
  
## <a name="float-and-real-styles"></a>float 型スタイルと real 型スタイル
*expression* が **float** または **real** である場合、*style* には次の表に示すいずれかの値を指定できます。 その他の値は 0 として処理されます。
  
|値|出力|  
|---|---|
|**0** (既定値)|最高 6 桁。 該当する場合は、科学的表記法で使用します。|  
|**1**|常に 8 桁。 常に科学的表記法で使用します。|  
|**2**|常に 16 桁。 常に科学的表記法で使用します。|  
|**3**|常に 17 桁。 損失のない変換に使用します。 このスタイルですべての個別の float または real の値は、個別の文字列に変換することが保証されます。<br /> **適用範囲:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、および [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降|  
|**126, 128, 129**|レガシ システムのために含まれていますが、将来のリリースでは廃止される可能性があります。|  
  
## <a name="money-and-smallmoney-styles"></a>money 型スタイルおよび smallmoney 型スタイル
*expression* が **money** または **smallmoney** である場合、*style* には次の表に示すいずれかの値を指定できます。 その他の値は 0 として処理されます。
  
|値|出力|  
|---|---|
|**0** (既定値)|小数点位置から左へ 3 桁ごとの位置にはコンマを挿入しません。また、小数点右側には 2 桁をとります。たとえば 4235.98 のようになります。|  
|**1**|小数点位置から左へ 3 桁ごとにコンマを挿入し、小数点右側には 2 桁をとります。たとえば 3,510.92 のようになります。|  
|**2**|小数点位置から左へ 3 桁ごとの位置にはコンマを挿入しません。また、小数点右側には 4 桁をとります。たとえば 4235.9819 のようになります。|  
|**126**|char(n) または varchar(n) に変換する場合はスタイル 2 に相当します。|  
  
## <a name="xml-styles"></a>xml スタイル
*expression* が **xml** である場合、*style* には次の表に示すいずれかの値を指定できます。 その他の値は 0 として処理されます。
  
|値|出力|  
|---|---|
|**0** (既定値)|既定の解析動作を使用します。つまり、余分な空白を破棄し、内部の DTD サブセットを許可しません。<br /> **注:** **xml** データ型への変換では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での余分な空白は XML 1.0 とは別の方法で処理されます。 詳細については、「[XML データのインスタンスを作成する](../../relational-databases/xml/create-instances-of-xml-data.md)」を参照してください。|  
|**1**|余分な空白を保持します。 このスタイル設定では、既定の **xml:space** 処理が設定され、**xml:space="preserve"** が代わりに指定された場合と同じ動作が行われます。|  
|**2**|限定的な内部 DTD サブセット処理を有効にします。<br /><br /> 有効な場合、サーバーでは内部 DTD サブセットで提供される情報を次のように使用して、検証を行わない解析操作を実行できます。<br /> -属性の既定の設定が適用されます。<br /> -内部エンティティ参照は解決され、展開します。<br /> の構文の正確さ DTD のコンテンツ モデルがチェックされます。<br /> パーサーでは外部 DTD サブセットが無視されます。 また、パーサーでは XML 宣言を評価して **standalone** 属性が **yes** と **no** のどちらであるかを確認するのではなく、XML インスタンスをスタンドアロン ドキュメントと見立てて解析します。|  
|**3**|余分な空白を保持し、限定的な内部 DTD サブセット処理を有効にします。|  
  
## <a name="binary-styles"></a>バイナリ スタイル
*expression* が **binary(n)**、**varbinary(n)**、**char(n)**、または **varchar(n)** である場合、*style* には次の表に示すいずれかの値を指定できます。 表に記載されていないスタイル値の場合は、エラーが返されます。
  
|値|出力|  
|---|---|
|**0** (既定値)|ASCII 文字をバイナリ バイトに変換するか、バイナリ バイトを ASCII 文字に変換します。 各文字またはバイトは 1:1 で変換されます。<br /> *data_type* がバイナリ型である場合、文字 0x が結果の左側に追加されます。|  
|**1**, **2**|*data_type* がバイナリ型である場合、式は文字式であることが必要です。 *expression* は偶数桁の 16 進数 (0、1、2、3、4、5、6、7、8、9、A、B、C、D、E、F、a、b、c、d、e、f) で構成される必要があります。 *style* が 1 に設定されている場合は、式の先頭の 2 文字を文字 0x にする必要があります。 式に奇数桁の文字が含まれているか、いずれかの文字が無効な場合は、エラーが発生します。<br /> 変換された式の長さが *data_type* の長さよりも長い場合、結果の右側が切り捨てられます。<br /> 変換された結果よりも長い固定長の *data_types* の場合、結果の右側に 0 が追加されます。<br /> data_type が文字型である場合、式はバイナリ式であることが必要です。 各バイナリ文字は、16 進値を表す 2 桁の英数文字に変換されます。 変換された式の長さが *data_type* の長さよりも長い場合は、右側が切り捨てられます。<br /> *data_type* が固定サイズの文字型で、変換された結果の長さが *data_type* の長さよりも短い場合、変換された式の右側に空白が追加され、偶数桁の 16 進数が維持されます。<br /> *style* が 1 の場合、変換された結果の左側に文字 0x が追加されます。|  
  
## <a name="implicit-conversions"></a>暗黙的な変換
暗黙的な変換とは、CAST または CONVERT 関数を指定せずに実行される変換のことです。 一方、明示的な変換には、CAST または CONVERT 関数を指定する必要があります。 次の図は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムで提供されるデータ型に許可されている、すべての明示的および暗黙的なデータ型変換です。 これには、**xml**、**bigint**、および **sql_variant** 型が含まれます。 代入時に **sql_variant** データ型からの暗黙的な変換は行われませんが、**sql_variant** データ型への暗黙的な変換は行われます。
  
> [!TIP]  
>  この表は、[Microsoft ダウンロード センター](http://www.microsoft.com/download/details.aspx?id=35834)で PDF ファイルとしてダウンロードできます。  
  
![データ型変換テーブル](../../t-sql/data-types/media/lrdatahd.png "データ型変換テーブル")
  
**datetimeoffset** と、**char**、**varchar**、**nchar**、および **nvarchar** の各文字型との間で変換を行う場合、変換後のタイム ゾーン オフセットの部分は、-08:00 のように HH と MM の両方が常に 2 桁である必要があります。
  
> [!NOTE]  
>  Unicode データでは常に偶数のバイト数が使用されるので、**binary** 型または **varbinary** 型と、Unicode がサポートするデータ型との間でデータを変換する場合は注意してください。 たとえば、`SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)` という変換を行うと、16 進数の 41 ではなく、4100 が返されます。  
  
## <a name="large-value-data-types"></a>大きな値のデータ型
大きな値のデータ型では、それより小さな値のデータ型、つまり **varchar**、**nvarchar** および **varbinary** 型と同様の明示的および暗黙的な変換動作が行われます。 ただし、次のガイドラインを考慮する必要があります。
-   **image** 型から **varbinary(max)** 型への変換およびその逆の変換は暗黙的な変換であり、**text** 型と **varchar(max)** 型の間、および **ntext** 型と **nvarchar(max)** 型の間の変換も暗黙的な変換です。  
-   **varchar(max)** 型のような大きな値のデータ型から、**varchar** 型のような小さな値のデータ型への変換は暗黙的な変換ですが、大きな値が、小さなデータ型で指定された長さに対して大きすぎると、切り捨てが発生します。  
-   **varchar** 、**nvarchar**、または **varbinary** 型からそれぞれ対応する大きな値のデータ型への変換は、暗黙的に実行されます。  
-   **sql_variant** 型から大きな値のデータ型への変換は明示的な変換です。  
-   大きな値のデータ型は、**sql_variant** 型へは変換できません。  
  
**xml** データ型からの変換方法の詳細については、「[XML データのインスタンスを作成する](../../relational-databases/xml/create-instances-of-xml-data.md)」を参照してください。
  
## <a name="xml-data-type"></a>xml データ型
明示的か暗黙的かにかかわらず、**xml** データ型を文字列またはバイナリのデータ型にキャストするとき、**xml** データ型の内容は一連のルールに基づいてシリアル化されます。 このルールの詳細については、「[XML データのシリアル化を定義する](../../relational-databases/xml/define-the-serialization-of-xml-data.md)」を参照してください。 他のデータ型から **xml** データ型への変換方法については、「[XML データのインスタンスを作成する](../../relational-databases/xml/create-instances-of-xml-data.md)」を参照してください。
  
## <a name="text-and-image-data-types"></a>text および image データ型
データ型の自動変換は、**text** 型および **image** 型ではサポートされません。 **text** データは文字データに、**image** データは **binary** または **varbinary** 型に明示的に変換できますが、最大の長さは 8,000 バイトに制限されます。 文字を含む文字式を **int** 型に変換するなど、不適切な変換が試行された場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラー メッセージが返されます。
  
## <a name="output-collation"></a>出力の照合順序  
CAST または CONVERT の入出力が文字列である場合、出力では入力と同じ照合順序および照合順序ラベルが使用されます。 入力が文字列ではない場合、出力ではデータベースの既定の照合順序、および強制可能な既定照合順序の照合順序ラベルが使用されます。 詳細については、「[照合の優先順位 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)」を参照してください。
  
出力に別の照合順序を割り当てるには、CAST 関数または CONVERT 関数の結果式に COLLATE 句を適用します。 例:
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>切り捨てと丸め処理の結果
文字やバイナリ式 (**char**、 **nchar**、 **nvarchar**、 **varchar**、**binary**、または**varbinary**)を別のデータ型に変換する場合は、データを切り捨てて一部分だけが表示されることがあります。または、結果が短すぎて表示できないというエラーが返されます。 **char** 、**varchar**、**nchar**、**nvarchar**、**binary**、および **varbinary** 型への変換では、次の表に示す変換を除き、切り捨てが行われます。
  
|変換前のデータ型|変換後のデータ型|結果|  
|---|---|---|
|**int**、 **smallint**、または**tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**、 **smallmoney**、**numeric**、 **decimal**、 **float**、または**real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\* = 結果が短すぎて表示できない。 E  = 結果が短すぎて表示できない場合エラーが返される。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、元のデータから別のデータ型に変換し、再度元のデータ型に戻すラウンド トリップ変換の場合にだけ、異なるバージョンでも同じ結果が生成されることが保証されています。 次にラウンド トリップ変換の例を示します。
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  **binary** 型の値を作成し、これを数値データ型に変換することは避けてください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**decimal** または **numeric** データ型の **binary** 型への変換が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン間で同じになることは保証されていません。  
  
次の例では、短すぎて表示できない結果式を示します。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
小数点の位置が異なるデータ型を変換すると、場合によって結果の値が切り捨てられるか丸められます。 次の表はその動作です。
  
|From|To|動作|  
|---|---|---|
|**numeric**|**numeric**|丸め処理|  
|**numeric**|**int**|切り捨て|  
|**numeric**|**money**|丸め処理|  
|**money**|**int**|丸め処理|  
|**money**|**numeric**|丸め処理|  
|**float**|**int**|切り捨て|  
|**float**|**numeric**|丸め処理<br /><br /> 科学的表記法を使用する **float** 値から **decimal** または **numeric** への変換は、有効桁数が 17 桁の値にのみ制限されます。 有効桁数が 17 より多い値はゼロに丸められます。|  
|**float**|**datetime**|丸め処理|  
|**datetime**|**int**|丸め処理|  
  
たとえば、値 10.6496 および-10.6496 は、**int**または**numeric**型への変換中に切り捨てられるか丸められます。
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
クエリの結果は次の表に示します。
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
変換後のデータ型の小数点以下桁数が変換前のデータ型の小数点以下桁数より少ない場合は、値が丸められます。 たとえば、次の変換の結果は`$10.3497`です。
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、数値型ではない **char**、**nchar**、**varchar**、または **nvarchar** データを **int**、**float**、**numeric**、または **decimal** に変換するとエラー メッセージが返されます。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、空の文字列 (" ") を **numeric** または **decimal** に変換してもエラーが返されます。
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>一部の datetime 変換は非決定的である
次の表は、文字列から datetime への変換が非決定的であるスタイルを示します。
  
|||  
|-|-|  
|100 未満のすべてのスタイル<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup>スタイル 20 と 21 を除く
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降、補助文字 (SC) の照合順序を使用した場合は、**nchar** または **nvarchar** から短い **nchar** または **nvarchar** 型への CAST 操作を実行すると、サロゲート ペア内ではなく、補助文字の前で切り捨てが行われます。 たとえば次のコードでは、`@x` で `'ab'` だけが保持されます。 補助文字を保持するための十分な領域がありません。
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
SC の照合順序を使用する場合、`CONVERT` の動作は `CAST` の動作と似たものとなります。
  
## <a name="compatibility-support"></a>互換性サポート
以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**time** および **datetime2** データ型に対する CAST および CONVERT 操作の既定のスタイルは、いずれかの型が計算列の式で使用されている場合を除き、121 です。 計算列の場合、既定のスタイルは 0 です。 この動作は、計算列が作成されるとき、自動パラメーター化を含むクエリで使用されるとき、または制約の定義で使用されるときに、計算列に影響を与えます。
  
互換性レベル 110 以上では、**time** および **datetime2** データ型に対する CAST および CONVERT 操作の既定のスタイルは常に 121 です。 クエリが古い動作に依存する場合は、110 より小さい互換性レベルを使用するか、または影響を受けるクエリで 0 スタイルを明示的に指定してください。
  
データベースを互換性レベル 110 以上にアップグレードしても、ディスクに格納されているユーザー データは変更されません。 このようなデータは手動で適切に修正する必要があります。 たとえば、SELECT INTO を使用して、前に説明した計算列の式を含むソースからテーブルを作成した場合は、計算列の定義自体ではなく、(スタイル 0 を使用する) データが格納されます。 このようなデータは、手動で更新してスタイル 121 に一致させる必要があります。
  
## <a name="BKMK_examples"></a> 使用例  
  
### <a name="a-using-both-cast-and-convert"></a>A. CAST と CONVERT の両方を使用する  
次の各例では、表示価格の最初の桁が `3` である製品について製品名を取得し、その `ListPrice` を `int` 型に変換します。
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. CAST を算術演算子と共に使用する  
次の例では、今年のこれまでの売り上げ合計 (`SalesYTD`) を手数料のパーセンテージ (`CommissionPCT`) で割り、単一列の計算 (`Computed`) を行います。 この結果は、最も近い整数に丸められた後、`int` データ型に変換されます。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. CAST を使用して連結する  
次の例では、CAST を使って、文字型でない式を連結します。 AdventureWorksDW を使用します。
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. CAST を使用してテキストをさらに読みやすくする  
次の例では、選択リストの中で CAST を使用し、`Name` 列を **char(10)** 型の列に変換します。 AdventureWorksDW を使用します。
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. CAST を LIKE 句と共に使用する  
次の例では、`money` 列 `SalesYTD` を `int` 型に変換して、次に `LIKE` 句と共に使用できるよう `char(20)` 列に変換します。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. CONVERT または CAST を、型指定された XML と共に使用する  
次に示す例では、「[XML データ型と列 (SQL Server)](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)」により、CONVERT を使用して型指定された XML への変換を行います。
  
次の例では、空白、テキスト、およびマークアップのある文字列を、型指定された XML に変換し、すべての余分な空白 (ノード間の境界の空白) を削除します。
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
次の例では、空白、テキスト、およびマークアップのある同様の文字列を、型指定された XML に変換し、すべての余分な空白 (ノード間の境界の空白) を保持します。
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
次の例では、空白、テキスト、マークアップのある文字列を、型指定された XML にキャストします。
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
例については、「[XML データのインスタンスを作成する](../../relational-databases/xml/create-instances-of-xml-data.md)」を参照してください。
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. CAST および CONVERT を datetime データと共に使用する  
次の例では、現在の日付と時刻を表示し、`CAST` を使用して現在の日付と時刻を文字列データ型に変更した後、`CONVERT` を使用して `ISO 8901` 形式で日付と時刻を表示します。
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
次の例は、前の例とほぼ逆になります。 この例では、日付と時刻を文字型データとして表示し、`CAST` を使用して文字型データを `datetime` データ型に変更します。さらに、`CONVERT` を使用して、文字型データを `datetime` データ型に変換します。
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. CONVERT をバイナリ データおよび文字データと共に使用する  
以下は、さまざまなスタイルを使用してバイナリ データと文字データを変換した結果を示す例です。
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
次の例では、スタイル 1 によって結果が切り捨てられるように強制されることを示します。 切り捨ての原因は文字 0x が結果に含まれることです。  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
次の例は、文字 0x が結果に含まれないため、スタイル 2 では結果が切り捨てられないことを示します。  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
'Name' の文字の値をバイナリ値に変換します。  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. 日付と時刻のデータ型の変換  
次の例では、date、time、および datetime データ型の変換の例を示します。
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. CAST および CONVERT を使用する  
この例では、表示価格の最初の桁が `3` の製品の名前を取得し、`ListPrice` を **int** に変換します。AdventureWorksDW を使用します。
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
この例では、CAST ではなく CONVERT を使用して、同じクエリを使用します。 AdventureWorksDW を使用します。
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. CAST を算術演算子と共に使用する  
次の例は、製品の単価 (`UnitPrice`) を割引率 (`UnitPriceDiscountPct`) で割ることによって、1 つの列を計算します。 この結果は最も近い整数に丸められた後に`int`に変換されます。 AdventureWorksDW を使用します。
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>L. CAST を LIKE 句と共に使用する  
次の例では、**money**列`ListPrice`を**int**型に変換し、さらに、LIKE 句と共に使用できるように **char(20)** に変換します。 AdventureWorksDW を使用します。
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. CAST および CONVERT を datetime データと共に使用する  
次の例では、現在の日付と時刻を表示し、CAST を使用して現在の日付と時刻を文字列データ型に変更した後、CONVERT を使用して ISO 8901 形式で日付と時刻を表示します。 AdventureWorksDW を使用します。
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
次の例は、前の例とほぼ逆になります。 この例では、日付と時刻を文字型データとして表示し、CAST を使用して文字型データを **datetime** データ型に変更します。さらに、CONVERT を使用して、文字型データを **datetime** データ型に変換します。 AdventureWorksDW を使用します。
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>参照
[データ型の変換 &#40;データベース エンジン&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
[システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[国際化に対応した Transact-SQL ステートメントの記述](../../relational-databases/collations/write-international-transact-sql-statements.md)
  
