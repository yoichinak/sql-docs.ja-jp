---
description: SQLSetDescField および SQLSetDescRec (カーソル ライブラリ)
title: SQLSetDescField および SQLSetDescRec (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cef4967a81a78e08dee733072359459c864b9627
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476944"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField および SQLSetDescRec (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLSetDescField** 関数と **SQLSetDescRec** 関数の使用について説明します。 これらの関数の一般的な情報については、「 [SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md) と [SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)」を参照してください。  
  
 カーソルライブラリは、ブックマーク列に対して設定されたフィールドの値を返すために呼び出されると、 **SQLSetDescField** を実行します。  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 カーソルライブラリは、ブックマーク列に対して **SQLSetDescRec** への呼び出しを実行します。  
  
 ODBC 2.x ドライバーを使用する場合、カーソルライブラリは SQLSTATE HY090 (無効な文字列またはバッファー長) を返します。 **SQLSetDescField**または**SQLSetDescRec**を呼び出すと、のブックマークレコードの SQL_DESC_OCTET_LENGTH フィールドが4に等しくない値に設定さ*れます。* ODBC 3.x ドライバーを使用する場合、カーソルライブラリを使用すると、バッファーを任意のサイズにすることができ*ます。*  
  
 カーソルライブラリは、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE、または SQL_DESC_ROW_STATUS_PTR の各フィールドの値を返すために呼び出されると、 **SQLSetDescField** を実行します。 これらのフィールドは、ブックマーク行だけでなく、任意の行に対して返すことができます。  
  
 カーソルライブラリは、前に説明したフィールド以外の記述子フィールドを変更するために **SQLSetDescField** を実行しません。 カーソルライブラリの読み込み中に、アプリケーションが **SQLSetDescField** を呼び出して他のフィールドを設定すると、その呼び出しはドライバーに渡されます。  
  
 カーソルライブラリでは、アプリケーションの行記述子の任意の行の SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドを動的に変更できます ( **SQLExtendedFetch**、 **sqlfetch**、または **sqlfetchscroll**を呼び出した後)。 SQL_DESC_OCTET_LENGTH_PTR フィールドは、列の長さバッファーのバインドを解除するためにのみ null ポインターに変更できます。  
  
 カーソルライブラリでは、カーソルが開いているときに APD 内の SQL_DESC_BIND_TYPE フィールドを変更することはサポートされていません。 SQL_DESC_BIND_TYPE フィールドは、カーソルが閉じられてから新しいカーソルが開かれるまでの間のみ変更できます。 カーソルが開いているときにカーソルライブラリが変更できる記述子フィールドは、SQL_DESC_ARRAY_STATUS_PTR、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR、および SQL_DESC_ROWS_PROCESSED_PTR だけです。  
  
 カーソルライブラリでは、 **SQLExtendedFetch** または **sqlfetchscroll** が呼び出された後、カーソルが閉じられる前に、そのフィールドの SQL_DESC_COUNT 変更がサポートされていません。
