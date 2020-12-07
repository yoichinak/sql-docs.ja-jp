---
description: カタログ関数の実行
title: カタログ関数の実行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19baae1518078c44b8e170fb623eab0087bac12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482915"
---
# <a name="executing-catalog-functions"></a>カタログ関数の実行
カタログ関数は結果セットを作成するので、結果セット生成の SQL ステートメントを実行するのと同じです。 実際、カタログ関数は、定義済みの SQL ステートメントを実行したり、ドライバーまたは DBMS に付属する定義済みプロシージャを呼び出したりすることによって実装されます。 結果セットを作成する SQL ステートメントに適用されるほとんどすべての処理は、カタログ関数にも適用されます。 たとえば、SQL_ATTR_MAX_ROWS statement 属性では、 **SELECT** ステートメントによって返される行の数を制限するのと同じように、カタログ関数によって返される行の数が制限されます。  
  
 カタログ関数を実行するために、アプリケーションは関数を呼び出します。  
  
 カタログ関数の詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。
