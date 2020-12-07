---
description: ドライバーの仕様のサブキー
title: トランスレーター指定サブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c02317c8abe12dbc693cdf7b715b6de84e5bc631
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461294"
---
# <a name="translator-specification-subkeys"></a>ドライバーの仕様のサブキー
ODBC トランスレーターのサブキーに記載されている各トランスレーターには、独自のサブキーがあります。 このサブキーには、ODBC トランスレーターサブキーの下にある対応する値と同じ名前が付けられています。 このサブキーの下の値には、translator および translator セットアップ Dll の完全なパスと使用量が一覧表示されます。 値の形式を次の表に示します。  
  
|名前|データ型|データ|  
|----------|---------------|----------|  
|[変換者]|REG_SZ|*translator-DLL-パス*|  
|設定|REG_SZ|*setup.exe-path*|  
|UsageCount|REG_DWORD|*count*|  
  
 使用量の詳細については、このセクションで前述した [使用量のカウント](../../../odbc/reference/install/usage-counting.md) に関するセクションを参照してください。  
  
 アプリケーションで使用状況カウントを設定しないでください。 ODBC ではこのカウントが維持されます。  
  
 たとえば、Microsoft コードページトランスレーターに Mscpxl32.dll という名前の翻訳 DLL があり、translator セットアップ関数が同じ DLL 内にあり、翻訳者が3回インストールされているとします。 Microsoft コードページトランスレーターサブキーの下の値は、次のようになります。  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
