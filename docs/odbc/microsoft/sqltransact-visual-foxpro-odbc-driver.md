---
description: SQLTransact (Visual FoxPro ODBC ドライバー)
title: SQLTransact (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1deed379c456ba2f15d30b6783c95d657e688457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500115"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: コアレベル  
  
 接続に関連付けられているすべてのステートメントハンドル (*hstmt*s) のすべてのアクティブな操作、または環境ハンドル *henv*に関連付けられているすべての接続に対して、コミットまたはロールバックの操作を要求します。 **Sqltransact** は、 [データベース](../../odbc/microsoft/visual-foxpro-terminology.md)であるデータソースに対してのみ機能します。  
  
 手動モードでコミットが失敗した場合、トランザクションはアクティブのままです。トランザクションをロールバックするか、コミット操作を再試行するかを選択できます。 自動トランザクションモードでコミット操作が失敗した場合、トランザクションは自動的にロールバックされます。トランザクションを非アクティブにすることはできません。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [sqltransact](../../odbc/reference/syntax/sqltransact-function.md) 」を参照してください。
