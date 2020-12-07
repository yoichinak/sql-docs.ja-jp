---
description: データ型識別子の使用
title: データ型識別子の使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 54fe7267ea70dc50b0b40f16b27a1306fea533f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386278"
---
# <a name="using-data-type-identifiers"></a>データ型識別子の使用
アプリケーションでは、2つの方法でデータ型識別子を使用します。ドライバーにバッファーを記述し、その結果セットに関するメタデータをドライバーから取得して、データの格納に使用する C バッファーの種類を決定できるようにします。 アプリケーションは、次の関数を呼び出してこれらのタスクを実行します。  
  
-   **SQLBindParameter**、 **SQLBindCol**、および **SQLGetData** -アプリケーションバッファーの C データ型について説明します。  
  
-   **SQLBindParameter** -動的パラメーターの SQL データ型について説明します。  
  
-   **Sqlcolattribute** と **SQLDescribeCol** -結果セット列の SQL データ型を取得します。  
  
-   **SQLDescribeParameter** -パラメーターの SQL データ型を取得します。  
  
-   **Sqlcolumns**、 **SQLProcedureColumns**、および **sqlcolumns な列** -さまざまなスキーマ情報の SQL データ型を取得します。  
  
-   **SQLGetTypeInfo** -サポートされているデータ型の一覧を取得するには  
  
 データ型識別子は、記述子の SQL_DESC_CONCISE_TYPE フィールドに格納されます。 記述子関数 **SQLSetDescField** と **SQLSetDescRec** を適切な型と共に使用して、前の一覧に一覧表示されているタスクを実行できます。 詳細については、「 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」を参照してください。
