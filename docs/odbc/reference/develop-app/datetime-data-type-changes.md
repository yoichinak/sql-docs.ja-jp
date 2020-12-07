---
description: datetime データ型の変更
title: Datetime データ型の変更 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a36339f275ff03584a3682f9f57eeeb8445faf3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424754"
---
# <a name="datetime-data-type-changes"></a>datetime データ型の変更
*ODBC 3.x では、日付*、時刻、およびタイムスタンプの SQL データ型の識別子が、SQL_DATE、SQL_TIME、および SQL_TIMESTAMP (ヘッダーファイル (9、10、および11の **#define**インスタンス) から SQL_TYPE_DATE、SQL_TYPE_TIME、および SQL_TYPE_TIMESTAMP (ヘッダーファイル91、92、93 **) に**それぞれ変更されました。 対応する C 型識別子が SQL_C_DATE、SQL_C_TIME、および SQL_C_TIMESTAMP から、それぞれ SQL_C_TYPE_DATE、SQL_C_TYPE_TIME、および SQL_C_TYPE_TIMESTAMP に変更されました。  
  
 *Odbc 3.x*の SQL datetime データ型に対して返される列サイズと10進桁数は、odbc 2.x で返される有効桁数および小数点以下桁数と*同じです。* これらの値は、SQL_DESC_PRECISION および SQL_DESC_SCALE の記述子フィールドの値とは異なります。 (詳細については、「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください)。  
  
 これらの変更は、 **SQLDescribeCol**、 **SQLDescribeParam**、および **sqlcolattribute**に影響します。 **SQLBindCol**、 **SQLBindParameter**、および **SQLGetData**;および **Sqlcolumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **sqlcolumns**、および **sqlcolumns 列**。  
  
 次の表は *、ODBC 3.X* Driver Manager が、 **SQLBindCol**および**SQLGetData**の*TargetType*引数に入力された日付、時刻、およびタイムスタンプの C データ型のマッピングを実行する方法、または**SQLBindParameter**の*ValueType*引数に含まれる方法を示しています。  
  
|データ型<br /><br /> 入力されたコード|*2. x* アプリから<br /><br /> *2.x* 2.x ドライバー|*2. x* アプリから<br /><br /> *3.x* 3.x ドライバー|*3. x* アプリから<br /><br /> *2.x* 2.x ドライバー|*3. x* アプリから<br /><br /> *3.x* 3.x ドライバー|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|マッピングなし|SQL_C_TYPE_DATE (91)|マッピング [1] はありません|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|エラー (DM から)|エラー (DM から)|SQL_C_DATE (9)|マッピング [2] がありません|  
|SQL_C_TIME (10)|マッピングなし|SQL_C_TYPE_TIME (92)|マッピング [1] はありません|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|エラー (DM から)|エラー (DM から)|SQL_C_TIME (10)|マッピング [2] がありません|  
|SQL_C_TIMESTAMP (11)|マッピングなし|SQL_C_TYPE_TIMESTAMP (93)|マッピング [1] はありません|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|エラー (DM から)|エラー (DM から)|SQL_C_TIMESTAMP (11)|マッピング [2] がありません|  
  
 [1] この結果として *、odbc 2.x アプリケーションで*odbc 2.x ドライバーを使用する場合は、カタログ関数によって返された結果セットで返された日付、時刻、またはタイムスタンプコードを使用*できます。*  
  
 [2] この結果として *、odbc 3.x アプリケーションで*odbc 3.x ドライバーを使用する場合は、カタログ関数によって返された結果セットで返された日付、時刻、またはタイムスタンプコードを使用*できます。*  
  
 次の表に、ODBC *3. x* Driver Manager が、 **SQLBindParameter**の*ParameterType*引数または**SQLGetTypeInfo**の*DataType*引数に入力された日付、時刻、およびタイムスタンプの SQL データ型のマッピングを実行する方法を示します。  
  
|データ型<br /><br /> 入力されたコード|*2. x* アプリから<br /><br /> *2.x* 2.x ドライバー|*2. x* アプリから<br /><br /> *3.x* 3.x ドライバー|*3. x* アプリから<br /><br /> *2.x* 2.x ドライバー|*3. x* アプリから<br /><br /> *3.x* 3.x ドライバー|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|マッピングなし|SQL_TYPE_DATE (91)|マッピング [1] はありません|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|エラー (DM から)|エラー (DM から)|SQL_DATE (9)|マッピング [2] がありません|  
|SQL_TIME (10)|マッピングなし|SQL_TYPE_TIME (92)|マッピング [1] はありません|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|エラー (DM から)|エラー (DM から)|SQL_TIME (10)|マッピング [2] がありません|  
|SQL_TIMESTAMP (11)|マッピングなし|SQL_TYPE_TIMESTAMP (93)|マッピング [1] はありません|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|エラー (DM から)|エラー (DM から)|SQL_TIMESTAMP (11)|マッピング [2] がありません|  
  
 [1] この結果として *、odbc 2.x アプリケーションで*odbc 2.x ドライバーを使用する場合は、カタログ関数によって返された結果セットで返された日付、時刻、またはタイムスタンプコードを使用*できます。*  
  
 [2] この結果として *、odbc 3.x アプリケーションで*odbc 3.x ドライバーを使用する場合は、カタログ関数によって返された結果セットで返された日付、時刻、またはタイムスタンプコードを使用*できます。*
