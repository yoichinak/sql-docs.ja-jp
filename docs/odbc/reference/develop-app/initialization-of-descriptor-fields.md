---
description: 記述子フィールドの初期化
title: 記述子フィールドの初期化 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2537e5e74c600c72368e46bda7640b881d9a34df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424654"
---
# <a name="initialization-of-descriptor-fields"></a>記述子フィールドの初期化
アプリケーションの行記述子が割り当てられると、そのフィールドには [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)に示されている初期値が与えられます。 SQL_DESC_TYPE フィールドの初期値は SQL_DEFAULT です。 これにより、アプリケーションに表示するためのデータベースデータの標準的な処理が提供されます。 アプリケーションでは、記述子レコードのフィールドを設定することによって、異なるデータ処理を指定できます。  
  
 記述子ヘッダー内の SQL_DESC_ARRAY_SIZE の初期値は1です。 アプリケーションでこのフィールドを変更して、複数行のフェッチを有効にすることができます。  
  
 既定値の概念は、IRD のフィールドでは無効です。 アプリケーションは、準備されたステートメントまたは実行されたステートメントが関連付けられている場合にのみ、IRD のフィールドにアクセスできます。  
  
 IPD の特定のフィールドは、IPD がドライバーによって自動的に設定された後にのみ定義されます。 定義されていない場合は未定義です。 これらのフィールドは、SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED、および SQL_DESC_LOCAL_TYPE_NAME です。
