---
description: SQL-92 CAST 関数
title: SQL-92 CAST 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7818cd653ac770de8f3d78d8599da5b66c4cf768
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424934"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 関数
SQL-92 で定義されている **CAST** 関数は、ODBC で定義されている **CONVERT** 関数に相当します。 同等の関数の構文は次のとおりです。  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **CAST** 関数は、他のデータ型に変換できるデータ型を指定します。 (詳細については、「SQL-92 の仕様」を参照してください)。 **CAST** 関数は FIPS 移行レベルでサポートされています。  
  
 アプリケーションでは、 **キャスト** 関数のサポートを次のように決定できます。  
  
1.  SQL_SQL_CONFORMANCE 情報の種類を使用して **SQLGetInfo** を呼び出します。 情報型の戻り値が SQL_SC_FIPS127_2_TRANSITIONAL、SQL_SC_SQL92_INTERMEDIATE、または SQL_SC_SQL92_FULL の場合、 **CAST** 関数はサポートされています。  
  
2.  SQL_SQL_CONFORMANCE 情報の種類の戻り値が SQL_SC_ENTRY_LEVEL または0の場合は、SQL_SQL92_VALUE_EXPRESSIONS 情報の種類を使用して **SQLGetInfo** を呼び出します。 SQL_SVE_CAST ビットが設定されている場合、 **CAST** 関数がサポートされます。
