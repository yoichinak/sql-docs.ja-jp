---
description: 相対と絶対のスクロール
title: 相対スクロールと絶対スクロール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c7471e7ee245d9cf70adc8c3453705453bc1aac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482944"
---
# <a name="relative-and-absolute-scrolling"></a>相対と絶対のスクロール
**Sqlfetchscroll**のスクロールオプションのほとんどは、カーソルを現在の位置または絶対位置に相対的に配置します。 **Sqlfetchscroll** では、次、前、最初、および最後の行セットのフェッチと、相対フェッチ (現在の行セットの先頭から行セット *n* 行をフェッチ) と絶対フェッチ (行 *n*で始まる行セットのフェッチ) がサポートされています。 絶対フェッチで *n* が負の値の場合、行は結果セットの末尾からカウントされます。 したがって、行-1 の絶対フェッチは、結果セットの最後の行で始まる行セットをフェッチすることを意味します。  
  
 動的カーソルは、結果セットに挿入された行を検出します。そのため、動的カーソルは、結果セットの先頭からの読み取り以外の特定の数値で行を取得する簡単な方法はありません。 また、行が挿入および削除されると行番号が変化するため、動的カーソルでは絶対フェッチはあまり役に立ちません。そのため、同じ行番号を連続してフェッチすると、異なる行が生成される可能性があります。  
  
 レポートなどのブロックカーソル機能に対してのみ **Sqlfetchscroll** を使用するアプリケーションは、次の行セットをフェッチするオプションのみを使用して、結果セットを1回だけ通過する可能性があります。 一方、画面ベースのアプリケーションでは、 **Sqlfetchscroll**のすべての機能を利用できます。 アプリケーションで、行セットのサイズを画面に表示される行数に設定し、画面バッファーを結果セットにバインドすると、スクロールバーの操作を **Sqlfetchscroll**の呼び出しに直接変換できます。  
  
|スクロール バーの操作|SQLFetchScroll のスクロール操作|  
|--------------------------|-------------------------------------|  
|1 画面分上へ移動 (PageUp)|SQL_FETCH_PRIOR|  
|1 画面分下へ移動 (PageDown)|SQL_FETCH_NEXT|  
|1 行上へ移動|*Fetchoffset*が-1 に等しい SQL_FETCH_RELATIVE|  
|1 行下へ移動|*Fetchoffset*が1に等しい SQL_FETCH_RELATIVE|  
|一番上にスクロールボックス|SQL_FETCH_FIRST|  
|下のスクロールボックス|SQL_FETCH_LAST|  
|スクロール ボックスを任意の位置に移動|SQL_FETCH_ABSOLUTE|  
  
 このようなアプリケーションでは、スクロール操作の後に、現在の行番号と行数を必要とするスクロールボックスを配置する必要もあります。 現在の行番号については、アプリケーションは現在の行番号を追跡するか、SQL_ATTR_ROW_NUMBER 属性を使用して **SQLGetStmtAttr** を呼び出して取得することができます。  
  
 結果セットのサイズであるカーソル内の行の数は、診断ヘッダーの SQL_DIAG_CURSOR_ROW_COUNT フィールドとして使用できます。 このフィールドの値は、 **Sqlexecute**、 **SQLExecDirect**、または **SQLMoreResult** が呼び出された後にのみ定義されます。 この数には、ドライバーの機能に応じて概数または正確な数を指定できます。 ドライバーのサポートは、cursor 属性情報型を使用して **SQLGetInfo** を呼び出し、カーソルの種類に対して SQL_CA2_CRC_APPROXIMATE または SQL_CA2_CRC_EXACT ビットが返されるかどうかを確認することによって決定できます。  
  
 動的カーソルでは、正確な行数はサポートされません。 その他の種類のカーソルの場合、ドライバーは正確な行数または概数の行数をサポートできますが、両方をサポートすることはできません。 ドライバーが特定のカーソルの種類に対して正確な行カウントも概数値もサポートしていない場合、SQL_DIAG_CURSOR_ROW_COUNT フィールドには、これまでにフェッチされた行の数が含まれます。 ドライバーでサポートされている内容にかかわらず、 **Sqlfetchscroll** SQL_FETCH_LAST *操作* を使用すると、SQL_DIAG_CURSOR_ROW_COUNT フィールドに正確な行数が含まれます。
