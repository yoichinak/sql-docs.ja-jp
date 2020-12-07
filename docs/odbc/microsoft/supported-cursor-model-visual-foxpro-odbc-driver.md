---
description: サポートされるカーソル モデル (Visual FoxPro ODBC ドライバー)
title: サポートされているカーソルモデル (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 789d55a894e66c87fc5773856375757947835b35
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471534"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>サポートされるカーソル モデル (Visual FoxPro ODBC ドライバー)
Visual FoxPro ODBC ドライバーでは、 *ブロック* (*行セット*) と *静的* カーソルの両方がサポートされています。 静的カーソルは、レベル1の ODBC 準拠に準拠しているすべてのドライバーでサポートされています。 ドライバーでは、動的カーソル、キーセットドリブンカーソル、または混合 (keyset および動的) カーソルはサポートされていません。  
  
 アプリケーションでは、SQL_CURSOR_FORWARD_ONLY (ブロックカーソル) または SQL_CURSOR_STATIC (静的カーソル) の SQL_CURSOR_TYPE オプションを使用して [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) を呼び出すことができます。  
  
> [!NOTE]  
>  SQL_CURSOR_FORWARD_ONLY または SQL_CURSOR_STATIC 以外の SQL_CURSOR_TYPE オプションを指定して **SQLSetStmtOption** を呼び出した場合、関数は SQLSTATE が 01S02 (オプション値が変更されました) の SQL_SUCCESS_WITH_INFO を返します。 ドライバーは、サポートされていないすべてのカーソルモードを SQL_CURSOR_STATIC に設定します。  
  
 カーソルの種類と **SQLSetStmtOption**の詳細については、 [ODBC プログラマーズリファレンス](../../odbc/reference/odbc-programmer-s-reference.md)を参照してください。  
  
## <a name="block-cursor"></a>ブロック カーソル (block cursor)  
 クライアントに返される前方スクロール、読み取り専用の結果セット。データのストレージを管理します。  
  
## <a name="static-cursor"></a>静的カーソル (static cursor)  
 クエリで定義されたデータセットのスナップショット。 静的カーソルには、他のユーザーによって基になるデータのリアルタイムの変更が反映されません。 カーソルのメモリバッファーは ODBC カーソルライブラリによって管理されます。これにより、前方および後方スクロールが可能になります。  
  
## <a name="rowset"></a>行セット (rowset)  
 カーソルに格納されているデータのブロック。データソースから取得した行を表します。
