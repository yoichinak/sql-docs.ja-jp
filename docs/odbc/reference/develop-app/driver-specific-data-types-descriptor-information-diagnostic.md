---
description: ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性
title: ドライバー固有の種類-データ、記述子、情報、診断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a0ac3fd67e07f23f14420ee46ccda5cd409f87a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483005"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性
ドライバーは、次の目的でドライバー固有の値を割り当てることができます。  
  
-   **SQL データ型インジケーター**これらは、 **SQLBindParameter**の*ParameterType*と**SQLGetTypeInfo**の*データ型*で使用され、 **sqlcolattribute**、 **Sqlcolumns**、 **SQLDescribeCol**、 **SQLGetTypeInfo**、 **SQLDescribeParam**、 **SQLProcedureColumns**、および**sql 列**によって返されます。  
  
-   **記述子フィールド**これらは、 **Sqlcolattribute**、 **SQLGetDescField**、および**SQLSetDescField**の*FieldIdentifier*で使用されます。  
  
-   **診断フィールド**これらは、 **SQLGetDiagField**および**SQLGetDiagRec**の*DiagIdentifier*で使用されます。  
  
-   **情報の種類**これらは、 **SQLGetInfo**の*InfoType*で使用されます。  
  
-   **接続属性とステートメント属性**これらは、 **Sqlgetconnectattr**、 **SQLGetStmtAttr**、 **SQLSetConnectAttr**、および**SQLSetStmtAttr**の*属性*で使用されます。  
  
 これらの各項目には、2つの値のセットがあります。 ODBC によって使用されるように予約されている値と、ドライバーで使用するために予約されている値です。 ドライバー固有の値を実装する前に、ドライバーの作成者は、開いているグループのドライバー固有の型、フィールド、または属性ごとに値を要求する必要があります。 新しいドライバーを開発する場合は、次の表に記載されている範囲を使用します。 次に示す範囲外の不明な値が使用されている場合、ODBC 3.8 Driver Manager ではエラーは生成されません。 ただし、それ以降のバージョンのドライバーマネージャーでは、範囲外の不明な値を受信した場合にエラーが発生する可能性があります。  
  
 これらの値のいずれかが ODBC 関数に渡されると、ドライバーは値が有効であるかどうかを確認する必要があります。 ドライバーは、他のドライバーに適用されるドライバー固有の値の SQLSTATE HYC00 (オプションの機能は実装されていません) を返します。  
  
 ODBC 3.8 以降では、ドライバーライターは予約された範囲内でドライバー固有の属性を割り当てることができます。  
  
> [!NOTE]  
>  ODBC 3.8 Driver Manager は、旧バージョンとの互換性のためにこれらの範囲を検証または適用しません。 ただし、ドライバーマネージャーの将来のバージョンでは、ドライバーマネージャーが強制的に適用される可能性があります。  
  
|属性の型|ODBC データ型|ドライバー固有の範囲のベース|ドライバー固有の範囲制限|ドライバー固有の値範囲ベースの ODBC 定数|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL データ型インジケーター|SQLSMALLINT|0x4000|~|SQL_DRIVER_SQL_TYPE_BASE|  
|記述子フィールド|SQLSMALLINT|0x4000|~|SQL_DRIVER_DESCRIPTOR_BASE|  
|診断フィールド|SQLSMALLINT|0x4000|~|SQL_DRIVER_DIAGNOSTIC_BASE|  
|情報の種類|SQLUSマル糸|0x4000|~|SQL_DRIVER_INFO_TYPE_BASE|  
|接続属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|ステートメントの属性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  ドライバー固有のデータ型、記述子フィールド、診断フィールド、情報の種類、ステートメント属性、および接続属性については、ドライバーのドキュメントを参照してください。 これらの値のいずれかが ODBC 関数に渡されると、ドライバーは値が有効であるかどうかを確認する必要があります。 ドライバーは、他のドライバーに適用されるドライバー固有の値の SQLSTATE HYC00 (オプションの機能は実装されていません) を返します。  
  
 基本値は、ドライバーの開発を容易にするために定義されています。 たとえば、ドライバー固有の診断属性は、次の形式で定義できます。  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
