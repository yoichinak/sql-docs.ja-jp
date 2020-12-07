---
description: ステートメントのバッチ
title: ステートメントのバッチ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9d0842a0cc4c38c25af9dc3bdf334f846993f480
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867304"
---
# <a name="batches-of-statements"></a>ステートメントのバッチ
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ステートメントのバッチには [!INCLUDE[tsql](../../../includes/tsql-md.md)] 、2つ以上のステートメントが含まれています。セミコロン (;) は、 **SQLExecDirect** または [SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)に渡される1つの文字列に組み込まれています。 次に例を示します。  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 バッチでは、通常、ネットワーク トラフィックが削減されるので、複数のステートメントを個別に送信するよりも効率的になる可能性があります。 現在の結果セットが完成したときに、次の結果セットに配置するには、 [Sqlmoreresults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) を使用します。  
  
 行セットのサイズが 1 になっている、順方向専用かつ読み取り専用のカーソルの既定値に ODBC カーソル属性が設定されている場合は、常にバッチを使用できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対してサーバー カーソルを使用しているときにバッチを実行すると、サーバー カーソルが暗黙的に既定の結果セットに変換されます。 **SQLExecDirect** または **sqlexecute** は SQL_SUCCESS_WITH_INFO を返し、 **SQLGetDiagRec** を呼び出すと次のように返されます。  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>参照  
 [ODBC&#41;&#40;のステートメントの実行 ](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
