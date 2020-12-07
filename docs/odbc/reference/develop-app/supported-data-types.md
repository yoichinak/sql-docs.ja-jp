---
description: サポートされるデータ型
title: サポートされるデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349636553112449485d99fed269a43069974fccf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385828"
---
# <a name="supported-data-types"></a>サポートされるデータ型
Dbms でサポートされるデータ型は大きく異なります。 アプリケーションでは、 **SQLGetTypeInfo**を呼び出すことによって、サポートされているデータ型の名前と特性を判断できます。 データ型名にはさまざまなバリエーションがあるため、アプリケーションは**CREATE TABLE**ステートメントで**SQLGetTypeInfo**によって返されるデータ型名を使用する必要があります。 詳細については、「 [ODBC のデータ型](../../../odbc/reference/develop-app/data-types-in-odbc.md)」を参照してください。
