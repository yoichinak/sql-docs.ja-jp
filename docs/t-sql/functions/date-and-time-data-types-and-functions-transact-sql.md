---
title: "日付と時刻のデータ型および関数 (Transact-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
caps.latest.revision: "79"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 05ce8f3240590e1be28722ded5a526ad2dd2d6df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>日付と時刻のデータ型および関数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

このトピックの以下のセクションでは、日付と時刻に関連して [!INCLUDE[tsql](../../includes/tsql-md.md)] が備えているすべてのデータ型および関数について概要を紹介します。
-   [日付と時刻のデータ型](#DateandTimeDataTypes)  
-   [日付と時刻関数](#DateandTimeFunctions)  
    -   [システム日付と時刻の値を取得する関数](#GetSystemDateandTimeValues)  
    -   [日付と時刻の部分を取得する関数](#GetDateandTimeParts)  
    -   [要素から日付と時刻の値を取得する関数](#fromParts)  
    -   [日付と時刻の差を取得する関数](#GetDateandTimeDifference)  
    -   [日付と時刻の値を変更する関数](#ModifyDateandTimeValues)  
    -   [セッションの形式を設定または取得する関数](#SetorGetSessionFormatFunctions)  
    -   [日付と時刻の値を検証する関数](#ValidateDateandTimeValues)  
-   [日付と時間に関連するトピック](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>日付と時刻のデータ型
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型を次の表に示します。
  
|データ型|形式|範囲|精度|記憶域のサイズ (バイト単位)|ユーザー定義の 1 秒未満の秒の有効桁数|タイム ゾーン オフセット|  
|---|---|---|---|---|---|---|  
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 ～ 23:59:59.9999999|100 ナノ秒|3 ～ 5|可|不可|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01 ～ 31.12.99|1 日|3|不可|不可|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01 ～ 2079-06-06|1 分|4|不可|不可|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01 ～ 9999-12-31|0.00333 秒|8|不可|不可|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 ～ 9999-12-31 23:59:59.9999999|100 ナノ秒|6 ～ 8|可|不可|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-MM-DD hh:mm:ss [.nnnnnnn] [+ &#124;-] hh:mm|0001-01-01 00:00:00.0000000 ～ 9999-12-31 23:59:59.9999999 (UTC)|100 ナノ秒|8 ～ 10|可|可|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] [Rowversion](../../t-sql/data-types/rowversion-transact-sql.md) データ型は、日付や時刻のデータ型ではありません。**timestamp** は、**rowversion** の非推奨シノニムです。  
  
##  <a name="DateandTimeFunctions"></a>日付と時刻関数  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻の関数を次の表に示します。 決定性の詳細については、「[決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。
  
###  <a name="GetSystemDateandTimeValues"></a>システム日付と時刻の値を取得する関数 
システムのすべての日付値と時刻値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピュータのオペレーティング システムから取得されます。
  
#### <a name="higher-precision-system-date-and-time-functions"></a>高精度のシステム日付/時刻関数  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]は、GetSystemTimeAsFileTime() Windows API を使用して日付と時刻の値を取得します。 精度は、コンピューターのハードウェアとする Windows のバージョンによって異なります。 のインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が実行されています。 この API の精度は 100 ナノ秒で固定されます。 GetSystemTimeAdjustment() Windows API を使用して、精度を確認できます。
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピュータの日付と時刻を含む **datetime2(7)** 値を返します。タイム ゾーン オフセットは含まれません。|**datetime2(7)**|非決定的|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピュータの日付と時刻を含む **datetimeoffset(7)** 値を返します。タイム ゾーン オフセットが含まれます。|**datetimeoffset (7)**|非決定的|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピュータの日付と時刻を含む **datetime2(7)** 値を返します。日付と時刻は UTC 時刻 (協定世界時) で返されます。|**datetime2(7)**|非決定的|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>低精度のシステム日付と時刻関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピュータの日付と時刻を含む **datetime** 値を返します。タイム ゾーン オフセットは含まれません。|**datetime**|非決定的|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピュータの日付と時刻を含む **datetime** 値を返します。タイム ゾーン オフセットは含まれません。|**datetime**|非決定的|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピュータの日付と時刻を含む **datetime** 値を返します。日付と時刻は UTC 時刻 (協定世界時) で返されます。|**datetime**|非決定的|  
  
###  <a name="GetDateandTimeParts"></a>日付と時刻の部分を取得する関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* ,*date*)|指定された日付について、特定の *datepart* を表す文字列を返します。|**nvarchar**|非決定的|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* ,*date*)|指定された *date* の特定の *datepart* を表す整数を返します。|**int**|非決定的|  
|[DAY](../../t-sql/functions/day-transact-sql.md)|DAY ( *date* )|指定された *date* の日の部分を表す整数を返します。|**int**|決定的|  
|[MONTH](../../t-sql/functions/month-transact-sql.md)|MONTH ( *date* )|指定された *date* の月の部分を表す整数を返します。|**int**|決定的|  
|[YEAR](../../t-sql/functions/year-transact-sql.md)|YEAR ( *date* )|指定された *date* の年の部分を表す整数を返します。|**int**|決定的|  
  
###  <a name="fromParts"></a>要素から日付と時刻の値を取得する関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS (*year*,*month*,*day*)|指定した年、月、および日の **date** 値を返します。|**date**|決定的|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS (*year*,*month*,*day*,*hour*,*minute*, *seconds*,*fractions*,*precision*)|指定された有効桁数を使用して、指定した日付と時刻の **datetime2** 値を返します。|**datetime2(** *precision* **)**|決定的|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS (*year*,*month*,*day*,*hour*,*minute*, *seconds*,*milliseconds*)|指定した日付と時刻の **datetime** 値を返します。|**datetime**|決定的|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS (*year*,*month*,*day*,*hour*,*minute*, *seconds*,*fractions*, *hour_offset*, *minute_offset*,*precision*)|指定されたオフセットおよび有効桁数を使用して、指定した日付と時刻の **datetimeoffset** 値を返します。|**datetimeoffset(** *precision* **)**|決定的|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS (*year*,*month*,*day*,*hour*,*minute*)|指定した日付と時刻の **smalldatetime** 値を返します。|**smalldatetime**|決定的|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS (*hour*,*minute*,*seconds*,*fractions*,*precision*)|指定された有効桁数を使用して、指定した時間の **time** 値を返します。|**time(** *precision* **)**|決定的|  
  
###  <a name="GetDateandTimeDifference"></a>日付と時刻の差を取得する関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|指定された 2 つの日付間の差を、日付または時刻の *datepart* 単位で返します。|**int**|決定的|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|指定された 2 つの日付間の差を、日付または時刻の *datepart* 単位で返します。|**bigint**|決定的|  
  
###  <a name="ModifyDateandTimeValues"></a>日付と時刻の値を変更する関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD ( *datepart*, *number*, *date* )|*date* の *datepart* に特定の期間を加えた新しい **datetime** 型の値を返します。|*date* 引数のデータ型|決定的|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *start_date* \[, *month_to_add* \] )|オプションのオフセットを使用して、指定された日付を含んでいる月の最後の日付を返します。|戻り値の型は、 *start_date* の型または **date**です。|決定的|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCHOFFSET(*DATETIMEOFFSET* , *time_zone*)|SWITCHOFFSETは *DATETIMEOFFSET* 値のタイム ゾーン オフセットを変更し、UTC 値を保持します。|*DATETIMEOFFSET* の有効桁数を持つ **datetimeoffset**|決定的|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expression*, *time_zone*)|TODATETIMEOFFSET は、datetime2 値を datetimeoffset 値に変換します。 datetime2 値は、指定された time_zone のローカル時刻で解釈されます。|*datetime* 引数の有効桁数を持つ **datetimeoffset**|決定的|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>セッションの形式を設定または取得する関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST |現在のセッションにおける、SET DATEFIRST の現在の値を返します。|**tinyint**|非決定的|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST {*number* &#124; **@** *number_var* }|週の最初の曜日を 1 ～ 7 の数値で設定します。|適用なし|適用なし|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT {*format* &#124; **@** *format_var* }|**datetime** 型または **smalldatetime** 型のデータを入力する場合の日付要素 (月、日、年) の順番を設定します。|適用なし|適用なし|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE |現在使用されている言語の名前を返します。 @@LANGUAGE は日付または時刻の関数ではありません。 ただし、言語設定は日付関数の出力に影響します。|適用なし|適用なし|  
|[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {\[N\] **'***language***'** &#124; **@** *language_var* }|セッションおよびシステム メッセージの言語環境を設定します。 SET LANGUAGE は日付または時刻の関数ではありません。 ただし、言語設定には、日付関数の出力が影響します。|適用なし|適用なし|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [  **@language =** ] **'***language***'** ]|サポートされている言語の日付形式に関する情報を返します。 **sp_helplanguage** は日付または時刻のストアド プロシージャではありません。 ただし、言語設定には、日付関数の出力が影響します。|適用なし|適用なし|  
  
###  <a name="ValidateDateandTimeValues"></a>日付と時刻の値を検証する関数
  
|関数|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE (*expression*)|**datetime** または **smalldatetime** の入力式が有効な日付値または時刻値であるかどうかを調べます。|**int**|ISDATE は、CONVERT 関数と共に使用され、CONVERT スタイル パラメーターが指定されており、スタイルが 0、100、9、または 109 と等しくない場合にのみ決定的関数になります。|  
  
##  <a name="DateandTimeRelatedTopics"></a>日付と時間に関連するトピック 
  
|トピック|Description|  
|-----------|-----------------|  
|[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|文字列リテラルとその他の日付/時刻形式間の変換に関する情報を提供します。|  
|[国際化に対応した Transact-SQL ステートメントの記述](../../relational-databases/collations/write-international-transact-sql-statements.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用するデータベースやデータベース アプリケーションをある言語から別の言語に移行するためのガイドラインを提供します。|  
|[ODBC スカラー関数 &#40;Transact-SQL&#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで使用できる ODBC スカラ関数に関する情報を提供します。これには、ODBC の日付および時刻の関数が含まれます。|  
|[タイム ゾーン &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|タイム ゾーンの変換を提供します。|  
  
## <a name="see-also"></a>参照
[関数](../../t-sql/functions/functions.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
