---
description: ヘッダー レコード
title: ヘッダーレコード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4de764381e54a0b3485130c1a3bdf25b2a9bf9fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476644"
---
# <a name="header-record"></a>ヘッダー レコード
ヘッダーレコード内のフィールドには、関数の実行に関する一般的な情報が含まれています。これには、リターンコード、行数、状態レコードの数、実行されたステートメントの種類などが含まれます。 関数が SQL_INVALID_HANDLE を返さない限り、ヘッダーレコードは常に作成されます。 ヘッダーレコード内のフィールドの完全な一覧については、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 関数の説明を参照してください。
