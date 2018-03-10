---
title: "ODBC スカラー関数 (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- CURDATE ODBC function
- DAYOFMONTH ODBC function
- WEEK ODBC function
- functions, ODBC CONCAT
- SECOND ODBC function
- functions, ODBC CURRENT_TIME
- functions, ODBC HOUR
- functions, ODBC QUARTER
- TRUNCATE ODBC function
- functions, ODBC SECOND
- DAYOFWEEK ODBC function
- CURRENT_DATE ODBC function
- DAYNAME ODBC function
- CURTIME ODBC function
- functions, ODBC CURRENT_DATE
- MINUTE ODBC function
- functions, ODBC BIT_LENGTH
- functions, ODBC OCTET_LENGTH
- CONCAT ODBC function
- MONTHNAME ODBC function
- functions, ODBC DAYOFYEAR
- OCTET_LENGTH ODBC function
- functions [SQL Server], ODBC scalar functions
- BIT_LENGTH ODBC function
- functions, ODBC DAYOFMONTH
- CURRENT_TIME ODBC function
- functions, ODBC CURDATE
- functions, ODBC CURTIME
- functions, ODBC TRUNCATE
- functions, ODBC MONTHNAME
- functions, ODBC DAYNAME
- ODBC scalar functions
- functions, ODBC MINUTE
- functions, ODBC DAYOFWEEK
- QUARTER ODBC function
- DAYOFYEAR ODBC function
- functions, ODBC WEEK
- HOUR ODBC function
ms.assetid: a0df1ac2-6699-4ac0-8f79-f362f23496f1
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2838242bcef767206af71446f9decd9ed798536a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="odbc-scalar-functions-transact-sql"></a>ODBC スカラー関数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、[ODBC スカラー関数](http://go.microsoft.com/fwlink/?LinkID=88579)を使用できます。 これらのステートメントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって解釈されます。 具体的には、ストアド プロシージャやユーザー定義関数の中で、文字列、数値、時刻、日付、間隔を扱う関数のほか、システム関数を使用することができます。  
  
## <a name="usage"></a>使用方法  
 `SELECT {fn <function_name> [ (<argument>,....n) ] }`  
  
## <a name="functions"></a>関数  
 次の表は、同等の機能が [!INCLUDE[tsql](../../includes/tsql-md.md)] に存在しない ODBC スカラー関数をまとめたものです。  
  
### <a name="string-functions"></a>文字列関数  
  
|関数|Description|  
|--------------|-----------------|  
|BIT_LENGTH( string_exp ) (ODBC 3.0)|文字列式の長さ (ビット単位) を返します。<br /><br /> 引数は文字列データ型に限定されません。 そのため、string_exp から文字列型への暗黙的な変換は実行されず、指定されたデータ型の (内部的な) サイズを返します。|  
|CONCAT( string_exp1,string_exp2) (ODBC 1.0)|string_exp1 に対して string_exp2 を連結した結果の文字列を返します。 結果の文字列は DBMS に依存します。 たとえば、string_exp1 によって表される列に NULL 値が含まれている場合は、DB2 が NULL を返しますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は NULL 以外の文字列を返します。|  
|OCTET_LENGTH( string_exp ) (ODBC 3.0)|文字列式の長さ (バイト単位) を返します。 結果は、ビット数を 8 で割った値以上の最小の整数になります。<br /><br /> 引数は文字列データ型に限定されません。 そのため、string_exp から文字列型への暗黙的な変換は実行されず、指定されたデータ型の (内部的な) サイズを返します。|  
  
### <a name="numeric-function"></a>数値関数  
  
|関数|Description|  
|--------------|-----------------|  
|TRUNCATE( numeric_exp, integer_exp) (ODBC 2.0)|numeric_exp を、小数点の右側の integer_exp 桁までに切り詰めて返します。 Numeric_exp に切り捨てられます integer_exp が負の場合は、&#124; integer_exp &#124;です。小数点の左側に位置します。|  
  
### <a name="time-date-and-interval-functions"></a>時刻、日付、および間隔を扱う関数  
  
|関数|Description|  
|--------------|-----------------|  
|CURRENT_DATE( ) (ODBC 3.0)|現在の日付を返します。|  
|CURDATE( ) (ODBC 3.0)|現在の日付を返します。|  
|CURRENT_TIME`[( time-precision )]` (ODBC 3.0)|現在のローカル時間を返します。 time-precision 引数には、取得する値の秒の有効桁数を指定します。|  
|CURTIME() (ODBC 3.0)|現在のローカル時間を返します。|  
|DAYNAME( date_exp ) (ODBC 2.0)|date_exp の日の部分について、データ ソース固有の曜日名を表す文字列を返します (例 : 英語を使ったデータ ソースの場合は Sunday ～ Saturday または Sun. ～ Sat.、 ドイツ語を使ったデータ ソースの場合は Sonntag ～ Samstag など)。|  
|DAYOFMONTH( date_exp ) (ODBC 1.0)|date_exp の月部分に基づき、月初から数えた日を 1 ～ 31 の整数値として返します。|  
|DAYOFWEEK( date_exp ) (ODBC 1.0)|date_exp の週部分に基づき、週の初めから数えた曜日を 1 ～ 7 の整数値として返します。1 は日曜日を表します。|  
|HOUR( time_exp ) (ODBC 1.0)|time_exp の時部分に基づき、対応する時刻を 0 ～ 23 の整数値として返します。|  
|MINUTE( time_exp ) (ODBC 1.0)|time_exp の分部分に基づき、対応する分を 0 ～ 59 の整数値として返します。|  
|SECOND( time_exp ) (ODBC 1.0)|time_exp の秒部分に基づき、対応する秒を 0 ～ 59 の整数値として返します。|  
|MONTHNAME( date_exp ) (ODBC 2.0)|date_exp の月の部分について、データ ソース固有の月名を表す文字列を返します (例 : 英語を使ったデータ ソースの場合は January ～ December または Jan. ～ Dec.、ドイツ語を使ったデータ ソースの場合は Januar ～ Dezember など)。|  
|QUARTER( date_exp ) (ODBC 1.0)|date_exp の四半期を 1 ～ 4 の整数値として返します。1 は、1 月 1 日～3 月 31 日を表します。|  
|WEEK( date_exp ) (ODBC 1.0)|date_exp の週部分に基づき、年頭から数えた週を 1 ～ 53 の整数値として返します。|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-an-odbc-function-in-a-stored-procedure"></a>A. ODBC 関数をストアド プロシージャで使用する  
 次の例では、ストアド プロシージャで、ODBC 関数を使用します。  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn OCTET_LENGTH( @string_exp )};  
```  
  
### <a name="b-using-an-odbc-function-in-a-user-defined-function"></a>B. ODBC 関数をユーザー定義関数で使用する  
 次の例では、ODBC 関数をユーザー定義関数で使用しています。  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn OCTET_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length.');  
--Returns 38  
  
```  
  
### <a name="c-using-an-odbc-functions-in-select-statements"></a>C. ODBC 関数を SELECT ステートメントで使用する  
 次の SELECT ステートメントでは、ODBC 関数が使用されています。  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
SELECT {fn OCTET_LENGTH( @string_exp )};  
-- Returns 38  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn TRUNCATE( 100.123456, 4)};  
-- Returns 100.123400  
SELECT {fn CURRENT_DATE( )};  
-- Returns 2007-04-20  
SELECT {fn CURRENT_TIME(6)};  
-- Returns 10:27:11.973000  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-an-odbc-function-in-a-stored-procedure"></a>D. ODBC 関数をストアド プロシージャで使用する  
 次の例では、ストアド プロシージャで、ODBC 関数を使用します。  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn BIT_LENGTH( @string_exp )};  
```  
  
### <a name="e-using-an-odbc-function-in-a-user-defined-function"></a>E. ODBC 関数をユーザー定義関数で使用する  
 次の例では、ODBC 関数をユーザー定義関数で使用しています。  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn BIT_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length in bits.');  
--Returns 432  
  
```  
  
### <a name="f-using-an-odbc-functions-in-select-statements"></a>F. ODBC 関数を SELECT ステートメントで使用する  
 次の SELECT ステートメントでは、ODBC 関数が使用されています。  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn CURRENT_DATE( )};  
-- Returns todays date  
SELECT {fn CURRENT_TIME(6)};  
-- Returns the time  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="see-also"></a>参照  
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



