---
description: SQL の適合性レベル
title: SQL 準拠レベル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 525cda9094213e6decf30643c23a7db623511e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499805"
---
# <a name="sql-conformance-levels"></a>SQL の適合性レベル
ドライバーでサポートされている SQL 92 文法のレベルは、SQL_SQL_CONFORMANCE 情報型の **SQLGetInfo** への呼び出しによって返される値によって示されます。 これは、ドライバーが SQL-92 で定義されているエントリ、FIPS 移行、中間、または完全なレベルに準拠しているかどうかを示します。  
  
 すべての ODBC ドライバーは、「付録 C: SQL 文法」の「 [sql の最小文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 」で説明されている最小の sql 文法をサポートしている必要があります。 この文法は、SQL-92 のエントリレベルのサブセットです。 ドライバーは、追加の SQL をサポートし、SQL-92 エントリ、中間レベル、または完全レベル、または FIPS 127-2 移行レベルに準拠している場合があります。 指定されたレベルの SQL-92 または FIPS 127-2 に準拠しているドライバーは、そのレベルに完全に準拠していない、より高いレベルの追加機能をサポートできます。 機能がサポートされているかどうかを判断するには、アプリケーションで、適切な情報の種類を使用して **SQLGetInfo** を呼び出す必要があります。 SQL 機能の準拠レベルは、対応する情報の種類で説明されています。 ( [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明を参照してください)。
