---
description: 実行時に構築された SQL ステートメント
title: 実行時に構築された SQL ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff9f7a4e579ce4e1d1177b8f5fa67f7d13a4fdc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424554"
---
# <a name="sql-statements-constructed-at-run-time"></a>実行時に構築された SQL ステートメント
アドホック分析を実行するアプリケーションは、通常、実行時に SQL ステートメントを作成します。 たとえば、スプレッドシートでは、ユーザーがデータを取得する列を選択できます。  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 実行時に SQL ステートメントを構築するアプリケーションのもう1つのクラスは、アプリケーション開発環境です。 ただし、作成するステートメントは、ビルドするアプリケーションでハードコーディングされており、通常は最適化とテストが可能です。  
  
 実行時に SQL ステートメントを作成するアプリケーションでは、ユーザーに対して非常に柔軟に対応できます。 前の例からわかるように、 **WHERE** 句、 **ORDER BY** 句、または join などの一般的な操作をサポートしていなかったため、実行時に SQL ステートメントを作成することは、ハードコーディングステートメントよりも大幅に複雑になります。 また、このようなアプリケーションのテストは、任意の数の SQL ステートメントを作成できるため、問題になります。  
  
 実行時に SQL ステートメントを構築する場合の潜在的な欠点は、ハードコーディングされたステートメントを使用するよりもステートメントの作成に時間がかかることです。 幸いなことに、これはほとんど心配ありません。 このようなアプリケーションはユーザーインターフェイスを集中的に使用する傾向があり、アプリケーションが SQL ステートメントの構築に費やす時間は通常、ユーザーが条件を入力する時間と比較して小さくなります。
