---
description: SQLBindCol (カーソル ライブラリ)
title: SQLBindCol (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3b3968687f1c9062457a16ec7c5bc11cb32d3a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456481"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLBindCol** 関数の使用について説明します。 **SQLBindCol**の一般的な情報については、「 [SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)」を参照してください。  
  
 アプリケーションでは、現在の行セットを返すために、カーソルライブラリの1つ以上のバッファーを割り当てます。 **SQLBindCol**を1回以上呼び出して、これらのバッファーを結果セットにバインドします。  
  
 アプリケーションで **SQLBindCol** を呼び出して、バインドされた列の C データ型、列サイズ、および10進数が同じである限り、 **SQLExtendedFetch**、 **Sqlfetch**、または **sqlfetchscroll**を呼び出した後に結果セット列を再バインドすることができます。 アプリケーションでは、別のアドレスに列を再バインドするためにカーソルを閉じる必要はありません。  
  
 カーソルライブラリでは、バインドオフセットを使用するための SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性の設定がサポートされています。 この再バインドを実行するには、**SQLBindCol** を呼び出す必要はありません。カーソルライブラリが ODBC *3. x* ドライバーで使用されている場合、 **sqlfetch** が呼び出されるときにバインドオフセットは使用されません。 バインドオフセットは、カーソルライブラリ*が ODBC 2.x*ドライバーで使用されているときに sqlfetch が呼び出され**た場合に**使用されます。これは、 **sqlfetch**が**SQLExtendedFetch**にマップされるためです。  
  
 カーソルライブラリでは、ブックマーク列をバインドするための **SQLBindCol** の呼び出しをサポートしています。  
  
 ODBC 2.x ドライバーを使用する場合、カーソルライブラリは SQLSTATE HY090 (無効な文字列またはバッファー長) を返します。 **SQLBindCol**を呼び出すと、ブックマーク列のバッファー長が4に等しくない値に設定さ*れます。* ODBC 3.x ドライバーを使用する場合、カーソルライブラリを使用すると、バッファーを任意のサイズにすることができ*ます。*
