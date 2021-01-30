---
description: SQLRowCount (カーソル ライブラリ)
title: SQLRowCount (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a8efc6fdef2a3bef563a5289acdef55958a03be
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202673"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLRowCount** 関数の使用について説明します。 **SQLRowCount** の一般的な情報については、「 [SQLRowCount 関数](../../../odbc/reference/syntax/sqlrowcount-function.md)」を参照してください。  
  
 アプリケーションが、カーソルに関連付けられているステートメントを使用して **SQLRowCount** を呼び出すと、カーソルライブラリは、ドライバーから取得したデータの行の数を返します。  
  
 アプリケーションが、位置指定の update または delete ステートメントに関連付けられたステートメントを使用して **SQLRowCount** を呼び出すと、カーソルライブラリは、ステートメントの影響を受けた行数を返します。  
  
 アプリケーションが **SELECT** ステートメントの後に **SQLRowCount** を呼び出すと、カーソルライブラリは-1 を返します。
