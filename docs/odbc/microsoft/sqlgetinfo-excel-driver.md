---
description: SQLGetInfo (Excel ドライバー)
title: SQLGetInfo (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Excel Driver
ms.assetid: fed4aea2-6d3d-4199-a5db-3d033eb63927
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d2cb149601f9c34bb7f0c35ca980a847b7948f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421756"
---
# <a name="sqlgetinfo-excel-driver"></a>SQLGetInfo (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 **SQLGetInfo** では、SQL_FILE_USAGE 情報の種類がサポートされています。 返される値は、ドライバーがデータソース内のファイルを直接扱う方法を示す16ビット整数です。  
  
-   SQL_FILE_NOT_SUPPORTED-ドライバーが単一層のドライバーではありません。  
  
-   SQL_FILE_TABLE-1 層ドライバーは、データソース内のファイルをテーブルとして扱います。  
  
-   SQL_FILE_QUALIFIER-1 層ドライバーは、データソース内のファイルを修飾子として扱います。  
  
 ODBC ドライバーは、各ファイルがテーブルであるため、Microsoft Exceldriver の SQL_FILE_TABLE を返します。  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ドライバー|Version|バージョン番号の形式|  
|----------|-------------|-------------------------------|  
|Microsoft Excel|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0/7.0|05.00.0000|  
||97/2000|08.00.0000|  
  
## <a name="sql_file_usage"></a>SQL_FILE_USAGE  
 SQL_FILE_TABLE (Excel 3.0/4.0)  
  
 SQL_FILE_CATALOG (Excel 5.0/7.0)  
  
## <a name="sql_max_char_literal_len"></a>SQL_MAX_CHAR_LITERAL_LEN  
 255 (Excel 3.0/4.0/5.0/7.0)  
  
 65535 (Excel 97)  
  
## <a name="sql_max_column_name_len"></a>SQL_MAX_COLUMN_NAME_LEN  
 30 (Excel 3.0/4.0)  
  
 64 (Excel 5.0/7.0/97)  
  
## <a name="sql_max_table_name_len"></a>SQL_MAX_TABLE_NAME_LEN  
 12 (Excel 3.0/4.0)  
  
 31 (Excel 5.0/7.0/97)  
  
## <a name="sql_catalog_name_separator"></a>SQL_CATALOG_NAME_SEPARATOR  
 " \\ " (Excel 3.0/4.0)  
  
 "."(Excel 5.0/7.0/97)  
  
## <a name="sql_catalog_term"></a>SQL_CATALOG_TERM  
 "ディレクトリ" (Excel 3.0/4.0)  
  
 "ブック" (Excel 5.0/7.0/97)  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
