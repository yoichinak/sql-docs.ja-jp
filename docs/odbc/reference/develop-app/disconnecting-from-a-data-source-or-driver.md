---
description: データ ソースまたはドライバーからの切断
title: データソースまたはドライバーからの切断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc14ca0ebf29a2ab203a4408db4b5681ad667497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476694"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>データ ソースまたはドライバーからの切断
アプリケーションでデータソースの使用が完了すると、 **Sqldisconnect**が呼び出されます。 **Sqldisconnect** は、接続に割り当てられているすべてのステートメントを解放し、データソースからドライバーを切断します。 トランザクションが処理中の場合は、エラーが返されます。  
  
 切断後、アプリケーションは **Sqlfreehandle** を呼び出して接続を解放できます。 接続を解放した後、ODBC 関数の呼び出しで接続のハンドルを使用するアプリケーションプログラミングエラーになります。この操作を行うと、未定義になりますが、致命的な結果になります。 **Sqlfreehandle**が呼び出されると、ドライバーは、接続に関する情報を格納するために使用される構造体を解放します。  
  
 また、アプリケーションは接続を再利用して、別のデータソースに接続したり、同じデータソースに再接続したりすることもできます。 接続を切断し、後で再接続するのではなく、接続を維持するかどうかを判断するには、アプリケーションの作成者が各オプションの相対的なコストを考慮する必要があります。接続メディアによっては、データソースへの接続と接続の残りの部分が比較的コストがかかることがあります。 また、アプリケーションでは、適切なトレードオフを行う際に、同じデータソースに対する後続の操作の可能性とタイミングについても想定する必要があります。
