---
description: パラメーターのバインド (ODBC)
title: パラメーターのバインド ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9893d6611ad2bfc7107df1cd2d4ffe72dbf32fad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499955"
---
# <a name="binding-parameters-odbc"></a>パラメーターのバインド (ODBC)
SQL ステートメントの各パラメーターは、ステートメントが実行される前に、アプリケーションの変数に関連付けられているか、 *バインド* されている必要があります。 アプリケーションは、変数をパラメーターにバインドするときに、その変数アドレス、C データ型などをドライバーに記述します。 また、パラメーター自体 (SQL データ型、有効桁数など) についても説明します。 ドライバーは、この情報をそのステートメント用に保持する構造体に格納し、その情報を使用して、ステートメントの実行時に変数から値を取得します。  
  
 パラメーターは、ステートメントを実行する前にいつでもバインドまたは再バインドできます。 ステートメントの実行後にパラメーターを再バインドする場合、ステートメントが再度実行されるまで、バインドは適用されません。 パラメーターを別の変数にバインドするには、アプリケーションが新しい変数でパラメーターを再バインドするだけです。前のバインドは自動的に解放されます。  
  
 変数は、SQL_RESET_PARAMS オプションを使用して **SQLFreeStmt** を呼び出すことによって、またはステートメントが解放されるまで、すべてのパラメーターがバインド解除されるまで、パラメーターにバインドされたままになります。 このため、アプリケーションは、バインドが解除されるまで変数が解放されないようにする必要があります。 詳細については、「 [バッファーの割り当てと解放](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)」を参照してください。  
  
 パラメーターのバインドは、ステートメントのドライバーによって保持されている構造に格納されている情報にすぎないため、任意の順序で設定できます。 また、実行される SQL ステートメントにも依存しません。 たとえば、アプリケーションが3つのパラメーターをバインドし、次の SQL ステートメントを実行するとします。  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 アプリケーションが SQL ステートメントを直ちに実行する場合  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 同じステートメントハンドルでは、 **INSERT** ステートメントのパラメーターバインドが使用されます。これは、ステートメント構造に格納されているバインドであるためです。 ほとんどの場合、これは不適切なプログラミング手法であり、回避する必要があります。 代わりに、アプリケーションは、SQL_RESET_PARAMS オプションを指定して **SQLFreeStmt** を呼び出し、古いパラメーターをすべてバインド解除してから、新しいパラメーターをバインドする必要があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [バインディング パラメーター マーカー](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [名前によるパラメーターのバインド (名前付きパラメーター)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [パラメーター バインディングのオフセット](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [パラメーターの記述](../../../odbc/reference/develop-app/describing-parameters.md)
