---
description: 予約済みキーワードの制限事項
title: 予約語の制限 |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e615ab4c8222ec7ac679f96f360458dfaab5abb9
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99182574"
---
# <a name="reserved-keyword-limitations"></a>予約済みキーワードの制限事項

SQL テーブルや関連オブジェクトの識別子として、ODBC の予約済みキーワードを使用することは避けてください。 予約済みキーワードを識別子として使用する必要がある場合に、奇数の場合は、 *バックティック* (') のペアで識別子を囲む必要があります。 *バックティック* のもう1つの名前は、*バッククォート* です。

予約済みキーワードの制限は、予約済みキーワードの短縮形にも適用されます。

ODBC の予約済みキーワードの一覧については、以下を参照してください。

- [ODBC の予約済みキーワード](../reference/appendixes/reserved-keywords.md)。

- *ODBC プログラマーズリファレンスガイド* については、「[付録 C: SQL 文法](../reference/appendixes/appendix-c-sql-grammar.md)」を参照してください。