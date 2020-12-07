---
description: Interval のエスケープ シーケンス
title: 間隔エスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2ef792403352568ce5f8d92c07a5b0e1027b507
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483295"
---
# <a name="interval-escape-sequences"></a>Interval のエスケープ シーケンス
ODBC では、間隔リテラルにエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
 {*interval-リテラル*}  
  
 *Interval リテラル*の BNF 構文については、この付録の後半の「 [interval リテラル構文](../../../odbc/reference/appendixes/interval-literal-syntax.md)」を参照してください。  
  
 Interval リテラルエスケープシーケンスは、データソースで interval データ型がサポートされている場合にサポートされます。 アプリケーションは、これらのデータ型がサポートされているかどうかを判断するために **SQLGetTypeInfo** を呼び出す必要があります。
