---
description: 複数の結果
title: 複数の結果 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc42bfa96c4784d232d8359a15ac74b2f3c5a2be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429254"
---
# <a name="multiple-results"></a>複数の結果
*結果*として、ステートメントの実行後にデータソースから返されるものがあります。 ODBC には、結果セットと行カウントという2種類の結果があります。 *行数は、* update、delete、または insert ステートメントの影響を受ける行の数です。 [SQL ステートメントのバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)で説明されているバッチでは、複数の結果が生成される可能性があります。  
  
 次の表に、アプリケーションで使用される **SQLGetInfo** オプションの一覧を示します。このオプションは、データソースが異なる種類のバッチごとに複数の結果を返すかどうかを判断するために使用されます。 特に、データソースは、バッチ内のステートメントごとに1行のカウント、またはバッチ内のステートメントごとに個別の行数を返すことができます。 パラメーターの配列を使用して結果セット生成ステートメントを実行した場合、データソースは、パラメーターのセットごとに1つの結果セットを返すことができます。  
  
|バッチの種類|行数|結果セット|  
|----------------|----------------|-----------------|  
|明示的なバッチ|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|手順|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|パラメーターの配列|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 行カウント-バッチ内のステートメントの生成はサポートされている可能性がありますが、行カウントはサポートされていません。 **SQLGetInfo**の SQL_BATCH_SUPPORT オプションは、行数を生成するステートメントをバッチで許可するかどうかを示します。SQL_BATCH_ROW_COUNTS オプションは、これらの行カウントがアプリケーションに返されるかどうかを示します。  
  
 [b] 明示的なバッチおよびプロシージャは、複数の結果セット生成ステートメントを含む場合は、常に複数の結果セットを返します。  
  
> [!NOTE]  
>  ODBC 1.0 で導入された SQL_MULT_RESULT_SETS オプションは、複数の結果セットを返すことができるかどうかに関する一般的な情報のみを提供します。 特に、SQL_BATCH_SUPPORT に対して SQL_BS_SELECT_EXPLICIT または SQL_BS_SELECT_PROC ビットが返された場合、または SQL_PARAM_ARRAYS_SELECT に対して SQL_PAS_BATCH が返された場合は、"Y" に設定されます。  
  
 複数の結果を処理するために、アプリケーションは **Sqlmoreresults**を呼び出します。 この関数は、現在の結果を破棄し、次の結果を使用できるようにします。 これ以上結果が得られない場合は SQL_NO_DATA が返されます。 たとえば、次のステートメントがバッチとして実行されたとします。  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 これらのステートメントを実行すると、アプリケーションは **SELECT** ステートメントによって作成された結果セットから行をフェッチします。 行のフェッチが完了すると、 **Sqlmoreresults** を呼び出して、再価格設定された部品の数を使用できるようにします。 必要に応じて、 **Sqlmoreresults** は、フェッチされていない行を破棄し、カーソルを閉じます。 次に、アプリケーションは **SQLRowCount** を呼び出して、 **UPDATE** ステートメントによって再料金されたパーツの数を確認します。  
  
 結果が使用可能になる前にバッチステートメント全体が実行されるかどうかは、ドライバーによって異なります。 実装によっては、次のような場合があります。それ以外では、 **Sqlmoreresults** を呼び出すと、バッチ内の次のステートメントの実行がトリガーされます。  
  
 バッチ内のステートメントのいずれかが失敗した場合、 **Sqlmoreresults** は SQL_ERROR または SQL_SUCCESS_WITH_INFO を返します。 ステートメントが失敗したとき、または失敗したステートメントがバッチの最後のステートメントであったときにバッチが中止された場合、 **Sqlmoreresults** は SQL_ERROR を返します。 ステートメントが失敗し、失敗したステートメントがバッチの最後のステートメントではなかったときにバッチが中止されなかった場合、 **Sqlmoreresults** は SQL_SUCCESS_WITH_INFO を返します。 SQL_SUCCESS_WITH_INFO は、少なくとも1つの結果セットまたはカウントが生成され、バッチが中止されなかったことを示します。
