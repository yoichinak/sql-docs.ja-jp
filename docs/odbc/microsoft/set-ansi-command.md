---
description: SET ANSI コマンド
title: SET ANSI Command |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9f9c576199905c23994af4dc6b031114f4ad72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466404"
---
# <a name="set-ansi-command"></a>SET ANSI コマンド
Visual FoxPro SQL コマンドで、= 演算子を使用して長さが異なる文字列間の比較を行う方法を決定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 (ドライバーの既定値は、Visual FoxPro の既定値は OFF です)。短い文字列に、長い文字列の長さと同じにするために必要な空白を埋め込みます。 2つの文字列は、その長さ全体の文字の文字を比較します。 次の比較を検討してください。  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果は False (です。F.) SET ANSI がオンの場合、埋め込まれたときに ' Tom ' は ' Tom ' になり、文字列 ' Tom ' と ' Tommy ' は文字の文字と一致しません。  
  
 = = 演算子は、Visual FoxPro SQL コマンドの比較にこのメソッドを使用します。  
  
 OFF  
 短い文字列に空白が埋め込まれないように指定します。 2つの文字列は、短い文字列の末尾に到達するまで、文字の文字を比較します。 次の比較を検討してください。  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果は True (.T.) SET ANSI が off の場合、比較は ' Tom ' の後で停止するためです。  
  
## <a name="remarks"></a>解説  
 SQL 文字列比較の実行時に、2つの文字列の短い方に空白が埋め込まれるかどうかを設定します。 SET ANSI は、= = 演算子には影響しません。= = 演算子を使用すると、比較のために短い文字列には常に空白が埋め込まれます。  
  
## <a name="string-order"></a>文字列の順序  
 SQL コマンドでは、比較において、2つの文字列の左から右の順序は、= または = = 演算子の一方の側からもう一方の側の文字列を比較しても、比較の結果には影響しません。  
  
## <a name="see-also"></a>関連項目  
 [SELECT-SQL コマンド](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT コマンド](../../odbc/microsoft/set-exact-command.md)
