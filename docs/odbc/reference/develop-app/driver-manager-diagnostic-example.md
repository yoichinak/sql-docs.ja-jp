---
description: ドライバー マネージャー診断の例
title: ドライバーマネージャーの診断の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1d852436600ffb3ce5258e731d23c4579bf8964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483065"
---
# <a name="driver-manager-diagnostic-example"></a>ドライバー マネージャー診断の例
ドライバーマネージャーは診断メッセージを生成することもできます。 たとえば、アプリケーションで **Sqldatasources ソース**に無効な direction オプションが渡された場合、ドライバーマネージャーは **SQLGetDiagRec**から次の値を書式設定して返します。  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 このエラーは Driver Manager で発生したため、ベンダ ([Microsoft]) とその識別子 ([ODBC Driver Manager]) の診断メッセージにプレフィックスが追加されました。
