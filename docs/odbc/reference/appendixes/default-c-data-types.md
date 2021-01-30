---
description: 既定の C データ型
title: 既定の C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd7f50e58fd84cec5938aacc598d12e6d733fcdc
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194899"
---
# <a name="default-c-data-types"></a>既定の C データ型
アプリケーションで **SQLBindCol**、 **SQLGetData**、または **SQLBindParameter** の SQL_C_DEFAULT が指定されている場合、ドライバーでは、出力バッファーまたは入力バッファーの C データ型が、バッファーのバインド先の列またはパラメーターの SQL データ型に対応していると見なされます。  
  
> [!IMPORTANT]  
>  相互運用可能なアプリケーションでは、SQL_C_DEFAULT を使用しないでください。 代わりに、使用しているバッファーの C 型を常に指定する必要があります。 これは、次の理由により、ドライバーが既定の C 型を常に正しく特定できないためです。  
  
-   DBMS が列またはパラメーターの SQL データ型を昇格させる場合、ドライバーは、列またはパラメーターの元の SQL データ型を特定できません。 したがって、対応する既定の C データ型を決定することはできません。  
  
-   ドライバーが、特定の列またはパラメーターが署名されているかどうかを判断できない場合、これが DBMS によって処理される場合と同様に、ドライバーは、対応する既定の C データ型が署名されているか署名なしであるかを判断できません。  
  
     SQL_C_DEFAULT はプログラミングの便宜的な機能としてのみ提供されるため、実際の C データ型を指定しても、アプリケーションは機能を失いません。  
  
 各 SQL データ型の既定の C データ型を示す表は、この付録の「 [sql から c データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」に含まれています。
