---
description: SQLSetScrollOptions (カーソル ライブラリ)
title: SQLSetScrollOptions (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eaba3884e90883cded418acc46d73cc1c0dfba88
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202608"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLSetScrollOptions** 関数の使用について説明します。 **SQLSetScrollOptions** の一般的な情報については、「 [SQLSetScrollOptions 関数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)」を参照してください。  
  
 カーソルライブラリでは、旧バージョンとの互換性のためだけに **SQLSetScrollOptions** をサポートしています。アプリケーションでは、代わりに SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、および SQL_ATTR_ROW_ARRAY_SIZE ステートメントの属性を使用する必要があります。
