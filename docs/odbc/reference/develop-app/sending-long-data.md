---
description: 長い形式のデータの送信
title: 長いデータを送信する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6a0ec1a7e8dc703d3e7a3ed5332d20e6539eafe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476464"
---
# <a name="sending-long-data"></a>長い形式のデータの送信
Dbms では、254文字など、特定のサイズの文字またはバイナリデータとして *長い形式のデータ* を定義します。 長いテキストドキュメントやビットマップを表す場合など、長いデータのアイテム全体をメモリに格納することはできません。 このようなデータを1つのバッファーに格納することはできないため、データソースは、ステートメントが実行されたときに **Sqlputdata** を使用して部分的にドライバーに送信します。 実行時にデータを送信するパラメーターは、 *実行時データパラメーター*と呼ばれます。  
  
> [!NOTE]  
>  アプリケーションでは、実行時に **Sqlputdata**を使用して任意の種類のデータを送信できます。ただし、部分的に送信できるのは文字データとバイナリデータだけです。 ただし、データが1つのバッファーに収まらない場合は、通常、 **Sqlputdata**を使用する必要はありません。 バッファーをバインドして、ドライバーがバッファーからデータを取得できるようにする方がはるかに簡単です。  
  
 実行時にデータを送信するために、アプリケーションは次の操作を実行します。  
  
1.  バッファーのアドレスを渡すのではなく、 **SQLBindParameter**の*parametervalueptr*引数のパラメーターを識別する32ビットの値を渡します。 この値はドライバーによって分析されません。 これは後でアプリケーションに返されるため、アプリケーションに対して何かを意味します。 たとえば、パラメーターの番号、またはデータを格納しているファイルのハンドルなどです。  
  
2.  **SQLBindParameter**の*StrLen_or_IndPtr*引数に長さ/インジケーターバッファーのアドレスを渡します。  
  
3.  SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC (*長さ*) マクロの結果を長さ/インジケーターバッファーに格納します。 これらの値はどちらも、パラメーターのデータが **Sqlputdata**と共に送信されることをドライバーに示します。 SQL_LEN_DATA_AT_EXEC (*長さ*) は、データソースに長いデータを送信するときに使用されます。これにより、大量のデータが送信されて、領域を事前に割り当てることができるようになります。 データソースにこの値が必要かどうかを判断するために、アプリケーションは SQL_NEED_LONG_DATA_LEN オプションを指定して **SQLGetInfo** を呼び出します。 すべてのドライバーがこのマクロをサポートしている必要があります。データソースがバイト長を必要としない場合、ドライバーはそのバイトを無視できます。  
  
4.  **Sqlexecute**または**SQLExecDirect**を呼び出します。 ドライバーは、長さ/インジケーターバッファーに SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC (*長さ*) マクロの結果が含まれていることを検出し、関数の戻り値として SQL_NEED_DATA を返します。  
  
5.  SQL_NEED_DATA 戻り値に応答して **Sqlparamdata** を呼び出します。 長いデータを送信する必要がある場合、 **Sqlparamdata** は SQL_NEED_DATA を返します。 *Valueptrptr*引数が指すバッファーでは、ドライバーは実行時データパラメーターを識別する値を返します。 実行時データパラメーターが複数ある場合、アプリケーションはこの値を使用して、データを送信するパラメーターを決定する必要があります。ドライバーは、特定の順序で実行時データパラメーターのデータを要求する必要はありません。  
  
6.  **Sqlputdata**を呼び出して、パラメーターデータをドライバーに送信します。 パラメーターデータが1つのバッファーに格納されていない場合 (長いデータの場合など)、アプリケーションは **Sqlputdata** を繰り返し呼び出して、データを部分的に送信します。データを再アセンブルするには、ドライバーとデータソースが必要です。 アプリケーションが null で終わる文字列データを渡す場合、ドライバーまたはデータソースは、再構築プロセスの一環として、null 終端文字を削除する必要があります。  
  
7.  **Sqlparamdata**を再度呼び出して、パラメーターのすべてのデータが送信されたことを示します。 データが送信されていない実行時データパラメーターがある場合、ドライバーは SQL_NEED_DATA と、次のパラメーターを識別する値を返します。アプリケーションが手順6に戻ります。 実行時データのすべてのパラメーターについてデータが送信されている場合は、ステートメントが実行されます。 **Sqlparamdata** は SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返し、 **Sqlexecute** または **SQLExecDirect** が返すことができる戻り値または診断を返すことができます。  
  
 **Sqlexecute**または**SQLExecDirect**が SQL_NEED_DATA を返した後、最後の実行時データパラメーターに対してデータが完全に送信される前に、ステートメントはデータの状態が必要です。 ステートメントが必要なデータ状態にある間、アプリケーションは **Sqlputdata**、 **sqlputdata**、 **SQLCancel**、 **SQLGetDiagField**、または **SQLGetDiagRec**を呼び出すことができます。他のすべての関数は、SQLSTATE HY010 (関数シーケンスエラー) を返します。 **SQLCancel**を呼び出すと、ステートメントの実行が取り消され、以前の状態に戻ります。 詳細については、「 [付録 B: ODBC 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」を参照してください。  
  
 実行時にデータを送信する例については、「 [Sqlputdata](../../../odbc/reference/syntax/sqlputdata-function.md) 関数の説明」を参照してください。
