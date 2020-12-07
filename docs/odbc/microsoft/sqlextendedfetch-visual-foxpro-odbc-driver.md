---
description: SQLExtendedFetch (Visual FoxPro ODBC ドライバー)
title: SQLExtendedFetch (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f938dda4e9e474854d62c50401ee0bf91317983
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449174"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル2  
  
 [Sqlfetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)に似ていますが、各列に配列を使用して複数の行を返します。 結果セットは順方向スクロール可能であり、カーソルが順方向専用ではなく静的に定義されている場合は、後方スクロール可能にすることができます。  
  
 既定では、Visual FoxPro ODBC ドライバーは、FoxPro テーブルで削除済みとマークされた行を返しません。 削除対象としてマークされている行は、テーブルからまだ削除されていないため、結果セットのカーソルには含まれません。 この動作は、[ [削除の設定](../../odbc/microsoft/set-deleted-command.md) ] コマンドを使用して変更できます。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 」を参照してください。
