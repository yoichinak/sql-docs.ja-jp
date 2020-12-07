---
description: SQLExecDirect (Visual FoxPro ODBC ドライバー)
title: SQLExecDirect (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d12218097caf6d4a2c4a0375f1a8e9542b2ccf59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449184"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: コアレベル  
  
 新しい [準備可能 SQL ステートメント](../../odbc/microsoft/visual-foxpro-terminology.md)を実行します。 ステートメントにパラメーターが存在する場合、Visual FoxPro ODBC ドライバーはパラメーターマーカー変数の現在の値を使用します。  
  
 一度に複数の SQL ステートメントを送信するバッチコマンドを作成するには、セミコロン;) () を使用します。バッチ内の各 SQL ステートメントを分離する場合はです。  
  
 テーブル、ビュー、またはフィールドの名前にスペースが含まれている場合は、名前を後方引用符で囲みます。 たとえば、データベースに My Table という名前のテーブルとフィールド My Field が含まれている場合は、識別子の各要素を次のように囲みます。  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 」を参照してください。
