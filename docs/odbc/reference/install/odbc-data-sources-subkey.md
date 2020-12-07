---
description: ODBC データソースサブキー
title: ODBC データソースサブキー |Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9897c68d110f59d03ac8e1b3e403ed21844082fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448934"
---
# <a name="odbc-data-sources-subkey"></a>ODBC データソースサブキー

サブキーの下の値には、 `ODBC Data Sources` データソースが一覧表示されます。 これらの値の形式を次の表に示します。

| 名前 | データ型 | データ |
| :--- | :-------- | :--- |
| *データソース名* | REG_SZ | *ドライバー-説明* |
| &nbsp; | &nbsp; | &nbsp; |

*データソース名*の値は、管理プログラムによって定義されます (通常はユーザーにプロンプトを表示します)。*ドライバーの説明*は、ドライバーの開発者によって定義されます (通常は、ドライバーに関連付けられている DBMS の名前です)。

たとえば、SQL Server を使用する Inventory という3つのデータソースが定義されているとします。DBASE を使用する Payroll書式設定されたテキストファイルを使用するスタッフ。 サブキーの下の値は次のように `ODBC Data Sources` なります。

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
