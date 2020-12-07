---
description: ブックマークの取得
title: ブックマークを取得する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22fba0ccc900d221e915fea939736aa87b101e80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429094"
---
# <a name="retrieving-bookmarks"></a>ブックマークの取得
アプリケーションでブックマークを使用する場合は、ステートメントを準備または実行する前に、SQL_ATTR_USE_BOOKMARKS ステートメントの属性を SQL_UB_VARIABLE に設定する必要があります。 これが必要なのは、ブックマークの作成と維持が負荷の高い操作である可能性があるためです。そのため、ブックマークは、アプリケーションで適切に使用できる場合にのみ有効にする必要があります。  
  
 ブックマークは、結果セットの列0として返されます。 アプリケーションでは、次の3つの方法で取得できます。  
  
-   結果セットの列0をバインドします。 **Sqlfetch** または **sqlfetchscroll** は、行セット内の行ごとに、他のバインドされた列のデータと共にブックマークを返します。  
  
-   **SQLSetPos**を呼び出して、行セット内の行に移動し、列0に対して**SQLGetData**を呼び出します。 ドライバーがブックマークをサポートしている場合、最後にバインドされた列の前にある他の列に対して**SQLGetData**を呼び出すことをアプリケーションに許可していない場合でも、列0に対して**SQLGetData**を呼び出すことができるようにする必要があります。  
  
-   *操作*引数を SQL_ADD に設定し、列0をバインドして**sqlbulkoperations**を呼び出します。 カーソルによって行が挿入され、バインドされたバッファー内の行のブックマークが返されます。
