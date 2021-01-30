---
description: SQLGetFunctions (カーソル ライブラリ)
title: SQLGetFunctions (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9414aa4d2be551ab3b6a44193f6b6c17e2deb145
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202763"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリで **Sqlgetfunctions** 関数を使用する方法について説明します。 **Sqlgetfunctions** に関する一般的な情報については、「 [Sqlgetfunctions 関数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)」を参照してください。  
  
 **Sqlgetfunctions** を呼び出すと、カーソルライブラリは、ドライバーでサポートされている関数に加えて、 **SQLExtendedFetch**、 **sqlgetfunctions**、 **SQLSetPos**、および **SQLSetScrollOptions** をサポートしていることを返します。
