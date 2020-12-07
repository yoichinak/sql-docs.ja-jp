---
description: C データ型
title: C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dadd93f13418d520c4ab908ba0d9402d07c893a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421526"
---
# <a name="c-data-types"></a>C データ型
ODBC C データ型は、アプリケーションにデータを格納するために使用される C バッファーのデータ型を示します。  
  
 すべてのドライバーは、すべての C データ型をサポートしている必要があります。 すべてのドライバーは、サポートされる SQL 型を変換できるすべての C 型をサポートする必要があり、すべてのドライバーが少なくとも1文字の SQL 型をサポートしているため、このことが必要です。 文字の SQL 型はすべての C 型に変換できるので、すべてのドライバーがすべての c 型をサポートしている必要があります。  
  
 C データ型は、 **SQLBindCol** 関数と **SQLGetData** 関数で、 *TargetType* 引数と **SQLBindParameter** 関数の *ValueType* 引数を使用して指定されます。 また、 **SQLSetDescField**を呼び出して、SQLSetDescRec または APD の SQL_DESC_CONCISE_TYPE フィールドを設定するか、または*型*引数 (および必要に応じて*SubType*引数) を指定してを呼び出すことによって、または、 **SQLSetDescRec**または APD のハンドルに設定された*記述子ハンドル*引数を指定することもできます。  
  
 次の表に、C データ型の有効な型識別子を示します。 この表には、各識別子とこのデータ型の定義に対応する ODBC C データ型も一覧表示されています。  
  
|C 型識別子|ODBC C typedef|C 型|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSマル糸|unsigned short int|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE、SQLDOUBLE|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT [j]|SQL・ AR|signed char|  
|SQL_C_UTINYINT [j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|署名されていない _int64 [h]|  
|SQL_C_BINARY|SQLCHAR|unsigned char *|  
|SQL_C_BOOKMARK [i]|ブックマーク|unsigned long int [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|  
|すべての C interval データ型|SQL_INTERVAL_STRUCT|この付録の後半の「 [C の間隔構造](../../../odbc/reference/appendixes/c-interval-structure.md) 」を参照してください。|  
  
 **C 型識別子** SQL_C_TYPE_DATE [C]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **C 型**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 型識別子** SQL_C_TYPE_TIME [C]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **C 型**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 型識別子** SQL_C_TYPE_TIMESTAMP [C]  
  
 **ODBC C typedef** SQL_TIMESTAMP_STRUCT  
  
 **C 型**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **C 型識別子** SQL_C_NUMERIC  
  
 **ODBC C typedef** SQL_NUMERIC_STRUCT  
  
 **C 型**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C 型識別子** SQL_C_GUID  
  
 **ODBC C typedef** SQLGUID  
  
 **C 型**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] datetime C データ型の年、月、日、時、分、および秒の各フィールドの値は、グレゴリオ暦の制約に準拠している必要があります。 (この付録の後半 [の「グレゴリオ暦の制約](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) 」を参照してください)。  
  
 [b] 分数フィールドの値は、秒の billionths の数であり、0 ~ 999999999 の範囲 (1 は10億未満) です。 たとえば、0.5 秒の小数フィールドの値は5億で、1秒の 1/1000 (1 ミリ秒) は100万で、秒の万 (1 マイクロ秒) は1000で、10億分の場合は1秒間になります (1 ナノ秒)。  
  
 [c] (ODBC 2)。*x*、C 日付、時刻、およびタイムスタンプデータ型は、SQL_C_DATE、SQL_C_TIME、および SQL_C_TIMESTAMP です。  
  
 [d] ODBC 3 *. x* アプリケーションでは、SQL_C_BOOKMARK ではなく SQL_C_VARBOOKMARK を使用する必要があります。 Odbc 3 *. x* アプリケーションが odbc 2 で動作する場合。*x* ドライバーは、ODBC 3 *. x* ドライバーマネージャーが SQL_C_VARBOOKMARK を SQL_C_BOOKMARK にマップします。  
  
 [e] 数値は、スケールされた整数として SQL_NUMERIC_STRUCT 構造体の *val* フィールドに格納されます。これはリトルエンディアンモード (一番左のバイトが最下位バイト) です。 たとえば、小数点以下桁数が4の10.001 基数10は、整数100010にスケーリングされます。 これは186AA の16進数形式であるため、SQL_NUMERIC_STRUCT の値は "AA 86 01 00 00...00 "の場合は、SQL_MAX_NUMERIC_LEN **#define**によって定義されたバイト数を指定します。  
  
 **SQL_NUMERIC_STRUCT**の詳細については、「 [HOWTO: SQL_NUMERIC_STRUCT を使用した数値データの取得](retrieve-numeric-data-sql-numeric-struct-kb222831.md)」を参照してください。  
  
 [f] SQL_C_NUMERIC のデータ型の有効桁数および小数点以下桁数のフィールドは、アプリケーションからの入力、およびドライバーからアプリケーションへの出力に使用されます。 ドライバーは、SQL_NUMERIC_STRUCT に数値を書き込むときに、独自のドライバー固有の既定値を *有効桁数* フィールドの値として使用し、 *スケール* フィールドのアプリケーション記述子の SQL_DESC_SCALE フィールド (既定値は 0) の値を使用します。 アプリケーションでは、アプリケーション記述子の SQL_DESC_PRECISION および SQL_DESC_SCALE フィールドを設定することによって、有効桁数と小数点以下桁数の固有の値を指定できます。  
  
 [g] 符号フィールドは正の場合は1、負の場合は0になります。  
  
 [h] _int64 一部のコンパイラでは提供されない可能性があります。  
  
 [i] _SQL_C_BOOKMARK は ODBC 3.x では非推奨*となりました。*  
  
 [j] _SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT は、符号付きおよび符号なしの型によって ODBC で置き換えられました。 SQL_C_SSHORT と SQL_C_USHORT、SQL_C_SLONG と SQL_C_ULONG、および SQL_C_STINYINT と SQL_C_UTINYINT です。 Odbc 2 で動作する ODBC*3.x ドライバー。**x*アプリケーションは SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT をサポートする必要があります。これらが呼び出されると、ドライバーマネージャーによってドライバーに渡されます。  
  
 [k] SQL_C_GUID SQL_CHAR または SQL_WCHAR にのみ変換できます。  
  
 ここでは、次のトピックについて説明します。  
  
-   [64 ビットの整数の構造](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>参照  
 [ODBC の C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
