---
description: SQLFetchScroll (カーソル ライブラリ)
title: SQLFetchScroll (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9783e2e0e7e5030aef0173a67cf8a4eac416242f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461654"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **Sqlfetchscroll** 関数の使用について説明します。 **Sqlfetchscroll**に関する一般的な情報については、「 [Sqlfetchscroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)」を参照してください。  
  
 カーソルライブラリは、ドライバーで**Sqlfetch**を繰り返し呼び出すことによって**sqlfetchscroll**を実装します。 このメソッドは、ドライバーから取得したデータを、アプリケーションによって提供される行セットバッファーに転送します。 また、メモリとディスクファイルにデータをキャッシュします。 アプリケーションが新しい行セットを要求すると、カーソルライブラリは、ドライバーから必要に応じて (まだフェッチされていない場合)、またはキャッシュ (既にフェッチされている場合) を取得します。 最後に、カーソルライブラリはキャッシュされたデータの状態を保持し、この情報を行ステータス配列のアプリケーションに返します。  
  
 カーソルライブラリを使用する場合、 **Sqlfetchscroll** の呼び出しと **Sqlfetch** または **SQLExtendedFetch**の呼び出しを混在させることはできません。  
  
 カーソルライブラリを使用すると、 **Sqlfetchscroll** の呼び出しが ODBC 2 でもサポートされます。*x* および ODBC 3 の場合。*x* ドライバー。  
  
## <a name="rowset-buffers"></a>行セットバッファー  
 カーソルライブラリは、次の場合に、ドライバーからアプリケーションによって提供される行セットバッファーへのデータの転送を最適化します。  
  
-   アプリケーションでは、行方向のバインドを使用します。  
  
-   データ行を保持するためにアプリケーションが宣言する構造体のフィールド間に未使用のバイトはありません。  
  
-   **Sqlfetch**または**sqlfetchscroll**が列の長さ/インジケーターを返すフィールドは、その列のバッファーに続き、次の列のバッファーの前に置かれます。 これらのフィールドは省略可能です。  
  
 アプリケーションが新しい行セットを要求すると、カーソルライブラリは必要に応じてキャッシュとドライバーからデータを取得します。 新しい行セットと古い行セットが重複している場合、カーソルライブラリでは、行セットバッファーの重複するセクションのデータを再利用することにより、パフォーマンスを最適化できます。 したがって、行セットバッファーに対する未保存の変更は、新しい行セットと古い行セットが重なっていて、変更が行セットバッファーの重複セクションにある場合を除き、失われます。 アプリケーションは、変更を保存するために、配置された update ステートメントを送信します。  
  
 アプリケーションが*Fetchorientation*引数を SQL_FETCH_RELATIVE に設定し、 *fetchoffset*引数を0に設定して**sqlfetchscroll**を呼び出すと、カーソルライブラリは常にキャッシュからのデータを使用して行セットバッファーを更新することに注意してください。  
  
 カーソルライブラリでは、カーソルが開いている間に行セットのサイズを変更するために SQL_ATTR_ROW_ARRAY_SIZE の*属性*を使用した**SQLSetStmtAttr**の呼び出しをサポートしています。 新しい行セットのサイズは、次に **Sqlfetchscroll** が呼び出されたときに有効になります。  
  
## <a name="result-set-membership"></a>結果セットのメンバーシップ  
 カーソルライブラリは、アプリケーションが要求したときにのみ、ドライバーからデータを取得します。 データソースと SQL_CONCURRENCY statement 属性の設定によっては、次のような結果になります。  
  
-   カーソルライブラリによって取得されるデータは、ステートメントの実行時に使用可能だったデータとは異なる場合があります。 たとえば、カーソルを開いた後、現在のカーソル位置を超えた時点で挿入された行は、一部のドライバーで取得できます。  
  
-   結果セットのデータは、カーソルライブラリのデータソースによってロックされている可能性があるため、他のユーザーが使用することはできません。  
  
 カーソルライブラリがデータ行をキャッシュした後で、基になるデータソース内のその行に対する変更を検出することはできません (同じカーソルのキャッシュで動作する位置指定更新と削除を除く)。 これは、 **Sqlfetchscroll**を呼び出すと、カーソルライブラリがデータソースからデータを refetches ことがないために発生します。 代わりに、キャッシュからデータを refetches します。  
  
## <a name="scrolling"></a>スクロール  
 カーソルライブラリでは、 **Sqlfetchscroll**で次のフェッチの種類がサポートされています。  
  
|カーソルの種類|フェッチの種類|  
|-----------------|-----------------|  
|順方向専用|SQL_FETCH_NEXT|  
|静的|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>エラー  
 **Sqlfetchscroll**が呼び出され、 **sqlfetch**の呼び出しの1つが SQL_ERROR を返すと、カーソルライブラリは次のように処理を続行します。 これらの手順が完了すると、カーソルライブラリは処理を続行します。  
  
1.  **SQLGetDiagRec**を呼び出してドライバーからエラー情報を取得し、それをドライバーマネージャーの診断レコードとして post します。  
  
2.  診断レコードの SQL_DIAG_ROW_NUMBER フィールドを適切な値に設定します。  
  
3.  診断レコードの SQL_DIAG_COLUMN_NUMBER フィールドを適切な値 (該当する場合) に設定します。それ以外の場合は0に設定されます。  
  
4.  行の状態配列でエラーになっている行の値を SQL_ROW_ERROR に設定します。  
  
 **Sqlfetchscroll**の実装でカーソルライブラリが**sqlfetch**を複数回呼び出した後、 **sqlfetch**への呼び出しのいずれかによって返されたエラーまたは警告は診断レコードに含まれ、 **SQLGetDiagRec**の呼び出しによって取得できます。 データがフェッチ時に切り捨てられた場合は、切り捨てられたデータがカーソルライブラリのキャッシュに格納されるようになります。 その後、 **Sqlfetchscroll** を呼び出して、切り捨てられたデータを含む行までスクロールすると、切り捨てられたデータが返されます。データがカーソルライブラリのキャッシュからフェッチされるため、警告は発生しません。 返されるデータの長さを追跡して、バッファーで返されたデータが切り捨てられているかどうかを判断できるようにするには、アプリケーションで長さ/インジケーターバッファーをバインドする必要があります。  
  
## <a name="bookmark-operations"></a>ブックマーク操作  
 カーソルライブラリでは、SQL_FETCH_BOOKMARK の*Fetchorientation*を使用した**sqlfetchscroll**の呼び出しをサポートしています。 また、bookmark 操作で使用できる *fetchoffset* 引数にオフセットを指定することもできます。 これは、カーソルライブラリがサポートする唯一のブックマーク操作です。 カーソルライブラリは、 **Sqlbulkoperations**の呼び出しをサポートしていません。  
  
 アプリケーションで SQL_ATTR_USE_BOOKMARKS statement 属性が設定されていて、が bookmark 列にバインドされている場合、カーソルライブラリは固定長のブックマークを生成し、それをアプリケーションに返します。 カーソルライブラリは、使用するブックマークを作成して管理します。データソースで管理されているブックマークは使用しません。 データソースから既にフェッチされているデータのブロックを取得するために **Sqlfetchscroll** が呼び出されると、カーソルライブラリキャッシュからデータを取得します。 その結果、SQL_FETCH_BOOKMARK の*Fetchorientation*を使用した**sqlfetchscroll**の呼び出しで使用されるブックマークは、カーソルライブラリによって作成および管理される必要があります。  
  
## <a name="interaction-with-other-functions"></a>他の関数との対話  
 アプリケーションは、位置指定の update ステートメントまたは delete ステートメントを準備または実行する前に、 **Sqlfetch** または **sqlfetchscroll** を呼び出す必要があります。
