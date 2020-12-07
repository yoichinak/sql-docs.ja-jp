---
description: スカラー関数のエスケープ シーケンス
title: スカラー関数のエスケープシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b00be53fa0b9e23c2ee2b4e9cbac2db8e9884bc7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424944"
---
# <a name="scalar-function-escape-sequence"></a>スカラー関数のエスケープ シーケンス
ODBC では、スカラー関数にエスケープシーケンスを使用します。 このエスケープシーケンスの構文は次のとおりです。  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>解説  
 BNF 表記では、構文は次のようになります。  
  
 *ODBC スカラー関数-escape* :: =  
  
 *Odbc-esc-イニシエーター* fn *スカラー関数 ODBC-esc-ターミネータ*  
  
 *スカラー関数* :: = *関数名* (*引数リスト*)  
  
 (非終端の *関数名* と *関数名* (*引数リスト*) の定義は、 [「付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」のスカラー関数の一覧から派生します)。  
  
 *ODBC-esc-イニシエーター* :: = {  
  
 *ODBC-esc-ターミネータ* :: =}  
  
 データソースがプロシージャをサポートしているかどうか、およびドライバーが ODBC プロシージャ呼び出し構文をサポートしているかどうかを判断するために、アプリケーションは **SQLGetInfo**を呼び出すことができます。 詳細については、「 [付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」を参照してください。
