---
description: 文字列の制限事項
title: 文字列に関する制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12d02a6e69b34c13219e4bb5f00aeacfa9945cfb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188927"
---
# <a name="string-limitations"></a>文字列の制限事項
SQL ステートメント文字列の最大長は65000文字です。  
  
 Microsoft Access ドライバーが使用されている場合は、SQL-92 文字列定数 (二重引用符ではなく、単一引用符で囲む) のみがサポートされます。  
  
 文字が逆引用符で囲まれているかどうかにかかわらず、パイプ文字 (&#124;) を文字列内で使用することはできません。  
  
 相互運用性を最大にするために、アプリケーションは、引用符で囲まれた文字列を渡すのではなく、パラメーターに文字列を渡す必要があります。
