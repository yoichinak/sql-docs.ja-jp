---
description: バインディング列
title: 列のバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f3f02ec6487b34a6ca2c973c3115c3940ca8fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429434"
---
# <a name="binding-columns"></a>バインディング列
データソースからフェッチされたデータは、アプリケーションによってこの目的で割り当てられた変数でアプリケーションに返されます。 これを行うには、アプリケーションがこれらの変数を結果セットの列に関連付けるか、または *バインド*する必要があります。概念的には、このプロセスは、ステートメントパラメーターへのアプリケーション変数のバインドと同じです。 アプリケーションが変数を結果セット列にバインドすると、その変数アドレス、データ型などがドライバーに対して記述されます。 ドライバーは、この情報をそのステートメント用に保持する構造体に格納し、その情報を使用して、行がフェッチされるときに列から値を返します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [結果セットの列のバインド](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [SQLBindCol の使用](../../../odbc/reference/develop-app/using-sqlbindcol.md)
