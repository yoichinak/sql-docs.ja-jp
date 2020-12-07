---
description: 'Jet: 日付、時刻、およびタイムスタンプのリテラル'
title: 'Jet: Date、Time、および Timestamp リテラル |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02b2a7c5c633ee891dbcd962786cb1904bfd5df8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449444"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: 日付、時刻、およびタイムスタンプのリテラル
相互運用性を最大にするために、アプリケーションは、エスケープ句の構文を使用して、ODBC 標準形式で日付リテラルを渡す必要があります。  
  
-   日付リテラルの場合は {d '*値*'}。ここで、 *valu*e の形式は "yyyy-mm-dd" です。  
  
-   時刻リテラルの場合は {t '*値*'}。ここで、 *valu*e の形式は "hh: mm: ss" です。  
  
 タイムスタンプリテラル {ts '*値*'}。ここで、 *valu*e は、"yyyy-mm-dd hh: mm: ss [...]" という形式になっています。
