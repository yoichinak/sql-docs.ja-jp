---
description: Bookmark C データ型
title: ブックマーク C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4647002d5e57ea20656a4fa2dec03aa8092b9b36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411258"
---
# <a name="bookmark-c-data-type"></a>Bookmark C データ型
ブックマーク C データ型を使用すると、アプリケーションでブックマークを取得できます。 ブックマーク C 型は、長さが可変のブックマーク値を取得するためにのみ使用されます。他のデータ型に変換することはできません。 アプリケーションは、 **Sqlbulkoperations** (操作が SQL_ADD)、 **sqlfetch**、 **Sqlbulkoperations**、または **SQLGetData**を使用して、結果セットの列0からブックマークを取得します。 詳細については、「 [ブックマーク](../../../odbc/reference/develop-app/bookmarks-odbc.md)」を参照してください。  
  
 次の表に、bookmark C データ型の *CType* の値、ブックマーク c データ型を実装する ODBC c データ型、および SQL からのこのデータ型の定義を示します。始め.  
  
> [!NOTE]
>  SQL_C_BOOKMARK のデータ型は非推奨とされました。 ODBC *3. x* アプリケーションでは、SQL_C_BOOKMARK を使用しないでください。 ODBC *3.x ドライバーは* 、それを使用する odbc *2.x アプリケーションを* 操作する場合にのみ、SQL_C_BOOKMARK をサポートする必要があります。 ドライバーマネージャーは、アプリケーション *が ODBC 2.x* ドライバーで動作する場合に SQL_C_VARBOOKMARK を SQL_C_BOOKMARK にマップします。  
  
|C 型識別子|ODBC C typedef|C 型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(非推奨)|ブックマーク|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
