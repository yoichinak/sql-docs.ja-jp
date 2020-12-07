---
description: 長い形式のデータ、SQLSetPos および SQLBulkOperations
title: Long Data、SQLSetPos、および SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12bc0299df58bf85272445773a8f33a872c39ef2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429274"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>長い形式のデータ、SQLSetPos および SQLBulkOperations
SQL ステートメントのパラメーターの場合と同様に、 **sqlbulkoperations** または **SQLSetPos** を使用して行を更新するとき、または **sqlbulkoperations**を使用して行を挿入するときに、長いデータを送信できます。 データは、複数の **Sqlputdata**呼び出しを使用して部分的に送信されます。 実行時にデータが送信される列は、 *実行時データ列*と呼ばれます。  
  
> [!NOTE]  
>  アプリケーションでは、実行時に **Sqlputdata**を使用して任意の種類のデータを送信できます。ただし、部分的に送信できるのは、文字とバイナリデータのみです。 ただし、データが1つのバッファーに収まらない場合は、通常、 **Sqlputdata**を使用する必要はありません。 バッファーをバインドして、ドライバーがバッファーからデータを取得できるようにする方がはるかに簡単です。  
  
 通常、長いデータ列はバインドされていないため、 **sqlbulkoperations** または **sqlsetpos** を呼び出す前に列をバインドし、 **sqlbulkoperations** または **sqlsetpos**を呼び出した後にバインドを解除する必要があります。 列をバインドする必要があります。 **Sqlbulkoperations** または **SQLSetPos** はバインドされた列でのみ動作するため、 **SQLGetData** を使用して列からデータを取得できるように、バインドを解除する必要があります。  
  
 実行時にデータを送信するために、アプリケーションは次の処理を実行します。  
  
1.  データ値の代わりに、行セットバッファーに32ビット値を配置します。 この値は後でアプリケーションに返されるため、アプリケーションでは、列の番号やデータを含むファイルのハンドルなどの意味のある値に設定する必要があります。  
  
2.  長さ/インジケーターバッファーの値を SQL_LEN_DATA_AT_EXEC (*長さ*) マクロの結果に設定します。 この値は、パラメーターのデータが **Sqlputdata**と共に送信されることをドライバーに示します。 *長さ*の値は、データソースに長いデータを送信するときに使用されます。これにより、大量のデータが送信されて、領域を事前に割り当てることができるようになります。 データソースにこの値が必要かどうかを判断するために、アプリケーションは SQL_NEED_LONG_DATA_LEN オプションを指定して **SQLGetInfo** を呼び出します。 すべてのドライバーがこのマクロをサポートしている必要があります。データソースがバイト長を必要としない場合、ドライバーはそのバイトを無視できます。  
  
3.  **Sqlbulkoperations**または**SQLSetPos**を呼び出します。 ドライバーは、長さ/インジケーターバッファーに SQL_LEN_DATA_AT_EXEC (*長さ*) マクロの結果が含まれていることを検出し、関数の戻り値として SQL_NEED_DATA を返します。  
  
4.  SQL_NEED_DATA 戻り値に応答して **Sqlparamdata** を呼び出します。 長いデータを送信する必要がある場合、 **Sqlparamdata** は SQL_NEED_DATA を返します。 *Valueptrptr*引数が指すバッファーでは、ドライバーは、アプリケーションが行セットバッファーに配置した一意の値を返します。 実行時データ列が複数ある場合、アプリケーションはこの値を使用して、データを送信する列を決定します。ドライバーは、特定の順序で実行時データ列のデータを要求する必要はありません。  
  
5.  **Sqlputdata**を呼び出して、列データをドライバーに送信します。 列のデータが1つのバッファーに格納されていない場合 (長いデータの場合など)、アプリケーションは **Sqlputdata** を繰り返し呼び出して、データを部分的に送信します。データを再アセンブルするには、ドライバーとデータソースが必要です。 アプリケーションが null で終わる文字列データを渡す場合、ドライバーまたはデータソースは、再構築プロセスの一環として、null 終端文字を削除する必要があります。  
  
6.  **Sqlparamdata**を再度呼び出して、列のすべてのデータが送信されたことを示します。 データが送信されていない実行時データ列がある場合、ドライバーは、次の実行時データ列に対して SQL_NEED_DATA と一意の値を返します。アプリケーションが手順5に戻ります。 実行時データのすべての列についてデータが送信されている場合は、その行のデータがデータソースに送信されます。 **Sqlparamdata** は SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返し、 **sqlparamdata** または **SQLSetPos** が返す可能性のある SQLSTATE を返すことができます。  
  
 **Sqlbulkoperations**または**SQLSetPos**によって SQL_NEED_DATA が返された後、最後の実行時データ列に対してデータが完全に送信される前に、ステートメントはデータの状態が必要になります。 この状態では、アプリケーションは **Sqlputdata**、 **sqlputdata**、 **SQLCancel**、 **SQLGetDiagField**、または **SQLGetDiagRec**のみを呼び出すことができます。他のすべての関数は、SQLSTATE HY010 (関数シーケンスエラー) を返します。 **SQLCancel**を呼び出すと、ステートメントの実行が取り消され、以前の状態に戻ります。 詳細については、「 [付録 B: ODBC 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」を参照してください。
