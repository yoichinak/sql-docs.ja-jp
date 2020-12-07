---
description: ファイル ベースのドライバー診断の例
title: ファイルベースのドライバー診断の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8986ebaa8c4ecf0ac18f4e043eb731df35054884
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499862"
---
# <a name="file-based-driver-diagnostic-example"></a>ファイル ベースのドライバー診断の例
ファイルベースのドライバーは、ODBC ドライバーとデータソースの両方として機能します。 このため、エラーと警告は、ODBC 接続のコンポーネントとしても、データソースとしても生成されます。 これは、ドライバーマネージャーとのインターフェイスを持つコンポーネントでもあるため、 **SQLGetDiagRec**の引数を書式設定して返します。  
  
 たとえば、dBASE 用の Microsoft®ドライバーが十分なメモリを割り当てられなかった場合、 **SQLGetDiagRec**から次の値が返される可能性があります。  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 このエラーはデータソースに関連付けられていないため、ドライバーは、ベンダー ([Microsoft]) とドライバー ([ODBC dBASE ドライバー]) の診断メッセージにプレフィックスを追加しただけです。  
  
 ドライバーが **SQLGetDiagRec**ファイルを見つけられなかった場合は、次の値が返される可能性があります。  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 このエラーはデータソースに関連したものであるため、ドライバーはデータソース ([dBASE]) のファイル形式をプレフィックスとして診断メッセージに追加しました。 ドライバーは、データソースとの通信を行うコンポーネントでもあるため、ベンダー ([Microsoft]) とドライバー ([ODBC dBASE ドライバー]) のプレフィックスが追加されました。
