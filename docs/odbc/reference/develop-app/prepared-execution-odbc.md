---
description: 準備実行 ODBC
title: 実行を準備した ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6141af2cde7106419ab1eb68f86d5817f055aab2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465744"
---
# <a name="prepared-execution-odbc"></a>準備実行 ODBC
準備実行は、ステートメントを複数回実行する効率的な方法です。 ステートメントは、最初にアクセスプランにコンパイルされるか、 *準備* されます。 その後、アクセスプランが1回以上実行されます。 アクセスプランの詳細については、「 [SQL ステートメントの処理](../../../odbc/reference/processing-a-sql-statement.md)」を参照してください。  
  
 準備実行は、通常、垂直およびカスタムアプリケーションで、同じパラメーター化された SQL ステートメントを繰り返し実行するために使用されます。 たとえば、次のコードでは、さまざまなパーツの価格を更新するステートメントを準備しています。 次に、毎回異なるパラメーター値を使用してステートメントを複数回実行します。  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 準備された実行は、ステートメントが1回だけコンパイルされることが多いため、ステートメントを複数回実行するよりも直接実行するよりも高速です。直接実行されるステートメントは、実行されるたびにコンパイルされます。 準備実行では、データソースがアクセスプラン識別子をサポートしている場合、SQL ステートメント全体ではなく、ステートメントが実行されるたびにドライバーがデータソースにアクセスプラン識別子を送信できるため、ネットワークトラフィックを削減することもできます。  
  
 アプリケーションでは、ステートメントが準備されてから実行されるまでの間に、結果セットのメタデータを取得できます。 ただし、準備された unexecuted ステートメントのメタデータを返すことは、ドライバーによっては高価であり、可能であれば、相互運用可能なアプリケーションによって回避する必要があります。 詳細については、「 [結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)」を参照してください。  
  
 準備実行は、1 回しか実行されないステートメントには使用しないでください。 このようなステートメントでは、追加の ODBC 関数呼び出しが必要になるため、直接実行よりも少し遅くなります。  
  
> [!IMPORTANT]  
>  **SQLEndTran**を明示的に呼び出すか、自動コミットモードで作業することにより、トランザクションをコミットまたはロールバックすると、一部のデータソースによって、接続上のすべてのステートメントのアクセスプランが削除されます。 詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明」の SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR のオプションを参照してください。  
  
 ステートメントを準備して実行するために、アプリケーションは次のようになります。  
  
1.  **SQLPrepare**を呼び出し、SQL ステートメントを含む文字列を渡します。  
  
2.  任意のパラメーターの値を設定します。 パラメーターは、ステートメントを準備する前または後に実際に設定できます。 詳細については、このセクションで後述する「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
3.  **Sqlexecute**を呼び出し、データのフェッチなど、必要な追加の処理を実行します。  
  
4.  必要に応じて、手順 2. と 3. を繰り返します。  
  
5.  **SQLPrepare**が呼び出されると、ドライバーは次のようになります。  
  
    -   ステートメントを解析せずに、データソースの SQL 文法を使用するように SQL ステートメントを変更します。 これには、「 [ODBC でのエスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」で説明されているエスケープシーケンスの置換が含まれます。 アプリケーションでは、 **Sqlnativesql**を呼び出すことにより、変更された SQL ステートメントの形式を取得できます。 SQL_ATTR_NOSCAN statement 属性が設定されている場合、エスケープシーケンスは置き換えられません。  
  
    -   準備のためにステートメントをデータソースに送信します。  
  
    -   後で実行するために返されるアクセスプラン識別子を格納します (準備が正常に完了した場合)。または、準備が失敗した場合はエラーを返します。 エラーには、SQLSTATE 42000 (構文エラーまたはアクセス違反) や、SQLSTATE 42 S02 (ベーステーブルまたはビューが見つかりません) などのセマンティックエラーなどの構文エラーが含まれます。  
  
        > [!NOTE]  
        >  一部のドライバーは、この時点ではエラーを返しませんが、ステートメントが実行されたとき、またはカタログ関数が呼び出されたときに返されます。 したがって、 **SQLPrepare** は、実際には失敗したときに成功したように見えることがあります。  
  
6.  **Sqlexecute**が呼び出されると、ドライバーは次のようになります。  
  
    -   現在のパラメーター値を取得し、必要に応じて変換します。 詳細については、このセクションで後述する「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
    -   アクセスプラン識別子と変換されたパラメーター値をデータソースに送信します。  
  
    -   エラーを返します。 これらは通常、SQLSTATE 24000 (無効なカーソル状態) などの実行時エラーです。 ただし、一部のドライバーでは、この時点で構文エラーとセマンティックエラーが返されます。  
  
 データソースがステートメントの準備をサポートしていない場合、ドライバーは、可能な限りこのデータソースをエミュレートする必要があります。 たとえば、ドライバーは **SQLPrepare** が呼び出されたときに何も実行せず、 **sqlexecute** が呼び出されたときにステートメントを直接実行します。  
  
 データソースで実行されない構文チェックがサポートされている場合、ドライバーは、 **Sqlexecute**が呼び出されたときに**SQLPrepare**が呼び出されたかどうかを確認するためのステートメントを送信し、ステートメントを送信することがあります。  
  
 ドライバーがステートメントの準備をエミュレートできない場合、 **SQLPrepare** が呼び出されたときにステートメントが格納され、 **sqlexecute** が呼び出されたときに実行のために送信されます。  
  
 エミュレートされたステートメントの準備は完全ではないため、 **Sqlexecute** は **SQLPrepare**によって通常返されるエラーを返すことができます。
