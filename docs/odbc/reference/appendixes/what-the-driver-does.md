---
description: ドライバーの機能
title: ドライバーの機能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f15473d1eb0e6344fbd5772f2b28233c07aa7a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386228"
---
# <a name="what-the-driver-does"></a>ドライバーの機能
次の表は、ODBC *3.x ドライバーが* ブロックおよびスクロール可能なカーソルに対して実装する必要がある関数とステートメントの属性をまとめたものです。  
  
|関数または<br /><br /> statement 属性|コメント|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|**Sqlfetch**および**sqlfetchscroll**によって入力された行ステータス配列のアドレスを設定します。 この配列は、 **sqlsetpos**がステートメント状態 S6 で呼び出された場合に、 **sqlsetpos**によっても入力されます。 **SQLSetPos**が state S7 で呼び出された場合、この配列は塗りつぶされませんが、 **SQLExtendedFetch**の*rowstatusarray*引数によって示される配列は塗りつぶされます。 詳細については、「付録 B: ODBC 状態遷移テーブル」の「 [ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md) 」を参照してください。|  
|SQL_ATTR_ROWS_FETCHED_PTR|**Sqlfetch**および**sqlfetchscroll**がフェッチする行の数を返すバッファーのアドレスを設定します。 **SQLExtendedFetch**が呼び出された場合、このバッファーは入力されませんが、 *rowcountptr*引数はフェッチされた行の数を指します。|  
|SQL_ATTR_ROW_ARRAY_SIZE|**Sqlfetch**および**sqlfetchscroll**によって使用される行セットのサイズを設定します。|  
|SQL_ROWSET_SIZE|**SQLExtendedFetch**によって使用される行セットのサイズを設定します。 ODBC 3.x ドライバーは、 **SQLExtendedFetch**または**SQLSETPOS**を呼び出す odbc *2.x アプリケーションを*操作する場合に、これを実装し*ます*。|  
|**SQLBulkOperations**|ODBC 3.x ドライバーが、SQL_ADD の*操作*で**sqlsetpos**を使用*する odbc 2.x* *アプリケーションで*動作する必要がある場合、ドライバーは SQL_ADD*操作*を伴う**Sqlbulkoperations**に加えて、SQL_ADD の*操作*によって**sqlsetpos**をサポートする必要があります。|  
|**SQLExtendedFetch**|指定された行セットを返します。 ODBC 3.x ドライバーは、 **SQLExtendedFetch**または**SQLSETPOS**を呼び出す odbc *2.x アプリケーションを*操作する場合に、これを実装し*ます*。 実装の詳細は次のとおりです。<br /><br /> -ドライバーは、SQL_ROWSET_SIZE statement 属性の値から行セットのサイズを取得します。<br />-ドライバーは、SQL_ATTR_ROW_STATUS_PTR statement 属性ではなく、 *Rowstatusarray* 引数から行ステータス配列のアドレスを取得します。 **SQLExtendedFetch**の呼び出しの*rowstatusarray*引数を null ポインターにすることはできません。 (ODBC 3.x では *、SQL_ATTR_ROW_STATUS_PTR*statement 属性を null ポインターにすることができます)。<br />-ドライバーは、フェッチされた行のアドレスを *Rowcountptr* 引数から取得します。これは、SQL_ATTR_ROWS_FETCHED_PTR statement 属性ではありません。<br />-ドライバーは、 **SQLExtendedFetch**への呼び出しによって行がフェッチされている間にエラーが発生したことを示す SQLSTATE 01S01 (行のエラー) を返します。 ODBC 3.x ドライバーは、 **Sqlfetch**または**sqlfetchscroll**が呼び出されたときではなく、 **SQLExtendedFetch**が呼び出されたときに SQLSTATE 01S01 (行内のエラー) を返す必要があり*ます。* 旧バージョンとの互換性を維持するために、 **SQLExtendedFetch**によって SQLSTATE 01S01 (行内のエラー) が返された場合、ドライバーマネージャーは、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)の「状態レコードのシーケンス」セクションに記載されている規則に従って、エラーキューの状態レコードを注文しません。|  
|**SQLFetch**|次の行セットを返します。 実装の詳細は次のとおりです。<br /><br /> -ドライバーは、SQL_ATTR_ROW_ARRAY_SIZE statement 属性の値から行セットのサイズを取得します。<br />-ドライバーは、SQL_ATTR_ROW_STATUS_PTR statement 属性から行ステータス配列のアドレスを取得します。<br />-ドライバーは、フェッチされた行のアドレスを SQL_ATTR_ROWS_FETCHED_PTR statement 属性から取得します。<br />-アプリケーションは、 **Sqlfetchscroll** と **sqlfetch**の間の呼び出しを混在させることができます。<br />-   列0がバインドされている場合、 **Sqlfetch**はブックマークを返します。<br />-   **Sqlfetch** を呼び出して、複数の行を返すことができます。<br />-ドライバーは、 **Sqlfetch**の呼び出しによって行がフェッチされている間にエラーが発生したことを示す SQLSTATE 01S01 (行のエラー) を返しません。|  
|**SQLFetchScroll**|指定された行セットを返します。 実装の詳細は次のとおりです。<br /><br /> -ドライバーは、SQL_ATTR_ROW_ARRAY_SIZE statement 属性から行セットのサイズを取得します。<br />-ドライバーは、SQL_ATTR_ROW_STATUS_PTR statement 属性から行ステータス配列のアドレスを取得します。<br />-ドライバーは、フェッチされた行のアドレスを SQL_ATTR_ROWS_FETCHED_PTR statement 属性から取得します。<br />-アプリケーションは、 **Sqlfetchscroll** と **sqlfetch**の間の呼び出しを混在させることができます。<br />-ドライバーは、 **Sqlfetchscroll**への呼び出しによって行がフェッチされている間にエラーが発生したことを示す SQLSTATE 01S01 (行のエラー) を返しません。|  
|**SQLSetPos**|さまざまな位置指定操作を実行します。 実装の詳細は次のとおりです。<br /><br /> -ステートメントの状態 S6 または S7 で呼び出すことができます。 詳細については、「付録 B: ODBC 状態遷移テーブル」の「 [ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md) 」を参照してください。<br />-ステートメント状態 S5 または S6 で呼び出された場合、ドライバーは、SQL_ATTR_ROWS_FETCHED_PTR statement 属性から行セットサイズを取得し、SQL_ATTR_ROW_STATUS_PTR statement 属性から行ステータス配列のアドレスを取得します。<br />-このがステートメントの状態 S7 で呼び出された場合、ドライバーは、行セットのサイズを SQL_ROWSET_SIZE statement 属性から取得し、行の状態の配列の *Rowstatusarray* 引数から **SQLExtendedFetch**のアドレスを取得します。<br />-ドライバーは、S7 で関数が呼び出されたときに、 **SQLSetPos** への呼び出しによって行がフェッチされたときに、エラーが発生したことを示すために SQLSTATE 01S01 (行のエラー) のみを返します。 旧バージョンとの互換性を維持するために、 **SQLSetPos**によって SQLSTATE 01S01 (行内のエラー) が返された場合、ドライバーマネージャーは、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)の「状態レコードのシーケンス」セクションに記載されている規則に従って、エラーキューの状態レコードを注文しません。<br />-ドライバーが、SQL_ADD の*操作*引数を使用して**SQLSETPOS**を呼び出す ODBC 2.x アプリケーションで動作する必要がある場合、ドライバーは、SQL_ADD の*操作*引数を使用して**sqlsetpos**をサポートする必要が*あります。*|
