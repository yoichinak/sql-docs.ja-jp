---
description: 記述子フィールドの値の取得
title: 記述子フィールドの値を取得する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2118efe58b076287dd75192de679bdb74299435
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494650"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>記述子フィールドの値の取得
アプリケーションは **SQLGetDescField** を呼び出すことで、記述子レコードの1つのフィールドを取得できます。 **SQLGetDescField** では、ODBC で定義されているすべての記述子フィールドとドライバー定義フィールドへのアクセスがアプリケーションに与えられます。  
  
 **Sqlgetdescrec** を呼び出して、列またはパラメーターのデータのデータ型とストレージに影響を与える複数の記述子フィールドの設定を取得できます。
