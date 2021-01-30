---
description: 外部結合のエスケープ シーケンス
title: 外部結合のエスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e25cde1a4da326d06efe23bc2f7c642e61589ff3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160858"
---
# <a name="outer-join-escape-sequence"></a>外部結合のエスケープ シーケンス
ODBC では外部結合にエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>コメント  
 BNF 表記では、構文は次のようになります。  
  
 *ODBC 外部結合-エスケープ* :: =  
  
 *Odbc-esc-イニシエーター* oj *外部結合 odbc-esc-ターミネータ*  
  
 *外部結合* :: = *テーブル名* [*相関名*] {LEFT &#124; RIGHT &#124; FULL}  
  
 外部結合 {*テーブル名* [*相関名*] &#124; *外部結合*} ON  
  
 *サーチ*  
  
 *condition*  
  
 *相関名* :: = *ユーザー定義-名前*  
  
 *ODBC-esc-イニシエーター* :: = {  
  
 *ODBC-esc-ターミネータ* :: =}  
  
 このステートメントのどの部分がサポートされているかを判断するために、アプリケーションは SQL_OJ_CAPABILITIES 情報の種類を使用して **SQLGetInfo** を呼び出します。 外部結合の場合、 *検索条件* には、指定された *テーブル名* 間の結合条件だけを含める必要があります。
