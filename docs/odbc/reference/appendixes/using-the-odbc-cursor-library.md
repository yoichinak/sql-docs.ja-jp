---
description: ODBC カーソル ライブラリの使用
title: ODBC カーソルライブラリを使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be42c95692537c0479afb7ed492756b8a54ab030
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386198"
---
# <a name="using-the-odbc-cursor-library"></a>ODBC カーソル ライブラリの使用
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 ODBC カーソルライブラリを使用するには、次のアプリケーションを使用します。  
  
1.  SQL_ATTR_ODBC_CURSORS の*属性*を使用して**SQLSetConnectAttr**を呼び出し、特定の接続でカーソルライブラリを使用する方法を指定します。 カーソルライブラリは常に使用できます (SQL_CUR_USE_ODBC)。ドライバーがスクロール可能なカーソル (SQL_CUR_USE_IF_NEEDED) をサポートしていない場合、または使用されない場合 (SQL_CUR_USE_DRIVER) にのみ使用されます。  
  
2.  **SQLConnect**、 **SQLDriverConnect**、または**SQLBrowseConnect**を呼び出して、データソースに接続します。  
  
3.  **SQLSetStmtAttr**を呼び出して、カーソルの種類 (SQL_ATTR_CURSOR_TYPE)、同時実行 (SQL_ATTR_CONCURRENCY)、および行セットサイズ (SQL_ATTR_ROW_ARRAY_SIZE) を指定します。 カーソルライブラリでは、順方向専用カーソルと静的カーソルがサポートされています。 前方参照専用カーソルは読み取り専用である必要がありますが、静的カーソルは読み取り専用にすることも、オプティミスティック同時実行制御を使用して値を比較することもできます。  
  
4.  1つ以上の行セットバッファーを割り当て、 **SQLBindCol** を1回以上呼び出して、これらのバッファーを結果セット列にバインドします。  
  
5.  では、 **SELECT** ステートメントまたはプロシージャを実行するか、カタログ関数を呼び出すことによって、結果セットを生成します。 アプリケーションで位置指定更新ステートメントを実行する場合は、 **SELECT FOR update** ステートメントを実行して結果セットを生成する必要があります。  
  
6.  **Sqlfetch**または**sqlfetchscroll**を1回以上呼び出して、結果セットをスクロールします。  
  
 アプリケーションでは、行セットバッファー内のデータ値を変更できます。 カーソルライブラリのキャッシュのデータを使用して行セットバッファーを更新するには、アプリケーションは*Fetchorientation*引数を SQL_FETCH_RELATIVE に設定し、 *fetchoffset*引数を0に設定して**sqlfetchscroll**を呼び出します。  
  
 バインドされていない列からデータを取得するために、アプリケーションは **SQLSetPos** を呼び出して、カーソルを目的の行に配置します。 次に、 **SQLGetData** を呼び出してデータを取得します。  
  
 データソースから取得された行の数を確認するために、アプリケーションは **SQLRowCount**を呼び出します。
