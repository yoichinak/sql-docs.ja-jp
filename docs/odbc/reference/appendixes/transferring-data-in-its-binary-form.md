---
description: バイナリ形式でのデータ転送
title: バイナリ形式でデータを転送する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec858729e76c1e360ec0933eca3a29ab17542f4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386328"
---
# <a name="transferring-data-in-its-binary-form"></a>バイナリ形式でのデータ転送
アプリケーションは、同じ DBMS とハードウェアプラットフォームを使用する2つのデータソース間で、(指定された DBMS によって使用される内部形式の) データを安全に転送できます。 データの種類によっては、ソースとターゲットのデータソースで SQL データ型が同じである必要があります。 C データ型は SQL_C_BINARY です。  
  
 アプリケーションが、ソースデータソースからデータを取得するために **Sqlfetch**、 **sqlfetchscroll**、または **SQLGetData** を呼び出すと、ドライバーはデータソースからデータを取得し、そのデータを変換せずに、SQL_C_BINARY 型のストレージの場所に転送します。 アプリケーションが **Sqlbulkoperations**、 **sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations、または SQLSetPos** を呼び出してターゲットデータソースにデータを送信すると、ドライバーはストレージの場所からデータを取得し、変換を行わずにターゲットデータソースに転送します。  
  
> [!NOTE]  
>  この方法で任意のデータ (バイナリデータを除く) を転送するアプリケーションは、Dbms 間で相互運用できません。  
  
 **Sqlcopydesc** を使用して、ソース dbms からターゲット dbms のパラメーターバインドに行バインドをコピーできます。
