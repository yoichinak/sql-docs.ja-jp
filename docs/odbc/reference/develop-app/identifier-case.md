---
description: 識別子の大文字と小文字の区別
title: 識別子の Case |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ccac9b10e6a32c7265cd5f591944735454b85f80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461444"
---
# <a name="identifier-case"></a>識別子の大文字と小文字の区別
SQL ステートメントとカタログ関数の引数では、識別子と引用符で囲まれた識別子は大文字と小文字を区別するかどうかを指定できます。この場合、アプリケーションは、SQL_IDENTIFIER_CASE オプションと SQL_QUOTED_IDENTIFIER_CASE オプションを指定して **SQLGetInfo** を呼び出すことによって判断できます。  
  
 これらの各オプションには、次の4つの戻り値があります。1つは、識別子または引用符で囲まれた識別子の大文字と小文字が区別され、3番目は機密性がないことを示します。 大文字と小文字が区別されない3つの値は、識別子がシステムカタログに格納されるケースを示します。 識別子がシステムカタログに格納される方法は、アプリケーションがカタログ関数の結果を表示する場合など、表示目的のみに関連します。識別子の大文字と小文字の区別は変更されません。
