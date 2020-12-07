---
description: LIKE エスケープ シーケンス
title: LIKE エスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19d20f80f9fea4df2c508ec4ec4bcc2ee6718986
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429644"
---
# <a name="like-escape-sequence"></a>LIKE エスケープ シーケンス
ODBC では、LIKE 句にエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>解説  
 BNF 表記では、構文は次のようになります。  
  
 *ODBC のような-escape* :: =  
  
 *Odbc-esc-開始側* エスケープ '*エスケープ文字*' *odbc-esc-ターミネータ*  
  
 *エスケープ文字* :: = *文字*  
  
 *ODBC-esc-イニシエーター* :: = {  
  
 *ODBC-esc-ターミネータ* :: =}  
  
 ドライバーで LIKE エスケープシーケンスがサポートされているかどうかを判断するために、アプリケーションは SQL_LIKE_ESCAPE_CLAUSE 情報の種類を使用して **SQLGetInfo** を呼び出すことができます。
