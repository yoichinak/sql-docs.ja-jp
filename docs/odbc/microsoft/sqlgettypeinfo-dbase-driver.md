---
description: SQLGetTypeInfo (dBASE ドライバー)
title: SQLGetTypeInfo (dBASE ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c94bca8dbc8413f6a3b8fdffed61f9ecd15f78e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339968"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (dBASE ドライバー)
> [!NOTE]  
>  このトピックでは、dBASE ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 **SQLGetTypeInfo**によって生成されるテーブルに返される型の名前 (TYPE_NAME) は、データソースで最もよく使用される名前になります。  
  
 SQL_ALL_EXCEPT_LIKE は、Byte、Counter、Double、Single、Long、Short の各データ型の検索可能な列に返されます。 (LIKE 機能は、ODBC 正規変換関数を使用して値を文字に変換してから、比較を実行することで実現できます)。
