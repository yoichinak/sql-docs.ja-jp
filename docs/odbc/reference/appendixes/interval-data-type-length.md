---
description: Interval データ型の長さ
title: Interval データ型の長さ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 589a13e0f0b2c6e6e42ade0f0dc32415556a0efc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483284"
---
# <a name="interval-data-type-length"></a>Interval データ型の長さ
次の規則は、期間データ型の長さを文字数で決定するために使用されます。 長さは文字数で表現されます。 バイト数は、文字セットによって異なります。 長さには、次の値が一緒に追加されます。  
  
-   先頭のフィールドではない、間隔内のすべてのフィールドに対して2文字。  
  
-   先頭のフィールドで、明示的または暗黙的な有効桁数である文字の数。 先頭の有効桁数が指定されていない場合、既定値は2です。  
  
-   フィールド間の区切り記号として1文字。  
  
-   1に加えて、秒または暗黙の秒の有効桁数。 秒の有効桁数が指定されていない場合、既定値は6です。  
  
 各 interval データ型の特定の列長の値は、 [列のサイズ](../../../odbc/reference/appendixes/column-size.md)に含まれています。
