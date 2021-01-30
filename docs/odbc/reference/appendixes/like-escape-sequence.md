---
description: LIKE エスケープ シーケンス
title: LIKE エスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d32b0470cb2adf0960e23dac17d8cb4942f296c0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184389"
---
# <a name="like-escape-sequence"></a>LIKE エスケープ シーケンス
ODBC では、LIKE 句にエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>コメント  
 BNF 表記では、構文は次のようになります。  
  
 *ODBC のような-escape* :: =  
  
 *Odbc-esc-開始側* エスケープ '*エスケープ文字*' *odbc-esc-ターミネータ*  
  
 *エスケープ文字* :: = *文字*  
  
 *ODBC-esc-イニシエーター* :: = {  
  
 *ODBC-esc-ターミネータ* :: =}  
  
 ドライバーで LIKE エスケープシーケンスがサポートされているかどうかを判断するために、アプリケーションは SQL_LIKE_ESCAPE_CLAUSE 情報の種類を使用して **SQLGetInfo** を呼び出すことができます。
