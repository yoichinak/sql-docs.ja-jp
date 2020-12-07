---
description: ドライバー マネージャーの機能
title: ドライバーマネージャーの機能Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 399dec39e18c9e31ce4a93172d0597c333fb40cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386168"
---
# <a name="what-the-driver-manager-does"></a>ドライバー マネージャーの機能
次の表は、ODBC 2.x *Driver Manager* が odbc *2.x および odbc* *3.x ドライバーへ* の呼び出しをどのようにマップするかをまとめたものです。  
  
|関数または<br /><br /> statement 属性|コメント|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|**Sqlfetchscroll**で使用するブックマークをポイントします。 実装の詳細は次のとおりです。<br /><br /> -ODBC 2.x ドライバーでアプリケーションがこれを設定すると *、odbc* *3.x ドライバーマネージャー*によってキャッシュされます。 このメソッドはポインターを逆参照し、 **Sqlfetchscroll**が後でアプリケーションによって呼び出されたときに、 **SQLExtendedFetch**の*FETCHOFFSET*引数内*の ODBC 2.x*ドライバーに値を渡します。<br />-ODBC *3. x* ドライバーでアプリケーションがこれを設定すると *、Odbc 3.x* ドライバーマネージャーがドライバーに呼び出しを渡します。|  
|SQL_ATTR_ROW_STATUS_PTR|**Sqlfetch**、 **sqlfetchscroll**、 **sqlbulkoperations**、 **SQLSetPos**によって入力された行ステータス配列を指します。 実装の詳細は次のとおりです。<br /><br /> -ODBC 2.x*ドライバーで*アプリケーションがこれを設定すると、odbc *3.x ドライバーマネージャー*によってその値がキャッシュされます。 この値は、 **Sqlfetchscroll**または**sqlfetch**が呼び出されたときに、 **SQLExtendedFetch**の*rowstatusarray*引数*の ODBC 2.x*ドライバーに渡されます。<br />-ODBC *3. x* ドライバーでアプリケーションがこれを設定すると *、Odbc 3.x* ドライバーマネージャーがドライバーに呼び出しを渡します。<br />-状態 S6 で、アプリケーションが SQL_ATTR_ROW_STATUS_PTR を設定してから、最初に**Sqlfetch**または**sqlbulkoperations**を呼び出さずに**sqlbulkoperations** (*操作*SQL_ADD) または**SQLSetPos**を呼び出すと、SQLSTATE HY011 (属性を設定することはできません) が返されます。|  
|SQL_ATTR_ROWS_FETCHED_PTR|**Sqlfetch**および**sqlfetchscroll**がフェッチされた行の数を返すバッファーを指します。 実装の詳細は次のとおりです。<br /><br /> -ODBC 2.x*ドライバーで*アプリケーションがこれを設定すると、odbc *3.x ドライバーマネージャー*によってその値がキャッシュされます。 この値は、 **sqlfetch**または**sqlfetchscroll**がアプリケーションによって呼び出されたときに、 **SQLExtendedFetch**の*rowcountptr*引数の ODBC *2.x ドライバーに*渡されます。<br />-ODBC *3. x* ドライバーでアプリケーションがこれを設定すると *、Odbc 3.x* ドライバーマネージャーがドライバーに呼び出しを渡します。|  
|SQL_ATTR_ROW_ARRAY_SIZE|行セットのサイズを設定します。 実装の詳細は次のとおりです。<br /><br /> -アプリケーションが ODBC 2.x*ドライバーで*これを設定すると、odbc *3.x ドライバーマネージャー*は、それを SQL_ROWSET_SIZE statement 属性にマップします。<br />-ODBC *3. x* ドライバーでアプリケーションがこれを設定すると *、Odbc 3.x* ドライバーマネージャーがドライバーに呼び出しを渡します。<br />-ODBC 3.x ドライバーを使用しているアプリケーションが**SQLSetScrollOptions**を呼び出すと、基になるドライバーが**SQLSetScrollOptions**をサポートしていない場合、SQL_ROWSET_SIZE は*RowsetSize*引数の値に設定さ*れます。*|  
|SQL_ROWSET_SIZE|ODBC 2.x アプリケーションによって**SQLExtendedFetch**が呼び出されたときに、 **SQLExtendedFetch**によって使用される行セットのサイズを設定*します。* 実装の詳細は次のとおりです。<br /><br /> -アプリケーションがこれを設定すると、ドライバーのバージョンに関係なく、ODBC *3. x* ドライバーマネージャーがドライバーに呼び出しを渡します。<br />-ODBC 2.x ドライバーを使用しているアプリケーションが**SQLSetScrollOptions**を呼び出すと、SQL_ROWSET_SIZE が**RowsetSize**引数の値に設定さ*れます。*|  
|**SQLBulkOperations**|ブックマーク操作による挿入操作、または更新、削除、またはフェッチを実行します。 実装の詳細は次のとおりです。<br /><br /> -アプリケーションが ODBC 2.x ドライバーで SQL_ADD 操作を使用して**Sqlbulkoperations**を呼び出すと、odbc *3.x ドライバーマネージャー*は、SQL_ADD*操作*を使用して、その操作を**SQLSetPos**にマップ*します。* *Operation*<br />-SQL_ADD*操作*による**sqlsetpos**をサポートしていない odbc 2.x ドライバーを使用している場合 *、odbc* 3.x ドライバーマネージャーでは、SQL_ADD 操作によって*Operation* **Sqlsetpos**が SQL_ADD*操作*によって**sqlbulkoperations**にマップされることはありません。 *2.x* これは、 **Sqlbulkoperations** を state S7 で呼び出すことができないためです *。 ODBC 2.x では、* **SQLSetPos** を呼び出すことができませんでした。<br />- **Sqlbulkoperations**を呼び出す前に、アプリケーションが odbc 2.x ドライバーで SQL_ADD*操作*を使用して**sqlbulkoperations**を呼び出した場合 *、odbc* *3.x ドライバーマネージャー*はエラーを返します。|  
|**SQLExtendedFetch**|指定された行セットを返します。 上記の制限を除き *、ODBC 3.X* ドライバーマネージャーは、ドライバーのバージョンに関係なく、 **SQLExtendedFetch** の呼び出しをドライバーに渡します。|  
|**SQLFetch**|次の行セットを返します。 実装の詳細は次のとおりです。<br /><br /> -アプリケーションが ODBC 2.x ドライバーで**Sqlfetch**を呼び出すと、odbc *3.x ドライバーマネージャー*がそれを**SQLExtendedFetch**にマップし*ます。* **SQLExtendedFetch**の*fetchorientation*引数が SQL_FETCH_NEXT に設定されています。 ドライバーマネージャーは、 *Rowstatusarray* 引数の SQL_ATTR_ROW_STATUS_PTR statement 属性のキャッシュされた値と、 *rowstatusarray* 引数の SQL_ATTR_ROWS_FETCHED_PTR statement 属性のキャッシュされた値を使用します。<br />- *Odbc 2.x アプリケーションで*は *、odbc* *2.x ドライバー*で**sqlfetch**と**sqlfetchscroll**の呼び出しを混在させることができます。これは、アプリケーション*が Odbc 2.x*ドライバーで sqlfetch を呼び出したときに**sqlfetch**が**SQLExtendedFetch**にマップされるためです。<br />-ODBC 2.x ドライバーで**SQLExtendedFetch**がサポートされていない場合、アプリケーションがそのドライバーで**Sqlfetch**または**sqlfetchscroll**を呼び出すと、odbc *3.x ドライバーマネージャー*は**SQLExtendedFetch**にマップしませ*ん。* アプリケーションで SQL_ATTR_ROW_ARRAY_SIZE を1より大きい値に設定しようとすると、SQLSTATE HYC00 (省略可能な機能が実装されていません) が返されます。<br />-記載されている制限を除けば、ドライバーのバージョンに関係なく、ODBC *3. x* ドライバーマネージャーは **sqlfetch** への呼び出しをドライバーに渡します。|  
|**SQLFetchScroll**|指定された行セットを返します。 実装の詳細は次のとおりです。<br /><br /> -アプリケーション*が odbc 2.x*ドライバーで**sqlfetchscroll**を呼び出すと、odbc 3.x ドライバーマネージャーがそれを**SQLExtendedFetch**にマップし*ます。* *Rowstatusarray*引数の SQL_ATTR_ROW_STATUS_PTR statement 属性のキャッシュされた値と、 *rowstatusarray*引数の SQL_ATTR_ROWS_FETCHED_PTR statement 属性のキャッシュされた値を使用します。 **Sqlfetchscroll**の*fetchorientation*引数が SQL_FETCH_BOOKMARK 場合、 *fetchorientation*引数には SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性のキャッシュされた値が使用され、 **sqlfetchscroll**の*fetchorientation*引数が0でない場合はエラーが返されます。<br />-アプリケーションが ODBC *3. x*ドライバーでこれを呼び出すと、odbc 3.X ドライバーマネージャーがドライバーに呼び出しを*渡します。*|  
|**SQLSetPos**|さまざまな位置指定操作を実行します。 ODBC 3.x ドライバーマネージャーは、ドライバーのバージョンに関係なく、 **SQLSetPos**の呼び出しをドライバーに渡し*ます。*|  
|**SQLSetScrollOptions**|ドライバーマネージャーが、 **SQLSetScrollOptions**をサポートしていない ODBC 3.x ドライバーを使用しているアプリケーションの**SQLSetScrollOptions**をマップする場合、ドライバーマネージャーは、 **SQLSetScrollOption**の*RowsetSize*引数に、ステートメントの SQL_ATTR_ROW_ARRAY_SIZE の属性ではなく SQL_ROWSET_SIZE ステートメントオプションを設定*します。* 結果として、 **Sqlfetch**または**sqlfetchscroll**の呼び出しによって複数の行をフェッチするときに、アプリケーションで**SQLSetScrollOptions**を使用することはできません。 **SQLExtendedFetch**の呼び出しによって複数の行をフェッチする場合にのみ使用できます。|
