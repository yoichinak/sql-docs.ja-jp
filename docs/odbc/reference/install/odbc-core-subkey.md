---
description: ODBC Core サブキー
title: ODBC Core サブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37948c46d6a717975902bc2109ece2aea02b0129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499737"
---
# <a name="odbc-core-subkey"></a>ODBC Core サブキー
ODBC Core サブキーの下の値は、コアコンポーネント (ドライバーマネージャー、カーソルライブラリ、インストーラー DLL など) の使用回数を示します。 この値の形式を次の表に示します。  
  
|名前|データ型|データ|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 たとえば、3つの異なるアプリケーション用のセットアッププログラムによって ODBC Core コンポーネントがインストールされていて、2つの異なるドライバーがインストールされているとします。 ODBC Core サブキーの下の値は次のようになります。  
  
```  
UsageCount : REG_DWORD : 0x5  
```
