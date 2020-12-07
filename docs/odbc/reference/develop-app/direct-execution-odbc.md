---
description: 直接実行 (ODBC)
title: 直接実行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9be03c4f20a82e134481f8fd9bb849ffd830567a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476704"
---
# <a name="direct-execution-odbc"></a>直接実行 (ODBC)
直接実行は、ステートメントを実行する最も簡単な方法です。 ステートメントが実行のために送信されると、データソースはそれをアクセスプランにコンパイルしてから、そのアクセスプランを実行します。  
  
 直接実行は、実行時にステートメントを構築および実行する汎用アプリケーションによって一般的に使用されます。 たとえば、次のコードでは、SQL ステートメントをビルドし、1回だけ実行します。  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接実行は、1回だけ実行されるステートメントに最適です。 主な欠点は、SQL ステートメントが実行されるたびに解析されることです。 また、ステートメント (存在する場合) によって作成された結果セットに関する情報を、ステートメントが実行されるまで取得することはできません。これは、2つの異なる手順でステートメントを準備して実行した場合に発生する可能性があります。  
  
 ステートメントを直接実行するために、アプリケーションは次のアクションを実行します。  
  
1.  任意のパラメーターの値を設定します。 詳細については、このセクションで後述する「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
2.  **SQLExecDirect**を呼び出し、SQL ステートメントを含む文字列を渡します。  
  
3.  **SQLExecDirect**が呼び出されると、ドライバーは次のようになります。  
  
    -   ステートメントを解析せずに、データソースの SQL 文法を使用するように SQL ステートメントを変更します。これには、「 [ODBC でのエスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」で説明されているエスケープシーケンスの置換が含まれます。 アプリケーションでは、 **Sqlnativesql**を呼び出すことにより、変更された SQL ステートメントの形式を取得できます。 SQL_ATTR_NOSCAN statement 属性が設定されている場合、エスケープシーケンスは置き換えられません。  
  
    -   現在のパラメーター値を取得し、必要に応じて変換します。 詳細については、このセクションで後述する「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
    -   ステートメントと変換されたパラメーター値をデータソースに送信して実行します。  
  
    -   エラーを返します。 これには、SQLSTATE 24000 (無効なカーソル状態)、sqlstate 42000 (構文エラーまたはアクセス違反) などの構文エラー、SQLSTATE 42 S02 (ベーステーブルまたはビューが見つからない) などのセマンティックエラーなどのシーケンスまたは状態診断が含まれます。
