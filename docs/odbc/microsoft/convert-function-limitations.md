---
description: CONVERT 関数の制限事項
title: 関数の制限の変換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC SQL grammar, CONVERT function limitations
- Convert function limitations [ODBC]
ms.assetid: 3c81fc58-57f0-4dd7-be16-2b146eb15cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7f953f272b30095e31e68fa1bc2b6972bb4b6d3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99159548"
---
# <a name="convert-function-limitations"></a>CONVERT 関数の制限事項
型変換エラーが発生すると、影響を受ける列が NULL に設定されます。  
  
 DATE も TIMESTAMP データ型も、CONVERT 関数によって別のデータ型 (またはそれ自体) に変換することはできません。
