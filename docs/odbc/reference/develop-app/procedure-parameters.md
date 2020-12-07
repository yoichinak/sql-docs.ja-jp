---
description: Procedure Parameters
title: プロシージャのパラメーター |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b21780cc4a6670c76e60daa69cf7933b4182b44e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465724"
---
# <a name="procedure-parameters"></a>Procedure Parameters
プロシージャ呼び出しのパラメーターには、入力、入力、出力、または出力パラメーターを指定できます。 これは、常に入力パラメーターである他のすべての SQL ステートメントのパラメーターとは異なります。  
  
 入力パラメーターは、プロシージャに値を送信するために使用されます。 たとえば、Parts テーブルに PartID、Description、および Price 列があるとします。 InsertPart プロシージャには、テーブル内の各列に対する入力パラメーターが含まれている場合があります。 次に例を示します。  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 ドライバーは、 **SQLExecDirect** または **sqlexecute** が SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_NO_DATA を返すまで、入力バッファーの内容を変更しないようにする必要があります。 **SQLExecDirect**または**sqlexecute**が SQL_NEED_DATA または SQL_STILL_EXECUTING を返したときに、入力バッファーの内容を変更することはできません。  
  
 入力/出力パラメーターは、プロシージャに値を送信し、プロシージャから値を取得するために使用されます。 入力パラメーターと出力パラメーターの両方と同じパラメーターを使用すると、混乱が生じる傾向があるため、避ける必要があります。 たとえば、プロシージャが注文 ID を受け取り、顧客の ID を返すとします。 これは、1つの入力/出力パラメーターを使用して定義できます。  
  
```  
{call GetCustID(?)}  
```  
  
 次の2つのパラメーターを使用することをお勧めします。注文 ID の入力パラメーターと、customer ID の出力パラメーターまたは入力/出力パラメーターです。  
  
```  
{call GetCustID(?, ?)}  
```  
  
 プロシージャの戻り値を取得し、プロシージャの引数から値を取得するには、出力パラメーターを使用します。値を返すプロシージャは、 *関数*とも呼ばれます。 たとえば、前述の **GetCustID** プロシージャが、注文を検索できたかどうかを示す値を返すとします。 次の呼び出しでは、最初のパラメーターはプロシージャの戻り値を取得するために使用する出力パラメーター、2番目のパラメーターは注文 ID を指定するための入力パラメーター、3番目のパラメーターは顧客 ID を取得するための出力パラメーターです。  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 ドライバーは、プロシージャ内の入力パラメーターと入出力パラメーターの値を、他の SQL ステートメントの入力パラメーターとは異なる方法で処理します。 ステートメントを実行すると、これらのパラメーターにバインドされている変数の値が取得され、データソースに送信されます。  
  
 ステートメントが実行されると、ドライバーは、これらのパラメーターにバインドされた変数に入力/出力パラメーターと出力パラメーターの戻り値を格納します。 これらの戻り値は、プロシージャによって返されたすべての結果がフェッチされ、 **Sqlmoreresults** が SQL_NO_DATA を返した後に設定されることは保証されません。 ステートメントを実行した結果、エラーが発生した場合は、入力/出力パラメーターのバッファーまたは出力パラメーターのバッファーの内容が定義されていません。  
  
 アプリケーションは **Sqlprocedure** を呼び出して、プロシージャに戻り値があるかどうかを判断します。 **SQLProcedureColumns**を呼び出して、各プロシージャパラメーターの型 (戻り値、入力、入出力、出力) を決定します。
