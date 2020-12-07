---
description: SQL_ARD_TYPE
title: SQL_ARD_TYPE |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826b5aa2ff103a2c2868a6bc1dc09fb8cad40382
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483165"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 型識別子は、バッファー内のデータが、の SQL_DESC_CONCISE_TYPE フィールドで指定された型であることを示すために使用されます。 SQL_ARD_TYPE は、特定のデータ型ではなく**SQLGetData**への呼び出しの*TargetType*引数に入力され、記述子フィールドを変更することによって、アプリケーションでバッファーのデータ型を変更できます。 この値は、 * \* targetvalueptr*バッファーのデータ型と記述子フィールドを結び付けます。 (SQL_ARD_TYPE は、バインドされたバッファーの型が既に SQL_DESC_TYPE および SQL_DESC_CONCISE_TYPE フィールドに関連付けられており、これらのフィールドのいずれかを変更することによっていつでも変更できるため、 **SQLBindCol** または **SQLBindParameter** の呼び出しには入力されません。)  
  
 SQL_ARD_TYPE 型識別子を使用すると、先頭の有効桁数と秒の有効桁数のデータ型の既定値、および SQL_C_NUMERIC データ型の有効桁数と小数点以下桁数の値を指定できます。 詳細については、この付録の後の「 [Interval データ型の既定の先頭および秒の有効桁数のオーバーライド](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) 」と「 [数値データ型の既定の有効桁数と小数点以下桁数のオーバーライド](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)」を参照してください。
