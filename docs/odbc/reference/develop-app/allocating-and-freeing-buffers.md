---
description: バッファーの割り当てと解放
title: バッファーの割り当てと解放 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 629c613e8c0aba4675b2b95c9c9ccd82fb7cdfb6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429474"
---
# <a name="allocating-and-freeing-buffers"></a>バッファーの割り当てと解放
すべてのバッファーが割り当てられ、アプリケーションによって解放されます。 バッファーが遅延されていない場合は、関数の呼び出しの間のみ存在する必要があります。 たとえば、 **SQLGetInfo** は、 *infovalueptr* 引数が指すバッファー内の特定のオプションに関連付けられている値を返します。 このバッファーは、次のコード例に示すように、 **SQLGetInfo**の呼び出しの直後に解放できます。  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 遅延バッファーは1つの関数で指定され、別の関数で使用されるため、遅延バッファーを解放するためのアプリケーションプログラミングエラーであり、ドライバーが引き続き存在することを想定しています。 たとえば、 \* **sqlfetch**で後で使用するために、 *valueptr*バッファーのアドレスを**SQLBindCol**に渡します。 このバッファーは、次のコード例に示すように、 **SQLBindCol** や **SQLFreeStmt** を呼び出すなどして、列がバインド解除されるまでは解放できません。  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 このようなエラーは、バッファーを関数内でローカルに宣言することによって簡単に行うことができます。バッファーは、アプリケーションが関数を離れると解放されます。 たとえば、次のコードでは、ドライバーで未定義の致命的な動作が発生します。  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
