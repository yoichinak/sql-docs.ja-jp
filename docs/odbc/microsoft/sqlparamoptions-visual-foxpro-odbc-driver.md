---
description: SQLParamOptions (Visual FoxPro ODBC ドライバー)
title: SQLParamOptions (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e40af7f0bb03c0b5245717880e67e72b38559aed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500195"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 完全  
  
 ODBC API の準拠: レベル1  
  
 アプリケーションで、 [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)によって割り当てられた一連のパラメーターに対して複数の値を指定できるようにします。 一連のパラメーターに複数の値を指定する機能は、一括挿入や、データソースがさまざまなパラメーター値を使用して同じ SQL ステートメントを複数回処理する必要があるその他の作業に役立ちます。 たとえば、アプリケーションでは、 **insert** ステートメントに関連付けられた一連のパラメーターに対して3つの値のセットを指定し、insert ステートメントを1回 **実行して** 3 つの挿入操作を実行できます。  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [sqlparamoptions](../../odbc/reference/syntax/sqlparamoptions-function.md) 」を参照してください。
