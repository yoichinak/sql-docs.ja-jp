---
description: 値リストの引数
title: 値リストの引数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd2f2e970ea94635cda0b43b741abfda1130645b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421416"
---
# <a name="value-list-arguments"></a>値リストの引数
値リストの引数は、照合に使用するコンマ区切り値のリストで構成されます。 ODBC カタログ関数には、値リストの引数が1つだけあります。 **Sqltables**の*TableType*引数です。 *TableType*を null ポインターに設定することは SQL_ALL_TABLE_TYPES に設定されている場合と同じです。これにより、値リストのすべての可能なメンバーが列挙されます。 この引数は、SQL_ATTR_METADATA_ID statement 属性の影響を受けません。 詳細については、 [Sqltables](../../../odbc/reference/syntax/sqltables-function.md) 関数の説明を参照してください。
