---
description: ODBC ドライバーのサブキー
title: ODBC ドライバーのサブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b950a352c3da69a2a8de9a89f7bbebf87e0a597a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448922"
---
# <a name="odbc-drivers-subkey"></a>ODBC ドライバーのサブキー
[ODBC ドライバー] サブキーの下の値には、インストールされているドライバーが一覧表示されます。 これらの値の形式を次の表に示します。  
  
|名前|データ型|データ|  
|----------|---------------|----------|  
|*ドライバー-説明*|REG_SZ|**インストール済み**|  
  
 *ドライバーの説明*名は、ドライバーの開発者によって定義されます。 通常は、ドライバーに関連付けられている DBMS の名前です。  
  
 たとえば、フォーマットされたテキストファイルと SQL Server にドライバーがインストールされているとします。 ODBC ドライバーサブキーの下の値は次のようになります。  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
