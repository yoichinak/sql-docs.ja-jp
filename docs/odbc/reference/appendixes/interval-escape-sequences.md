---
description: Interval のエスケープ シーケンス
title: 間隔エスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0badac832ee4cf4e29f148dbd39a7989536b9c29
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99176494"
---
# <a name="interval-escape-sequences"></a>Interval のエスケープ シーケンス
ODBC では、間隔リテラルにエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
 {*interval-リテラル*}  
  
 *Interval リテラル* の BNF 構文については、この付録の後半の「 [interval リテラル構文](../../../odbc/reference/appendixes/interval-literal-syntax.md)」を参照してください。  
  
 Interval リテラルエスケープシーケンスは、データソースで interval データ型がサポートされている場合にサポートされます。 アプリケーションは、これらのデータ型がサポートされているかどうかを判断するために **SQLGetTypeInfo** を呼び出す必要があります。
