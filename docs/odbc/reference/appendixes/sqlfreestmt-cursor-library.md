---
description: SQLFreeStmt (カーソル ライブラリ)
title: SQLFreeStmt (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b7ebdcfc5a9997efb4301852b1aae3c1408464d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202815"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLFreeStmt** 関数の使用について説明します。 **SQLFreeStmt** の一般的な情報については、「 [SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)」を参照してください。  
  
 アプリケーションが、 **SQLExtendedFetch**、 **sqlfetch**、または **sqlfetchscroll** を呼び出した後に SQL_UNBIND オプションを使用して **SQLFreeStmt** を呼び出すと、カーソルライブラリはエラーを返します。 結果セットの列のバインドを解除する前に、アプリケーションは SQL_CLOSE オプションを指定して **Sqlcloの** または **SQLFreeStmt** を呼び出す必要があります。
