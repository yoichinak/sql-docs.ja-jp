---
description: データ バッファーのアドレス
title: データバッファーアドレス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 301202933ae9cb0206100b6bbf10dda305495be1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429384"
---
# <a name="data-buffer-address"></a>データ バッファーのアドレス
アプリケーションは、データバッファーのアドレスを引数の中でドライバーに渡します。多くの場合、 *Valueptr* または類似した名前という名前が付けられます。 たとえば、次の **SQLBindCol**への呼び出しでは、アプリケーションは *Date* 変数のアドレスを指定します。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 「 [バッファーの割り当てと解放](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) 」セクションで説明したように、遅延バッファーのアドレスは、バッファーがバインド解除されるまで有効なままにしておく必要があります。  
  
 特に禁止されていない限り、データバッファーのアドレスを null ポインターにすることができます。 ドライバーにデータを送信するために使用されるバッファーの場合、ドライバーは通常、バッファーに格納されている情報を無視します。 ドライバーからデータを取得するために使用されるバッファーの場合、ドライバーは値を返さないようにします。 どちらの場合も、ドライバーは対応するデータバッファー長引数を無視します。
