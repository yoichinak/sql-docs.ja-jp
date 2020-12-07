---
description: パラメーターの記述
title: パラメーターの説明 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a41bee40403cc3562c41ccc13a15c706a0772e27
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476754"
---
# <a name="describing-parameters"></a>パラメーターの記述
**SQLBindParameter** には、パラメーター (SQL の型、有効桁数、および小数点以下桁数) を記述する引数があります。 ドライバーは、この情報 (または *メタデータ)* を使用して、パラメーター値をデータソースに必要な型に変換します。 一見すると、ドライバーがアプリケーションよりもパラメーターメタデータを認識しやすい位置にあるように見えるかもしれません。結局のところ、ドライバーは結果セット列のメタデータを簡単に検出できます。 結局のところ、そうではありません。 まず、ほとんどのデータソースでは、ドライバーがパラメーターのメタデータを検出する方法が提供されていません。 次に、ほとんどのアプリケーションは既にメタデータを認識しています。  
  
 アプリケーションで SQL ステートメントがハードコーディングされている場合、アプリケーションライターは、各パラメーターの型を既に認識しています。 実行時にアプリケーションによって SQL ステートメントが構築される場合、アプリケーションはステートメントを作成するときにメタデータを判断できます。 たとえば、アプリケーションが句を構築する場合などです。  
  
```  
WHERE OrderID = ?  
```  
  
 ここでは、OrderID 列の **Sqlcolumns** を呼び出すことができます。  
  
 パラメーター化されたステートメントをユーザーが入力したときに、アプリケーションがパラメーターのメタデータを簡単に判断できない場合は、 この場合、アプリケーションは **SQLPrepare** を呼び出して、ステートメントを準備し、パラメーターの数を決定する **sqlnumparams** と、各パラメーターを記述する **SQLDescribeParam** を呼び出します。 ただし、前述のように、ほとんどのデータソースでは、ドライバーがパラメーターメタデータを検出する方法が提供されていないため、 **SQLDescribeParam** は広くサポートされていません。
