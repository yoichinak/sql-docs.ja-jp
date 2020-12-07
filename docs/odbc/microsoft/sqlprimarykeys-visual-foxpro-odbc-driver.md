---
description: SQLPrimaryKeys (Visual FoxPro ODBC ドライバー)
title: SQLPrimaryKeys (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b333e10c7000a8a44e957e33d0c84a3b004f43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483345"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル2  
  
 テーブルの主キーを構成する列名を返します。 Visual FoxPro ODBC ドライバーによる **Sqlprimarykeys** の実装は、次のように動作します。  
  
-   *Sztableowner*引数と*cbtableowner*引数は無視されます。  
  
-   [データベース](../../odbc/microsoft/visual-foxpro-terminology.md)であるデータソースに対してのみ機能します。 データソースが [フリーテーブル](../../odbc/microsoft/visual-foxpro-terminology.md)のディレクトリの場合、ドライバーは "ドライバーはこの機能をサポートしていません" というエラーを返します。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [sqlprimarykeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 」を参照してください。
