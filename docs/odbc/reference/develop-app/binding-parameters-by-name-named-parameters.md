---
description: 名前によるパラメーターのバインド (名前付きパラメーター)
title: 名前によるパラメーターのバインド (名前付きパラメーター) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75227b26b5f9f060089e6568e233d327e3f7faa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476844"
---
# <a name="binding-parameters-by-name-named-parameters"></a>名前によるパラメーターのバインド (名前付きパラメーター)
特定の Dbms では、アプリケーションでストアドプロシージャのパラメーターをプロシージャ呼び出しの位置ではなく、名前で指定できます。 このようなパラメーターは、 *名前付きパラメーター*と呼ばれます。 ODBC では、名前付きパラメーターの使用がサポートされています。 ODBC では、名前付きパラメーターはストアドプロシージャの呼び出しでのみ使用され、他の SQL ステートメントでは使用できません。  
  
 ドライバーは、IPD の SQL_DESC_UNNAMED フィールドの値をチェックして、名前付きパラメーターが使用されているかどうかを確認します。 SQL_DESC_UNNAMED が SQL_UNNAMED に設定されていない場合、ドライバーは IPD の SQL_DESC_NAME フィールドの名前を使用してパラメーターを識別します。 パラメーターをバインドするには、アプリケーションで **SQLBindParameter** を呼び出してパラメーター情報を指定し、 **SQLSetDescField** を呼び出して IPD の SQL_DESC_NAME フィールドを設定します。 名前付きパラメーターを使用する場合、プロシージャ呼び出しのパラメーターの順序は重要ではなく、パラメーターのレコード番号は無視されます。  
  
 名前のないパラメーターと名前付きパラメーターの違いは、記述子のレコード番号とプロシージャのパラメーター番号の間の関係にあります。 名前のないパラメーターを使用すると、最初のパラメーターマーカーは、パラメーター記述子の最初のレコードに関連付けられます。これは、プロシージャ呼び出しの最初のパラメーター (作成順) に関連します。 名前付きパラメーターが使用されている場合、最初のパラメーターマーカーはパラメーター記述子の最初のレコードに関連付けられていますが、記述子のレコード番号とプロシージャのパラメーター番号の間のリレーションシップは存在しません。 名前付きパラメーターでは、記述子レコード番号とプロシージャパラメーター位置のマッピングは使用されません。代わりに、記述子レコード名はプロシージャパラメーター名にマップされます。  
  
> [!NOTE]  
>  IPD の自動作成が有効になっている場合は、名前付きパラメーターが使用されていても、記述子レコードの順序がプロシージャ定義内のパラメーターの順序と一致するように、ドライバーによって記述子が設定されます。  
  
 名前付きパラメーターを使用する場合は、すべてのパラメーターが名前付きパラメーターである必要があります。 いずれかのパラメーターが名前付きパラメーターでない場合は、パラメーターとして指定されているパラメーター ca はありません。 名前付きパラメーターと名前のないパラメーターが混在している場合、動作はドライバーに依存します。  
  
 名前付きパラメーターの例として、SQL Server ストアドプロシージャが次のように定義されているとします。  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 この手順では、最初のパラメーターの @title_id 既定値は1です。 アプリケーションでは、次のコードを使用して、動的パラメーターを1つだけ指定するように、このプロシージャを呼び出すことができます。 このパラメーターは、"quote" という名前の名前付きパラメーターです \@ 。  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
