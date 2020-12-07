---
description: Jet 4.0 は ExtendedAnsiSQL_Set で SQL-92 の予約語リストを使用
title: Jet 4.0 では、SQL-92 の予約語の一覧を使用して ExtendedAnsiSQL_Set |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 464a2b57f5778c7b964e8462d37ab4e1873cead7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449454"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>Jet 4.0 は ExtendedAnsiSQL_Set で SQL-92 の予約語リストを使用
ExtendedAnsiSQL フラグが有効になっている場合、Jet 4.0 では、SQL-92 の予約語の一覧が使用されます。 SQL-92 の予約語を引用符で囲まれていないオブジェクト名として使用しようとすると、構文エラーが発生します。 ExtendedAnsiSQL フラグがオフになっている場合は、以前と同じように、新しい予約語をオブジェクト名として使用できます。
