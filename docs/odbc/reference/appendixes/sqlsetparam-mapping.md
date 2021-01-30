---
description: SQLSetParam のマッピング
title: SQLSetParam Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e2488c689a4da1152e115017287274252c6b405
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202628"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam のマッピング
**SQLSetParam** は、ODBC 2 の場合と同様に、 **SQLBindParameter** の上で引き続きマップされます。*x*。 概念的には **SQLBindParam** と似ていますが、ドライバーマネージャーは **SQLSetParam** を **SQLBindParam** にマップしません。 これは、特定の既存の ODBC 2 が原因です。*x* ドライバーは、 **SQLBindParameter** の上に **SQLSetParam** をマップするときにドライバーマネージャーによって生成される *bufferlength* (SQL_SETPARAM_VALUE_MAX) の特殊な値を使用して、1によっていつ呼び出されるかを判断します。*x* ODBC アプリケーション。  
  
 の呼び出し  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 次のようになります。  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
