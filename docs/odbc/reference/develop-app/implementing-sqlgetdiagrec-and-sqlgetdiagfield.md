---
description: SQLGetDiagRec および SQLGetDiagField の実装
title: SQLGetDiagRec と SQLGetDiagField | を実装するMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91e43252aea4ebf12dedcb14bb1b7fb34f75df6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461434"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec および SQLGetDiagField の実装
**SQLGetDiagRec** と **SQLGetDiagField** は、ドライバーマネージャーと各ドライバーによって実装されます。 ドライバーマネージャーと各ドライバーは、各環境、接続、ステートメント、記述子ハンドルの診断レコードを保持し、そのハンドルを使用して別の関数が呼び出された場合、またはハンドルが解放された場合にのみ、これらのレコードを解放します。  
  
 ドライバーマネージャーと各ドライバーは、 [一連の状態レコードの順序](../../../odbc/reference/develop-app/sequence-of-status-records.md)に従って最初のステータスレコードを特定する必要がありますが、ドライバーマネージャーは最後のレコードのシーケンスを決定します。  
  
 **SQLGetDiagRec** と **SQLGetDiagField** は、自身に関する診断レコードを投稿しません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [診断の処理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [ドライバー マネージャーのロール](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [ドライバーのロール](../../../odbc/reference/develop-app/role-of-the-driver.md)
