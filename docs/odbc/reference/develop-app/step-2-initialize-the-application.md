---
description: 手順 2:アプリケーションを初期化する
title: '手順 2: アプリケーションを初期化する |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d20a5b10ee7b414b9285a388359b3a93029f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482885"
---
# <a name="step-2-initialize-the-application"></a>手順 2:アプリケーションを初期化する
2番目の手順では、次の図に示すように、アプリケーションを初期化します。 ここで実行する内容は、アプリケーションによって異なります。  
  
 ![ODBC アプリケーションの初期化](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 この時点で、 **SQLGetInfo** を使用してドライバーの機能を検出するのが一般的です。 詳細については、「 [使用するデータベース機能の検討](../../../odbc/reference/develop-app/considering-database-features-to-use.md)」を参照してください。  
  
 すべてのアプリケーションは **SQLAllocHandle**を使用してステートメントハンドルを割り当てる必要があり、多くのアプリケーションでは、 **SQLSetStmtAttr**を使用して、カーソルの種類などのステートメント属性を設定します。 詳細については、「ステートメントハンドルおよび[ステートメント属性](../../../odbc/reference/develop-app/statement-attributes.md)[の割り当て](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)」を参照してください。
