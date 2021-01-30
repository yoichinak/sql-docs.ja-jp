---
description: SQLSetPos (カーソル ライブラリ)
title: SQLSetPos (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf97529f4fd411581738459accffc805a444a8ea
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202617"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリで **SQLSetPos** 関数を使用する方法について説明します。 **Sqlsetpos** に関する一般的な情報については、「 [sqlsetpos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。  
  
 カーソルライブラリでは、 **SQLSetPos** の *operation* 引数に対してのみ SQL_POSITION 操作がサポートされています。 SQL_LOCK_NO_CHANGE 値は、 *LockType* 引数に対してのみサポートされます。  
  
 ドライバーで一括操作がサポートされていない場合は、 **SQLSetPos** が 0 *に等しい値とし* て呼び出されたときに、カーソルライブラリが SQLSTATE HYC00 (ドライバーに対応していません) を返します。 このドライバーの動作はお勧めしません。  
  
 カーソルライブラリでは、 **SQLSetPos** の呼び出しで SQL_UPDATE および SQL_DELETE 操作はサポートされていません。 カーソルライブラリは、WHERE 句を使用して、検索された update または delete ステートメントを作成することによって、位置指定の update または delete SQL ステートメントを実装します。これにより、各バインド列のキャッシュに格納されている値を列挙します。 詳細については、「 [位置指定更新と Delete ステートメントの処理](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)」を参照してください。  
  
 ドライバーで静的カーソルがサポートされていない場合、カーソルライブラリを操作するアプリケーションは、 **Sqlfetch** ではなく、 **SQLExtendedFetch** または **sqlfetchscroll** によってフェッチされた行セットで **SQLSetPos** のみを呼び出す必要があります。 カーソルライブラリでは、ドライバーで **Sqlfetch** (行セットサイズが 1) を繰り返し呼び出すことで、 **SQLExtendedFetch** と **sqlfetchscroll** が実装されています。 カーソルライブラリは、 **Sqlfetch** の呼び出しをドライバーに渡します。 ドライバーが静的カーソルをサポートしていないときに **Sqlfetch** によってフェッチされた複数行の行セットで **sqlsetpos** が呼び出された場合、 **sqlsetpos** は順方向専用カーソルでは動作しないため、呼び出しは失敗します。 これは、アプリケーションが SQL_ATTR_CURSOR_TYPE を SQL_CURSOR_STATIC に設定するために **SQLSetStmtAttr** を正常に呼び出した場合にも発生します。これは、ドライバーが静的カーソルをサポートしていない場合でも、カーソルライブラリでサポートされます。
