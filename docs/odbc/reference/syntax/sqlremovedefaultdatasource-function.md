---
description: SQLRemoveDefaultDataSource 関数
title: SQLRemoveDefaultDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0010e59cc4dfad2d54b8b1c4e59e83ea72fcd3ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487090"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 関数
**互換性**  
 導入されたバージョン: ODBC 1.0、非推奨  
  
 **まとめ**  
 ODBC 3.0 では、 **Sqlremovedefaultdatasource**関数は、ODBC_REMOVE_DEFAULT_DSN の*frequest*引数を使用して[sqlconfigdatasource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)への呼び出しに置き換えられました。 ODBC 2.x のインストールプログラムがこの関数を呼び出すと、ODBC インストーラーによって、次の**Sqlconfigdatasource**呼び出しにマップさ*れます。*  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
