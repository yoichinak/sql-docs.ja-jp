---
description: プロシージャ呼び出し
title: プロシージャ呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed5da9bbe94bf1f508e1b94c17e81c7b0169f6e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465734"
---
# <a name="procedure-calls"></a>プロシージャ呼び出し
*プロシージャ*は、データソースに格納されている実行可能オブジェクトです。 これは通常、プリコンパイルされた 1 つ以上の SQL ステートメントです。 プロシージャを呼び出すためのエスケープシーケンスはです。  
  
 **{**[**? =**]**呼び出し***プロシージャ名*[**(**[*parameter*] [**,**[*parameter*]]...**)**]**}**  
  
 プロシージャ *名* はプロシージャ名を指定し、 *パラメーター* にはプロシージャパラメーターを指定します。  
  
 プロシージャ呼び出しのエスケープシーケンスの詳細については、「付録 C: SQL 文法」の「 [プロシージャ呼び出しのエスケープシーケンス](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) 」を参照してください。  
  
 プロシージャには、0 個以上のパラメーターを指定できます。 また、構文の先頭にある省略可能なパラメーターマーカー **? =** によって示されているように、値を返すこともできます。 *パラメーター*が入力または入力/出力パラメーターの場合は、リテラルまたはパラメーターマーカーを指定できます。 ただし、データソースによってはリテラルパラメーター値が受け付けられないため、相互運用可能なアプリケーションでは常にパラメーターマーカーを使用する必要があります。 *パラメーター*が出力パラメーターの場合は、パラメーターマーカーである必要があります。 プロシージャ呼び出しステートメントを実行する前に、パラメーターマーカーを **SQLBindParameter** にバインドする必要があります。  
  
 プロシージャ呼び出しでは、入力パラメーターと入出力パラメーターを省略できます。 プロシージャがかっこで呼び出され、{call *procedure-name*()} などのパラメーターが指定されていない場合、ドライバーは、最初のパラメーターに既定値を使用するようにデータソースに指示します。 プロシージャにパラメーターがない場合は、プロシージャが失敗する可能性があります。 {Call *procedure-name*} などのかっこを使用せずにプロシージャを呼び出すと、ドライバーはパラメーター値を送信しません。  
  
 プロシージャ呼び出しでは、入力パラメーターや入出力パラメーターとしてリテラルを指定できます。 たとえば、 **Insertorder** プロシージャに5つの入力パラメーターがあるとします。 次の **Insertorder** への呼び出しでは、最初のパラメーターを省略し、2番目のパラメーターにリテラルを指定し、3番目、4番目、および5番目のパラメーターにパラメーターマーカーを使用します。  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 パラメーターを省略した場合でも、他のパラメーターとの間でコンマを区切る必要があることに注意してください。 入力パラメーターまたは入出力パラメーターを省略すると、プロシージャはそのパラメーターの既定値を使用します。 入力パラメーターまたは入出力パラメーターの既定値を指定するもう1つの方法は、パラメーターにバインドされている長さ/インジケーターバッファーの値を SQL_DEFAULT_PARAM に設定することです。  
  
 入力/出力パラメーターが省略されている場合、またはパラメーターにリテラルが指定されている場合、ドライバーは出力値を破棄します。 同様に、プロシージャの戻り値のパラメーター マーカーを省略した場合、ドライバーは戻り値を破棄します。 最後に、値を返さないプロシージャに戻り値パラメーターを指定すると、ドライバーは、そのパラメーターにバインドされる長さ/インジケーター バッファーの値を SQL_NULL_DATA に設定します。  
  
 たとえば、特定の部品番号を含む注文の一覧を含む結果セットを作成する PARTS_IN_ORDERS プロシージャがあるとします。 次のコードは、パート番号544に対してこのプロシージャを呼び出します。  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 データソースがプロシージャをサポートしているかどうかを判断するために、アプリケーションは SQL_PROCEDURES オプションを指定して **SQLGetInfo** を呼び出します。  
  
 プロシージャの詳細については、「 [プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)」を参照してください。
