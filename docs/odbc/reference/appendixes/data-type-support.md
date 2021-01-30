---
description: データ型のサポート
title: データ型のサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b9249539c87e727b293c73ee12ed0fa734e08fa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99179536"
---
# <a name="data-type-support"></a>データ型のサポート
ODBC ドライバーは、少なくとも1つの SQL_CHAR と SQL_VARCHAR をサポートしている必要があります。 その他のデータ型のサポートは、ドライバーまたはデータソースの SQL-92 準拠レベルによって決まります。 アプリケーションは、 **SQLGetTypeInfo** を呼び出して、ドライバーでサポートされているデータ型を特定する必要があります。  
  
 データ型の詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。
