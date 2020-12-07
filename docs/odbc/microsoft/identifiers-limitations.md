---
description: 識別子の制限事項
title: 識別子の制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5efaba8fa73f61082be8d7cd8dca78626a9f972
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500345"
---
# <a name="identifiers-limitations"></a>識別子の制限事項
識別子に空白または特殊な記号が含まれている場合は、識別子を逆引用符で囲む必要があります。 有効な名前は、64文字以内の文字列で、最初の文字をスペースにすることはできません。 有効な名前には、制御文字または次の特殊文字を含めることはできません: ' &#124; # *? [ ] . ! $ .  
  
 SQL の文法に記載されている予約語は、 *ODBC プログラマーズリファレンス* の付録 C (または、これらの予約語の短縮形) の識別子として使用しないでください (または、テーブル名または列名)。これは、単語を引用符 (') で囲む場合を除きます。
