---
description: データ型のサポート
title: データ型のサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ab0fd163713a7f6657d8ce446336f5c35a3dd00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456639"
---
# <a name="data-type-support"></a>データ型のサポート
ODBC ドライバーは、少なくとも1つの SQL_CHAR と SQL_VARCHAR をサポートしている必要があります。 その他のデータ型のサポートは、ドライバーまたはデータソースの SQL-92 準拠レベルによって決まります。 アプリケーションは、 **SQLGetTypeInfo** を呼び出して、ドライバーでサポートされているデータ型を特定する必要があります。  
  
 データ型の詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。
