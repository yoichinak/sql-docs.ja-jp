---
description: データ ソースの仕様のサブキー
title: データソース指定サブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fabfd07779f74945bf647d20075de0cc057710b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494567"
---
# <a name="data-source-specification-subkeys"></a>データ ソースの仕様のサブキー
ODBC データソースサブキーに一覧表示される各データソースには、独自のサブキーがあります。 このサブキーには、ODBC データソースサブキーの下にある対応する値と同じ名前が付けられています。 このサブキーの下の値は、ドライバーの DLL の一覧を表示し、データソースの説明を一覧表示する必要があります。 ドライバーが変換プログラムをサポートしている場合は、既定の変換プログラムの名前、既定の翻訳 DLL、および既定の翻訳オプションが一覧表示されます。 値には、ドライバーがデータソースに接続するために必要なその他の情報も表示される場合があります。 たとえば、ドライバーでは、サーバー名、データベース名、またはスキーマ名が必要になる場合があります。  
  
 値の形式を次の表に示します。 ドライバー値のみが必要です。  
  
|名前|データ型|Data|  
|----------|---------------|----------|  
|説明|REG_SZ|*description*|  
|ドライバー|REG_SZ|*ドライバー-DLL パス*|  
|TranslationDLL|REG_SZ|*translator-DLL-パス*|  
|TranslationName|REG_SZ|*変換プログラム-名前*|  
|TranslationOption|REG_SZ|*translation-オプション*|  
|*opt-値-名前*|*opt-値型*|*opt-値-データ*|  
  
 たとえば、SQL Server ドライバーが OEM から ANSI への変換にサーバー名とフラグを必要とし、これらのサーバーと OEMTOANSI 値を定義するとします。 また、インベントリデータソースが Microsoft®コードページトランスレーターを使用して、Windows® Latin 1 (1250) と多言語 (850) のコードページを変換するとします。 Inventory サブキーの下の値は次のようになります。  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
