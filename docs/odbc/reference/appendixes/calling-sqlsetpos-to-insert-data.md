---
description: データを挿入するための SQLSetPos の呼び出し
title: SQLSetPos を呼び出してデータを挿入しています |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 215d02e9b5bd92f6a22f7e45c8c29c7c5a0a6a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449014"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>データを挿入するための SQLSetPos の呼び出し
*Odbc 2.x アプリケーションで*odbc *3.x ドライバーを*使用する場合、SQL_ADD の*操作*引数を使用して**SQLSetPos**を呼び出すと、ドライバーマネージャーはこの呼び出しを**sqlbulkoperations**にマップしません。 ODBC *3. x* ドライバーが SQL_ADD で **SQLSetPos** を呼び出すアプリケーションで動作する必要がある場合、ドライバーはその操作をサポートする必要があります。  
  
 SQL_ADD で **SQLSetPos** が呼び出されたときの動作の大きな違いの1つは、状態 S6 で呼び出されたときに発生します。 *ODBC 2.x では、状態*が S6 (カーソルが**sqlfetch**で配置された後) の SQL_ADD で**SQLSetPos**が呼び出されたときに、ドライバーから S1010 が返されました。 ODBC 3.x では、SQL_ADD*操作*を伴う**sqlbulkoperations**を state S6 で呼び出すことができ*ます。* 動作の2つ目の大きな違いは、SQL_ADD*操作*を伴う**sqlbulkoperations**を状態 S5 で呼び出すことができることです。一方、SQL_ADD の**操作**では、 **SQLSetPos**を呼び出すことはできません。 ODBC 3.x で同じ呼び出しに対して発生する可能性のあるステートメントの遷移について*は、「*[付録 B: Odbc 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」を参照してください。
