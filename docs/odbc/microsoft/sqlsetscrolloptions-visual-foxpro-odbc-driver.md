---
description: SQLSetScrollOptions (Visual FoxPro ODBC ドライバー)
title: SQLSetScrollOptions (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0e7cecfb0ce7640575cb69f1e84e805a884b57b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421636"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 部分的  
  
 ODBC API の準拠: レベル2  
  
 ステートメントハンドルの *hstmt*に関連付けられているカーソルの動作を制御するオプションを設定します。  
  
 Visual FoxPro ODBC ドライバーでは、SQL_CONCUR_READ_ONLY のみがサポートされます。 *Fconcurrency* 値 SQL_CONCUR_ROWVER はサポートされていません。 ドライバーは、SQL_KEYSET_SIZE、SQL_CURSOR_DYNAMIC、および SQL_CURSOR_KEYSET_DRIVEN を警告 ODBC_01S02 と共に SQL_SCROLL_STATIC に変換します。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 」を参照してください。
