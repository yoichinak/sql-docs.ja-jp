---
description: SQLSpecialColumns (Visual FoxPro ODBC ドライバー)
title: Sql特殊列 (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e83568c8370b56decb7c3f7c90cda443b88a72a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421606"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル1  
  
 テーブル内の行を一意に識別する最適な列のセットを取得します。  
  
 Visual FoxPro ODBC ドライバーは、FoxPro テーブルの主キーを構成する列を返します。 (「 [Sqlprimarykeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)」を参照してください)。 *Fcoltype* を SQL_ROWVER に設定して呼び出された場合、列は返されません。 **Sql特殊列** は、 [データベース](../../odbc/microsoft/visual-foxpro-terminology.md)であるデータソースに対してのみ機能します。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [sqlの列](../../odbc/reference/syntax/sqlspecialcolumns-function.md)」を参照してください。
