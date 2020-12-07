---
description: 埋め込み SQL の例
title: Embedded SQL の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fec0f3e3776b8ac70e85042c565343b35f8a893e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429064"
---
# <a name="embedded-sql-example"></a>埋め込み SQL の例
次のコードは、C で記述された単純な embedded SQL プログラムです。このプログラムは、埋め込まれている SQL 手法の多くを示していますが、すべてではありません。 このプログラムは、注文番号の入力をユーザーに求め、顧客番号、販売員、および注文の状態を取得し、取得した情報を画面に表示します。  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 このプログラムについて、次の点に注意してください。  
  
-   **ホスト変数** ホスト変数は、 **BEGIN declare** セクションと **END declare section** キーワードで囲まれたセクションで宣言されます。 各ホスト変数名の先頭にはコロン (:) が付きます。埋め込み SQL ステートメントに含まれている場合。 コロンを使用すると、コンパイラは、同じ名前を持つホスト変数とデータベースオブジェクト (テーブルや列など) を区別できます。  
  
-   **データ型** DBMS とホスト言語でサポートされているデータ型は、大きく異なる場合があります。 これは、2つの役割を果たすため、ホスト変数に影響します。 一方、ホスト変数は、ホスト言語ステートメントによって宣言および操作されるプログラム変数です。 一方、これらは、埋め込み SQL ステートメントでデータベースデータを取得するために使用されます。 DBMS データ型に対応するホスト言語の種類がない場合、DBMS はデータを自動的に変換します。 ただし、各 DBMS には変換処理に関連する独自のルールと特異性があるため、ホスト変数の種類を慎重に選択する必要があります。  
  
-   **エラー処理** DBMS は、SQL 通信領域 (SQLCA) を使用して、アプリケーションプログラムにランタイムエラーを報告します。 前のコード例では、最初の embedded SQL ステートメントには、SQLCA が含まれています。 これは、プログラムに SQLCA 構造を含めるようにプリコンパイラに指示します。 これは、プログラムが DBMS によって返されたエラーを処理するたびに必要です。 常に...GOTO ステートメントは、エラーが発生したときに特定のラベルに分岐するエラー処理コードを生成するように、プリコンパイラに指示します。  
  
-   **シングルトンの選択** データを返すために使用されるステートメントは、単一の SELECT ステートメントです。つまり、1行のデータのみが返されます。 このコード例では、カーソルを宣言したり、使用したりしません。
