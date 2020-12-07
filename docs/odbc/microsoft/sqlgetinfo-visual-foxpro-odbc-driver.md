---
description: SQLGetInfo (Visual FoxPro ODBC ドライバー)
title: SQLGetInfo (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 370661a9a0ade5c5159f93a9af37c17b675032c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421676"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル1  
  
 Visual FoxPro ODBC ドライバーと、接続ハンドル *hdbc*に関連付けられたデータソースに関する一般的な情報を返します。 次の一覧は、各 *Fintype* 引数と、返された値に関するコメントについて、VISUAL FoxPro ODBC ドライバーによって返される値を示しています。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) 」を参照してください。  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES は ' N ' を返します。  
  
 SQL_ACCESSIBLE_TABLES は ' Y ' を返します。  
  
 SQL_ACTIVE_CONNECTIONS は0を返します。  
  
 SQL_ACTIVE_STATEMENTS は0を返します。  
  
 SQL_ALTER_TABLE は SQL_AT_ADD_COLUMN または SQL_AT_DROP_COLUMN のいずれかを返します。  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE は SQL_BP_SCROLL を返します。  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS は ' Y ' を返します。  
  
 SQL_CONCAT_NULL_BEHAVIOR は SQL_CB_NULL を返します。  
  
 SQL_CONVERT_BIGINT は0を返します。 Visual FoxPro ODBC ドライバーでは、 *BigInt*はサポートされていません。  
  
 SQL_CONVERT_BINARY は0を返します。  
  
 SQL_CONVERT_BIT は0を返します。  
  
 SQL_CONVERT_CHAR は0を返します。  
  
 SQL_CONVERT_DATE は0を返します。  
  
 SQL_CONVERT_DECIMAL は0を返します。  
  
 SQL_CONVERT_DOUBLE は0を返します。  
  
 SQL_CONVERT_FLOAT は0を返します。  
  
 SQL_CONVERT_INTEGER は0を返します。  
  
 SQL_CONVERT_LONGVARBINARY は0を返します。  
  
 SQL_CONVERT_LONGVARCHAR は0を返します。  
  
 SQL_CONVERT_NUMERIC は0を返します。  
  
 SQL_CONVERT_REAL は0を返します。  
  
 SQL_CONVERT_SMALLINT は0を返します。  
  
 SQL_CONVERT_TIME は0を返します。  
  
 SQL_CONVERT_TIMESTAMP は0を返します。  
  
 SQL_CONVERT_TINYINT は0を返します。  
  
 SQL_CONVERT_VARBINARY は0を返します。  
  
 SQL_CONVERT_VARCHAR は0を返します。  
  
 SQL_CONVERT_FUNCTIONS は0を返します。  
  
 SQL_CORRELATION_NAME は SQL_CN_ANY を返します。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR は SQL_CB_PRESERVE を返します。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR は SQL_CB_PRESERVE を返します。  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME は、DSN として [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)または [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)に渡された値を返します。DSN が指定されていない場合は、空の文字列を返します。  
  
 SQL_DATA_SOURCE_READ_ONLY は ' N ' を返します。  
  
 データソースが [データベース](../../odbc/microsoft/visual-foxpro-terminology.md)の場合、SQL_DATABASE_NAME は、現在のデータベースへの完全な UNC パスを返します。 データソースが [テーブル](../../odbc/microsoft/visual-foxpro-terminology.md)のディレクトリに接続する場合、関数はディレクトリへのパスを返します。  
  
 SQL_DBMS_NAME は "Visual FoxPro" を返します。  
  
 SQL_DBMS_VER は "03.00.0000" を返します。  
  
 SQL_DEFAULT_TXN_ISOLATION は SQL_TXN_READ_COMMITTED を返します。 ダーティリードはできませんが、反復不可能な読み取りとファントムが可能です。  
  
 SQL_DRIVER_HDBC は、ドライバーマネージャーによって実装されます。  
  
 SQL_DRIVER_HENV は、ドライバーマネージャーによって実装されます。  
  
 SQL_DRIVER_HLIB は、ドライバーマネージャーによって実装されます。  
  
 SQL_DRIVER_HSTMT は、ドライバーマネージャーによって実装されます。  
  
 SQL_DRIVER_NAME は "vfpodbc.dll" を返します。  
  
 SQL_DRIVER_ODBC_VER によって "02.50" (SQL_SPEC_MAJOR、SQL_SPEC_MINOR) が返されます。  
  
 SQL_DRIVER_VER は "01.00.0000" を返します。  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY は ' N ' を返します。  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION は次の値を返します。  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK。  
  
 SQL_FILE_USAGE は、データベース (dbc ファイル) とフリーテーブル (.dbf ファイル) データソースの両方 SQL_FILE_QUALIFIER を返します。  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS は次の値を返します。  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY は SQL_GB_NO_RELATION を返します。  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE は SQL_IC_MIXED を返します。  
  
 SQL_IDENTIFIER_QUOTE_CHAR は ' を返します。  
  
## <a name="k"></a>K  
 SQL_KEYWORDS は "" を返します。  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE は ' N ' を返します。  
  
 SQL_LOCK_TYPES は SQL_LCK_NO_CHANGE を返します。  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN は0を返します。  
  
 SQL_MAX_CHAR_LITERAL_LEN は254を返します。  
  
 SQL_MAX_COLUMN_NAME_LEN は128を返します。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY は16を返します。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY は16を返します。  
  
 SQL_MAX_COLUMNS_IN_INDEX は0を返します。  
  
 SQL_MAX_COLUMNS_IN_SELECT は254を返します。  
  
 SQL_MAX_COLUMNS_IN_TABLE は254を返します。  
  
 SQL_MAX_CURSOR_NAME_LEN は254を返します。  
  
 SQL_MAX_INDEX_SIZE は0を返します。  
  
 SQL_MAX_OWNER_NAME_LEN は0を返します。  
  
 SQL_MAX_PROCEDURE_NAME_LEN は0を返します。 Visual FoxPro ODBC ドライバーでは、Visual FoxPro ストアドプロシージャに直接アクセスすることはできません。  
  
 SQL_MAX_QUALIFIER_NAME_LEN は、オペレーティングシステムの最大パス長を返します。  
  
 SQL_MAX_ROW_SIZE は 254 ^ 2 を返します。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG は ' N ' を返します。  
  
 SQL_MAX_STATEMENT_LEN は8192を返します。  
  
 SQL_MAX_TABLE_NAME_LEN は128を返します。  
  
 SQL_MAX_TABLES_IN_SELECT は16を返します。  
  
 SQL_MAX_USER_NAME_LEN は0を返します。  
  
 SQL_MULT_RESULT_SETS は ' Y ' を返します。  
  
 SQL_MULTIPLE_ACTIVE_TXN は ' Y ' を返します。 複数の接続で複数のトランザクションを同時に開くことができます。  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN は ' N ' を返します。  
  
 SQL_NON_NULLABLE_COLUMNS は SQL_NNC_NON_NULL を返します。  
  
 SQL_NULL_COLLATION は SQL_NC_LOW を返します。  
  
 SQL_NUMERIC_FUNCTIONS は SQL_FN_NUM_POWER を除くすべての関数を返します。これは、Visual FoxPro ODBC ドライバーではサポートされていません。 次の関数がサポートされています。  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE は SQL_OAC_LEVEL1 を返します。  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE は SQL_OSCC_COMPLIANT を返します。  
  
 SQL_ODBC_SQL_CONFORMANCE は SQL_OSC_MINIMUM を返します。 最小 SQL 構文がサポートされています。  
  
 SQL_ODBC_SQL_OPT_IEF は "N" を返します。  
  
 SQL_ODBC_VER は、ドライバーマネージャーによって実装されます。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT は "N" を返します。  
  
 SQL_OUTER_JOINS は "N" を返します。  
  
 SQL_OWNER_TERM は "" を返します。 Visual FoxPro ODBC ドライバーでは、オブジェクトの所有者はサポートされていません。  
  
 SQL_OWNER_USAGE は0を返します。 Visual FoxPro ODBC ドライバーでは、オブジェクトの所有者はサポートされていません。  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS は SQL_POS_POSITION を返します。  
  
 SQL_POSITIONED_STATEMENTS は0を返します。  
  
 SQL_PROCEDURE_TERM は "" を返します。  
  
 SQL_PROCEDURES は ' N ' を返します。  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION は SQL_QL_START を返します。  
  
 SQL_QUALIFIER_NAME_SEPARATOR は '! ' または ' ' を返し \\ ます。 データベースとテーブルの間の区切り記号は、 [データベース](../../odbc/microsoft/visual-foxpro-terminology.md)に接続されているデータソースの場合は '! '、 \\ [フリーテーブル](../../odbc/microsoft/visual-foxpro-terminology.md)のディレクトリであるデータソースの場合は ' ' です。  
  
 SQL_QUALIFIER_TERM は "database" または "directory" を返します。 修飾子は、 [データベース](../../odbc/microsoft/visual-foxpro-terminology.md)に接続されているデータソースの場合は "database"、 [フリーテーブル](../../odbc/microsoft/visual-foxpro-terminology.md)のディレクトリであるデータソースの場合は "directory" です。  
  
 SQL_QUALIFIER_USAGE は SQL_QU_PRIVILEGE_DEFINITION をサポートしていません。SQL_QU_DML_STATEMENT または SQL_QU_TABLE_DEFINITION のいずれかが返されます。  
  
 SQL_QUOTED_IDENTIFIER_CASE は SQL_IC_MIXED を返します。  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES は "N" を返します。 Visual FoxPro ODBC ドライバーでは、静的カーソルと転送カーソルのみがサポートされています。  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY は SQL_SCCO_READ_ONLY を返します。  
  
 SQL_SCROLL_OPTIONS は SQL_SO_STATIC または SQL_SO_READONLY のいずれかを返します。  
  
 SQL_SEARCH_PATTERN_ESCAPE は " \\ " を返します。  
  
 SQL_SERVER_NAME は "" を返します。  
  
 SQL_SPECIAL_CHARACTERS は "~ @ # $% ^" を返します。  
  
 SQL_STATIC_SENSITIVITY は0を返します。 Visual FoxPro ODBC ドライバーでは、位置指定更新はサポートされていません。  
  
 SQL_STRING_FUNCTIONS では、SQL_FN_STR_INSERT、SQL_FN_STR_LOCATE、SQL_FN_STR_LOCATE_2、または SQL_FN_STR_SOUNDEX はサポートされていません。  
  
 戻り値は次のとおりです。  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE。  
  
 SQL_SUBQUERIES は次の値を返します。  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED。  
  
 SQL_SYSTEM_FUNCTIONS は次の値を返します。  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 ただし、次のことはできません。  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM は "TABLE" を返します。  
  
 SQL_TIMEDATE_ADD_INTERVALS は次の値を返します。  
  
-   SQL_FN_TSI_ 秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 ただし、次のことはできません。  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS は次の値を返します。  
  
-   SQL_FN_TSI_ 秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS では、SQL_FN_TD_QUARTER、SQL_FN_TD_TIMESTAMPADD、SQL_FN_TD_DAYOFYEAR、または SQL_FN_TD_WEEK はサポートされていません。  
  
 戻り値は次のとおりです。  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR。  
  
 SQL_TXN_CAPABLE は SQL_TC_DML を返します。  
  
 SQL_TXN_ISOLATION_OPTION は SQL_TXN_READ_COMMITTED を返します。  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION は SQL_U_UNION または SQL_U_UNION_ALL のいずれかを返します。  
  
 SQL_USER_NAME はを返し \<blank> ます。
