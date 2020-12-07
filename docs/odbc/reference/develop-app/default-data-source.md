---
description: 既定のデータ ソース
title: 既定のデータソース |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0aecd2ec64926a9d1a38d8e3d603124d45223004
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424717"
---
# <a name="default-data-source"></a>既定のデータ ソース
ドライバーは、既定のデータソースと呼ばれるデータソースを選択することがあります。ただし、アプリケーションで明示的に指定されていない場合があります。  
  
-   **SQLConnect**の呼び出しで、 *ServerName*引数が長さ0の文字列、null ポインター、または DEFAULT です。  
  
-   **SQLDriverConnect**の呼び出しで、 *inconnectionstring*は**dsn**= DEFAULT を指定するか、 **dsn**キーワードにシステム情報に含まれていないデータソースを指定します。  
  
 既定のデータソースを指定する方法はドライバーで定義されています。 これには管理操作が含まれる場合があり、ユーザーによって異なる場合があります。
