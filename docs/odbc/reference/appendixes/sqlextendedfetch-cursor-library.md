---
description: SQLExtendedFetch (カーソル ライブラリ)
title: SQLExtendedFetch (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 266d408b765ce5025a7f275c87cc6b548e6e49bb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202870"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLExtendedFetch** 関数の使用について説明します。 **SQLExtendedFetch** の一般的な情報については、「 [SQLExtendedFetch 関数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)」を参照してください。  
  
 カーソルライブラリは、ドライバーで **Sqlfetch** を繰り返し呼び出すことによって、 **SQLExtendedFetch** を実装します。  
  
 カーソルライブラリでは、SQL_FETCH_BOOKMARK の *Fetchorientation* を使用した **SQLExtendedFetch** の呼び出しをサポートしています。  
  
 カーソルライブラリを使用する場合、 **SQLExtendedFetch** の呼び出しと **sqlfetchscroll** または **sqlfetch** の呼び出しを混在させることはできません。
