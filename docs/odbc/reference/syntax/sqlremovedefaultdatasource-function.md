---
description: SQLRemoveDefaultDataSource 関数
title: SQLRemoveDefaultDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
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
ms.openlocfilehash: 326522986785d7e76bc781fa4cc912401f2c237e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99192521"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 関数
**互換性**  
 導入されたバージョン: ODBC 1.0、非推奨  
  
 **要約**  
 ODBC 3.0 では、 **Sqlremovedefaultdatasource** 関数は、ODBC_REMOVE_DEFAULT_DSN の *frequest* 引数を使用して [sqlconfigdatasource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)への呼び出しに置き換えられました。 ODBC 2.x のインストールプログラムがこの関数を呼び出すと、ODBC インストーラーによって、次の **Sqlconfigdatasource** 呼び出しにマップさ *れます。*  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
