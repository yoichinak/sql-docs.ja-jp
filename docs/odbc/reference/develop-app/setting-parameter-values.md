---
description: パラメーターの値の設定
title: パラメーター値の設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af2992ea66601ec0ae4804e327863e6abb285d73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476424"
---
# <a name="setting-parameter-values"></a>パラメーターの値の設定
パラメーターの値を設定するために、アプリケーションは単にパラメーターにバインドされた変数の値を設定します。 この値が設定されている場合は、ステートメントが実行される前に設定されている必要があります。 アプリケーションでは、変数をバインドする前または後に値を設定できます。また、値は必要に応じて何度でも変更できます。 ステートメントが実行されると、ドライバーは単に変数の現在の値を取得します。 これは、準備されたステートメントを複数回実行する場合に特に便利です。アプリケーションでは、ステートメントが実行されるたびに、一部またはすべての変数の新しい値が設定されます。 この例については、このセクションの前半の「 [準備実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)」を参照してください。  
  
 長さ/インジケーターバッファーが **SQLBindParameter**の呼び出しでバインドされている場合は、ステートメントを実行する前に、次のいずれかの値に設定する必要があります。  
  
-   バインドされた変数内のデータのバイト長。 ドライバーは、変数が文字またはバイナリ (*ValueType* が SQL_C_CHAR または SQL_C_BINARY) の場合にのみ、この長さをチェックします。  
  
-   SQL_NTS。 データは、null で終わる文字列です。  
  
-   SQL_NULL_DATA。 データ値が NULL の場合、ドライバーはバインドされた変数の値を無視します。  
  
-   SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果。 パラメーターの値は、 **Sqlputdata**と共に送信されます。 詳細については、このセクションで後述する「 [長いデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)」を参照してください。  
  
 次の表は、バインドされた変数の値と、アプリケーションがさまざまなパラメーター値に対して設定する長さ/インジケーターバッファーを示しています。  
  
|パラメーター<br /><br /> value|パラメーター<br /><br /> SERVER<br /><br /> データ型 (data type)|変数 (C)<br /><br /> データ型 (data type)| の値<br /><br /> バインディング<br /><br /> 変数| の値<br /><br /> 長さ/インジケーター<br /><br /> バッファー [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS または3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS または2|  
|午後1時|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13、0、0 [b]|--|  
|午後1時|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13:00:00 '} \ 0 [a], [c]|SQL_NTS または14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\ 0" は、null 終了文字を表します。 Null 終了文字は、長さ/インジケーターバッファーの値が SQL_NTS 場合にのみ必要です。  
  
 [b] この一覧の数値は、TIME_STRUCT 構造体のフィールドに格納されている数値です。  
  
 [c] 文字列は、ODBC の date エスケープ句を使用します。 詳細については、「 [日付、時刻、およびタイムスタンプリテラル](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)」を参照してください。  
  
 [d] ドライバーは、SQL_NULL_DATA などの特別な値であるかどうかを確認するために、常にこの値を確認する必要があります。  
  
 ドライバーが実行時にパラメーター値を使用する場合、ドライバーに依存します。 必要に応じて、ドライバーは、バインドされた変数の C データ型とバイト長の値を、パラメーターの SQL データ型、有効桁数、および小数点以下桁数に変換します。 ほとんどの場合、ドライバーはデータソースに値を送信します。 場合によっては、データソースにステートメントを送信する前に、値がテキストとして書式設定され、SQL ステートメントに挿入されます。
