---
description: ODBC 3.x アプリケーション用のブロック カーソル、スクロール可能なカーソル、および下位互換性
title: ブロックとスクロール可能なカーソルの ODBC 3. x の互換性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96645f91d52f4141aacf4f2e171ef809a639f73c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476834"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x アプリケーション用のブロック カーソル、スクロール可能なカーソル、および下位互換性
**Sqlfetchscroll**と**SQLExtendedFetch**の両方が存在する場合は、アプリケーションプログラミングインターフェイス (API) と、アプリケーションが呼び出す一連の関数、およびドライバーが実装する関数のセットである SERVICE Provider Interface (SPI) との間の、ODBC での最初の clear split を表します。 この分割は、 **Sqlfetchscroll**を使用して標準に準拠し、 **SQLExtendedFetch***を使用する odbc 2.X*と互換性が*ある odbc 3.x*の要件とのバランスを取るために必要です。  
  
 ODBC 3.x API は、アプリケーションが呼び出す関数のセットであり、 **Sqlfetchscroll**および関連するステートメント属性が含まれてい*ます。* ODBC 3.x はドライバーが実装する関数のセットであり、 **Sqlfetchscroll**、 **SQLExtendedFetch**、および関連するステートメント属性が含まれて*います。* ODBC では API と SPI の間にこの分割が正式に適用されないため、ODBC 3.x アプリケーションは**SQLExtendedFetch**および関連するステートメント属性を呼び出すことが*できます。* ただし、これを行うの *は ODBC 3.x* アプリケーションではありません。 Api と Spi の詳細については、「 [ODBC アーキテクチャ](../../../odbc/reference/odbc-architecture.md)の概要」を参照してください。  
  
 Odbc *3.x ドライバーマネージャー* が odbc *2.x および odbc* *3.x ドライバーへ* の呼び出しをマップする方法、および odbc *3.x ドライバーが* ブロックおよびスクロール可能なカーソルに対して実装する必要がある関数とステートメントの属性の詳細については、「付録 G: ドライバーの旧バージョン [と](../../../odbc/reference/appendixes/what-the-driver-does.md) の互換性のためのガイドライン」を参照してください。  
  
 次の表は、ODBC *3. x* アプリケーションで使用する必要がある関数とステートメントの属性と、ブロックカーソルおよびスクロール可能なカーソルをまとめたものです。 また *、odbc 2.x アプリケーションが* *odbc 2.x ドライバーと*互換性があることを認識している必要が*ある、odbc 2.x と odbc* *3. x*の間の変更についても示します。  
  
|関数または<br /><br /> statement 属性|コメント|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|**Sqlfetchscroll**で使用するブックマークをポイントします。<br /><br /> アプリケーションが ODBC 2.x ドライバーでこれを設定する場合、これは固定長のブックマークを指す必要が*あります。*|  
|SQL_ATTR_ROW_STATUS_PTR|**Sqlfetch**、 **sqlfetchscroll**、 **sqlbulkoperations**、 **SQLSetPos**によって入力された行ステータス配列を指します。<br /><br /> アプリケーション*が ODBC 2.x*ドライバーでこれを設定し、 **sqlbulkoperation**、 **Sqlfetch**、または**SQLExtendedFetch**を呼び出す前に SQL_ADD*操作*で**Sqlbulkoperation**を呼び出すと、SQLSTATE HY011 (属性を設定することはできません) が返されます。<br /><br /> アプリケーション*が ODBC 2.x*ドライバーで**sqlfetch**を呼び出すと、 **sqlfetch**は**SQLExtendedFetch**にマップされるため、この配列の値が返されます。|  
|SQL_ATTR_ROWS_FETCHED_PTR|**Sqlfetch**および**sqlfetchscroll**がフェッチされた行の数を返すバッファーを指します。<br /><br /> アプリケーション*が ODBC 2.x*ドライバーで**sqlfetch**を呼び出すと、 **sqlfetch**は**SQLExtendedFetch**にマップされるため、このバッファーには値が返されます。|  
|SQL_ATTR_ROW_ARRAY_SIZE|行セットのサイズを設定します。<br /><br /> アプリケーションが ODBC *2.x ドライバーで*SQL_ADD 操作を使用して**sqlbulkoperations**を呼び出した場合、SQL_ATTR_ROW_ARRAY_SIZE ではなく、呼び出しに対して SQL_ROWSET_SIZE が使用されます。これは、SQL_ROWSET_SIZE を使用する SQL_ADD の*操作*で、呼び出しが**SQLSetPos**にマップされるためです。 *Operation*<br /><br /> ODBC 2.x ドライバーで SQL_ADD または**SQLExtendedFetch**の*操作*を使用して**SQLSetPos**を呼び出すと、SQL_ROWSET_SIZE が使用され*ます。*<br /><br /> ODBC 2.x ドライバーで**Sqlfetch**または**sqlfetchscroll**を呼び出すと、SQL_ATTR_ROW_ARRAY_SIZE が使用され*ます。*|  
|**SQLBulkOperations**|挿入操作とブックマーク操作を実行します。 SQL_ADD 操作を伴う**Sqlbulkoperations**が ODBC 2.x ドライバーで呼び出されると、SQL_ADD の*操作*によって**SQLSetPos**にマップさ*れます。* *Operation* 実装の詳細は次のとおりです。<br /><br /> -ODBC 2.x ドライバーを使用する場合、アプリケーションでは、 *StatementHandle*に関連付けられている、暗黙的に割り当てられたもののみを使用する必要が*あります。* 明示的な記述子操作は ODBC *2.x ドライバーで*はサポートされていないため、行を追加するために別のを割り当てることはできません。 アプリケーションでは、 **SQLSetDescField**または**SQLSetDescRec**ではなく、 **SQLBindCol**を使用して、にバインドする必要があります。<br />-ODBC 3.x ドライバーを呼び出す場合、アプリケーションは、 **Sqlfetch**または**sqlbulkoperations**を呼び出す前に、SQL_ADD 操作を使用して**sqlbulkoperations**を呼び出すことが*できます。* *Operation* ODBC 2.x ドライバーを呼び出すときに、アプリケーションは**Sqlfetchscroll**を呼び出してから、SQL_ADD 操作で**sqlfetchscroll**を呼び出す必要が*あります。*|  
|**SQLFetch**|次の行セットを返します。 実装の詳細は次のとおりです。<br /><br /> -アプリケーション*が ODBC 2.x*ドライバーで**sqlfetch**を呼び出すと、 **SQLExtendedFetch**にマップされます。<br />-アプリケーションが ODBC *3. x*ドライバーで**sqlfetch**を呼び出すと、SQL_ATTR_ROW_ARRAY_SIZE statement 属性で指定された行数が返されます。|  
|**SQLFetchScroll**|指定された行セットを返します。 実装の詳細は次のとおりです。<br /><br /> -アプリケーション*が ODBC 2.x*ドライバーで**sqlfetchscroll**を呼び出すと、1つの行に適用される各エラーの前に SQLSTATE 01S01 (行のエラー) が返されます。 これが行われるのは、ODBC *3.X ドライバーマネージャー* がこれを **SQLExtendedFetch** にマップし、 **SQLExtendedFetch** がこの SQLSTATE を返すためです。 アプリケーションが ODBC *3. x*ドライバーで**sqlfetchscroll**を呼び出すと、SQLSTATE 01S01 (行内のエラー) は返されません。<br />- *Fetchorientation*が SQL_FETCH_BOOKMARK に設定*された ODBC 2.x*ドライバーでアプリケーションが**sqlfetchscroll**を呼び出した場合、 *fetchoffset*引数を0に設定する必要があります。 ODBC 2.x ドライバーでオフセットベースのブックマークフェッチを *実行しよう* とすると、SQLSTATE HYC00 (省略可能な機能が実装されていません) が返されます。|  
  
> [!NOTE]  
>  ODBC *3.x* アプリケーションでは、 **SQLExtendedFetch** または SQL_ROWSET_SIZE statement 属性を使用しないでください。 代わりに、 **Sqlfetchscroll** と SQL_ATTR_ROW_ARRAY_SIZE statement 属性を使用する必要があります。 ODBC *3. x*アプリケーションでは、SQL_ADD*操作*で**SQLSetPos**を使用することはできませんが、SQL_ADD 操作で**sqlbulkoperations**を使用する必要があります。 *Operation*
