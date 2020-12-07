---
description: SQLSetPos による行セットの行の更新
title: SQLSetPos | を使用した行セットの行の更新Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d1b1b50007a03ee1973d92acafbe8f2be1022f52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471217"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos による行セットの行の更新
**SQLSetPos**の更新操作により、データソースは、バインドされた各列のアプリケーションバッファーのデータを使用して、テーブルの1つまたは複数の選択した行を更新します (長さ/インジケーターバッファーの値が SQL_COLUMN_IGNORE 場合を除きます)。 バインドされていない列は更新されません。  
  
 **SQLSetPos**を使用して行を更新する場合、アプリケーションは次のことを行います。  
  
1.  新しいデータ値を行セットバッファーに配置します。 **SQLSetPos**を使用して長いデータを送信する方法の詳細については、「 [Long data And Sqlsetpos And sqlbulkoperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)」を参照してください。  
  
2.  各列の長さ/インジケーターバッファーの値を必要に応じて設定します。 これは、文字列バッファーにバインドされている列のデータまたは SQL_NTS のバイト長、バイナリバッファーにバインドされた列のデータのバイト長、および NULL に設定する列の SQL_NULL_DATA です。  
  
3.  SQL_COLUMN_IGNORE に更新されない列の長さ/インジケーターバッファーの値を設定します。 アプリケーションでこの手順をスキップして既存のデータを再送信することはできますが、これは非効率的であり、読み取り時に切り捨てられたデータソースに値を送信するリスクです。  
  
4.  *操作*を SQL_UPDATE に設定し、 *RowNumber*を、更新する行の番号に設定して、 **SQLSetPos**を呼び出します。 *RowNumber*が0の場合、行セット内のすべての行が更新されます。  
  
 **SQLSetPos**が返された後、現在の行は更新された行に設定されます。  
  
 行セットのすべての行を更新するとき (*RowNumber* は 0)、アプリケーションでは、行操作配列の対応する要素 (SQL_ATTR_ROW_OPERATION_PTR statement 属性が指す) を SQL_ROW_IGNORE に設定することにより、特定の行の更新を無効にすることができます。 行の操作の配列は、行の状態の配列に対する要素のサイズと数に対応しています (SQL_ATTR_ROW_STATUS_PTR statement 属性によって示されています)。 正常にフェッチされ、行セットから削除されていない結果セット内の行のみを更新するには、行の操作の配列として行セットをフェッチした関数の行の状態の配列を **SQLSetPos**に使用します。  
  
 更新プログラムとしてデータソースに送信されるすべての行について、アプリケーションバッファーに有効な行データが含まれている必要があります。 フェッチによってアプリケーションバッファーがいっぱいになっていて、行の状態配列が保持されている場合は、行の各位置の値を SQL_ROW_DELETED、SQL_ROW_ERROR、または SQL_ROW_NOROW にすることはできません。  
  
 たとえば、次のコードを使用すると、ユーザーは Customers テーブルをスクロールして、新しい行を更新、削除、または追加することができます。 このメソッドは、 **SQLSetPos** を呼び出して新しい行を更新または追加する前に、新しいデータを行セットバッファーに配置します。 行セットバッファーの末尾に余分な行が割り当てられ、新しい行が保持されます。これにより、新しい行のデータがバッファーに配置されても、既存のデータが上書きされるのを防ぐことができます。  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
