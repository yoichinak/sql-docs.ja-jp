---
description: SQLSTATE マッピング
title: SQLSTATE マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14be1946b34433b0ff094cb79e2a1ec2ee849cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476404"
---
# <a name="sqlstate-mappings"></a>SQLSTATE マッピング
このトピックでは、ODBC 2.x *および odbc* *3. x*の SQLSTATE 値について説明します。 ODBC *3. x* SQLSTATE の値の詳細については、「 [付録 a: odbc エラーコード](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)」を参照してください。  
  
 ODBC 3.x では、S1xxx ではなく HYxxx SQLSTATEs が返され、S00XX ではなく 42 Sxx SQLSTATEs が返され *ます*。 これは、オープングループと ISO 標準に合わせて行われました。 多くの場合、マッピングは1対1ではありません。これは、標準によって複数の SQLSTATEs の解釈が再定義されているためです。  
  
 *Odbc 2.x アプリケーションを*odbc *2.x アプリケーションに*アップグレードする場合は、odbc 2.x sqlstates では*なく odbc* *2.x sqlstates*を想定するようにアプリケーションを変更する必要があります。 次の表に、各 ODBC 2.x*の SQLSTATE の*マップ先と*なる odbc 3.x*の状態を示します。  
  
 SQL_ATTR_ODBC_VERSION 環境属性が SQL_OV_ODBC2 に設定されている場合、ドライバーは、 **SQLGetDiagField**または**SQLGetDiagRec**が呼び出されたときに odbc 2.x sqlstates では*なく odbc 2.x* *sqlstates*をポストします。 特定のマッピングを決定するには、次の表の列1に *ある odbc 2.x で、odbc* *3.* x sqlstate (列 2) に対応する必要があります。  
  
|ODBC *2.x*|ODBC *3. x* SQLSTATE|コメント|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42 S01||  
|S0002|42 S02||  
|S0011|42 S11||  
|S0012|42 S12||  
|S0021|42 S21||  
|S0022|42 S22||  
|S0023|42 S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC 2.x S1002 は、基になる関数が**SQLBindCol**、 **sqlcolattribute**、 **SQLExtendedFetch**、 **sqlfetch**、 **sqlcolattribute**、または**SQLGetData**の場合に odbc *3. x* sqlstate 07009 にマップさ*れます。*|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Null ポインターの無効な使用に対して返されました。|  
|S1009|HY024|無効な属性値に対して返されます。|  
|S1009|HY092|同時実行が読み取り専用の場合に、 **SQLSetPos**への呼び出しによってデータを更新または削除したり、 **sqlbulkoperations**の呼び出しによってデータを追加、更新、または削除したりする場合に返されます。|  
|S1010|HY007 HY010|**SQLPrepare**、 **SQLExecDirect**、または*StatementHandle*のカタログ関数を呼び出す前に**SQLDescribeCol**が呼び出されると、sqlstate S1010 は sqlstate HY007 にマップされます。 それ以外の場合、SQLSTATE S1010 は SQLSTATE HY010 にマップされます。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3. x* sqlstate 07009 は、基になる関数が**SQLBindParameter**または**SQLDescribeParam**の場合 *、odbc 2.x* S1093 にマップされます。|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC *3. x* sqlstate 07008 は *、odbc 2.x* S1000 にマップされます。
