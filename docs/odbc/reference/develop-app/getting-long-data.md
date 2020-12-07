---
description: 長い形式のデータの取得
title: 長い形式のデータを取得する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a40bc3f4f65f747776d747d79868340de06f53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429284"
---
# <a name="getting-long-data"></a>長い形式のデータの取得
Dbms では、255文字など、特定のサイズの文字またはバイナリデータとして *長い形式のデータ* を定義します。 このデータは、1つのバッファーに格納するのに十分な大きさになる場合があります。たとえば、複数の1000文字の部分の説明などです。 ただし、長いテキストドキュメントやビットマップなど、メモリに格納するには長すぎる場合があります。 このようなデータは1つのバッファーに格納できないので、行の他のデータがフェッチされた後、 **SQLGetData** を使用してドライバーから取得されます。  
  
> [!NOTE]  
>  アプリケーションは、長いデータだけでなく、 **SQLGetData**を使用してデータのあらゆる種類のデータを取得できますが、部分で取得できるのは文字データとバイナリデータだけです。 ただし、データが1つのバッファーに収まらない場合は、一般に **SQLGetData**を使用する必要はありません。 バッファーを列にバインドし、ドライバーがバッファー内のデータを返すようにする方がはるかに簡単です。  
  
 1つの列から長いデータを取得するには、まず **Sqlfetchscroll** または **sqlfetch** を呼び出して、行に移動し、バインドされた列のデータをフェッチします。 次に、アプリケーションは **SQLGetData**を呼び出します。 **SQLGetData** には、 **SQLBindCol**: ステートメントハンドルと同じ引数があります。列番号。アプリケーション変数の C データ型、アドレス、およびバイト長。および長さ/インジケーターバッファーのアドレス。 これらの関数は基本的に同じタスクを実行するため、同じ引数を持ちます。これらの関数は、どちらもアプリケーション変数をドライバーに記述し、特定の列のデータをその変数で返すように指定します。 主な違いは、行がフェッチされた後 (この理由で*遅延バインディング*と呼ばれることもあります)、 **SQLGetData**によって指定されたバインディングが呼び出しの間だけ継続**することです**。  
  
 1つの列に関しては、 **SQLGetData** は **sqlfetch**のように動作します。これは、列のデータを取得し、それをアプリケーション変数の型に変換して、その変数で返します。 また、長さ/インジケーターバッファー内のデータのバイト長も返されます。 **Sqlfetch**がデータを返す方法の詳細については、「[データ行のフェッチ](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)」を参照してください。  
  
 **SQLGetData** は、1つの重要な点で **sqlfetch** とは異なります。 同じ列に対して2回以上呼び出された場合は、各呼び出しによってデータの連続する部分が返されます。 最後の呼び出しを除く各呼び出しは、SQL_SUCCESS_WITH_INFO と SQLSTATE 01004 (文字列データ、右側が切り捨てられました) を返します。最後の呼び出しでは SQL_SUCCESS が返されます。 **SQLGetData**を使用して、長いデータを部分的に取得する方法を次に示します。 返されるデータがなくなった場合、 **SQLGetData** は SQL_NO_DATA を返します。 アプリケーションは、長いデータをまとめて配置する必要があります。これは、データの一部を連結することを意味します。 各部分は null で終了します。部分を連結する場合は、アプリケーションで null 終了文字を削除する必要があります。 部分的なデータの取得は、可変長のブックマークや、その他の長いデータに対して行うことができます。 長さ/インジケーターバッファーで返される値は、前の呼び出しで返されたバイト数によって、呼び出しごとに減少します。ただし、ドライバーが使用可能なデータの量を検出できず、SQL_NO_TOTAL のバイト長を返すことは一般的ではありません。 次に例を示します。  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 **SQLGetData**の使用にはいくつかの制限があります。 一般に、 **SQLGetData**でアクセスされる列は次のとおりです。  
  
-   (結果セットの列がデータソースから読み取られる方法により) 列番号が増加する順にアクセスする必要があります。 たとえば、列5に対して **SQLGetData** を呼び出し、列4に対して呼び出すと、エラーになります。  
  
-   をバインドできません。  
  
-   最後にバインドされた列よりも大きい列番号を指定する必要があります。 たとえば、最後にバインドされた列が列3の場合、列2に対して **SQLGetData** を呼び出すとエラーになります。 このため、アプリケーションでは、長いデータ列を選択リストの末尾に配置する必要があります。  
  
-   複数の行を取得するために **Sqlfetch** または **sqlfetchscroll** が呼び出された場合は使用できません。 詳細については、「 [ブロックカーソルの使用](../../../odbc/reference/develop-app/using-block-cursors.md)」を参照してください。  
  
 一部のドライバーでは、これらの制限は適用されません。 相互運用可能なアプリケーションでは、それらが存在することを前提としているか、SQL_GETDATA_EXTENSIONS オプションを指定して **SQLGetInfo** を呼び出すことによって適用されない制限を決定する  
  
 アプリケーションが文字またはバイナリデータ列のすべてのデータを必要としない場合は、ステートメントを実行する前に SQL_ATTR_MAX_LENGTH statement 属性を設定することによって、DBMS ベースのドライバーのネットワークトラフィックを減らすことができます。 これにより、任意の文字またはバイナリ列に対して返されるデータのバイト数が制限されます。 たとえば、長いテキストドキュメントが列に含まれているとします。 この列を含むテーブルを参照するアプリケーションでは、各ドキュメントの最初のページのみを表示する必要がある場合があります。 このステートメント属性はドライバーでシミュレートできますが、これを行う理由はありません。 特に、アプリケーションが文字データまたはバイナリデータを切り捨てたい場合は、 **SQLBindCol** を使用して小さなバッファーを列にバインドし、ドライバーがデータを切り捨てられるようにする必要があります。
