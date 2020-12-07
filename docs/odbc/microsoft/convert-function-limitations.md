---
description: CONVERT 関数の制限事項
title: 関数の制限の変換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, CONVERT function limitations
- Convert function limitations [ODBC]
ms.assetid: 3c81fc58-57f0-4dd7-be16-2b146eb15cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56c1d9704026511f68e76260bb4495acf1a872bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466464"
---
# <a name="convert-function-limitations"></a>CONVERT 関数の制限事項
型変換エラーが発生すると、影響を受ける列が NULL に設定されます。  
  
 DATE も TIMESTAMP データ型も、CONVERT 関数によって別のデータ型 (またはそれ自体) に変換することはできません。
